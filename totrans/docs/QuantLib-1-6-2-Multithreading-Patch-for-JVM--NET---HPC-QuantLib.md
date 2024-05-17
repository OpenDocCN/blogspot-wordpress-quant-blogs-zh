<!--yml
category: 未分类
date: 2024-05-17 23:30:00
-->

# QuantLib 1.6.2 Multithreading Patch for JVM/.NET – HPC-QuantLib

> 来源：[https://hpcquantlib.wordpress.com/2015/09/20/quantlib-1-6-2-multithreading-patch-for-jvm-net/#0001-01-01](https://hpcquantlib.wordpress.com/2015/09/20/quantlib-1-6-2-multithreading-patch-for-jvm-net/#0001-01-01)

Update 23.11.2015: A modified version of the patch is now part of the official QuantLib Release 1.7.

The implementation of QuantLib’s observer pattern does not tolerate a parallel garbage collector running in a different thread. This can lead to random crashes or producing “pure virtual function calls” when using QuantLib in JVM and .NET languages (e.g. Java/Scala and C#/F#) via the SWIG interface. An original description of this problem can be found e.g. [here](https://hpcquantlib.wordpress.com/2012/02/27/quantlib-swig-and-a-thread-safe-observer-pattern-in-c/) and within the references.

With the version 1.58 and higher the boost library has extended the interface of class boost::enable_shared_from_this<T> by the method

```
weak_ptr<T> weak_from_this() noexcept;

```

which gives access to the underlying weak pointer used to implement the “shared pointer from this” functionality. This method now allows for a much cleaner and easier to install patch to make QuantLib’s observer pattern thread safe. Especially it is no longer necessary to define preprocessor defines or to edit boost files.

The implementation is backed by boost::signals2 to get the observer pattern working in a thread safe manner. The boost::signals2 library works purely based on shared_ptr. Therefore the first step is to add an Observer::Proxy class to QuantLib’s Observer, which can be registered with boost::signals2 and which forwards the update calls to the corresponding observer. In addition the class Observer is now derived from boost::enable_shared_from_this.

```
class Observer : public boost::enable_shared_from_this<Observer> {
          friend class Observable;
  public:
    // public interface remains untouched

    virtual ~Observer() {
        boost::lock_guard<boost::recursive_mutex> lock(mutex_);
        if (proxy_) {
            proxy_->deactivate();

            for (iterator i=observables_.begin(); 
                 i!=observables_.end(); ++i) 
                (*i)->unregisterObserver(proxy_);
        }
    }
  private:
    class Proxy {
      public:
        Proxy(Observer* const observer)
         : active_  (true),
           observer_(observer) {
        }

        void update() const {
            boost::lock_guard<boost::recursive_mutex> lock(mutex_);
            if (active_) {
                const boost::weak_ptr<Observer> o
                    = observer_->weak_from_this();
                if (!o._empty()) {
                    boost::shared_ptr<Observer> obs(o.lock());
                    if (obs)
                        obs->update();
                }
                else {
                    observer_->update();
                }
            }
        }

        void deactivate() {
            boost::lock_guard<boost::recursive_mutex> lock(mutex_);
            active_ = false;
        }

    private:
        bool active_;
        mutable boost::recursive_mutex mutex_;
        Observer* const observer_;
    };

    boost::shared_ptr<Proxy> proxy_;
    mutable boost::recursive_mutex mutex_;

    std::set<boost::shared_ptr<Observable> > observables_;
    typedef std::set<boost::shared_ptr >::iterator 
        iterator;
};
```

The critical path for the race condition in the original implementation is when the destructor of an observer is called while an observable triggers an update call. Now the destructor of an observer deactivates the proxy if the destructor is able to get the same mutex lock as the update method of the proxy acquires. If the proxy gets deactivated it will not forward any update calls to the observer which is about to be deleted.

If the update call manages to acquire the mutex lock then it will delay any concurrent observer destructor calls. Therefore it is safe trying to get the underlying weak pointer from the observer linked to the proxy in line 27\. This weak pointer can be empty if no shared pointer has been created from the observer in the past. If a weak pointer exists then the proxy tries to get the shared pointer and calls the update methods from there. This part follows the same methodology as outlined in [1}. The rest of the implementation inherits the thread safeness from the boost signals2 library.

The patch for QuantLib 1.6.2 can be found [here](http://hpc-quantlib.de/src/observer-1.6.2.zip). It also contains Riccardo’s thread-safe singleton patch and it requires boost version 1.58 or higher.

[1] Shuo Chen, [Where Destructors meet Threads](http://www.slideshare.net/chenshuo/where-destructors-meet-threads)