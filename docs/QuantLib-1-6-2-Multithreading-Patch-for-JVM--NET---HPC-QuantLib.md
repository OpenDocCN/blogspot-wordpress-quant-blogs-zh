<!--yml

分类：未分类

日期：2024-05-17 23:30:00

-->

# 量子库 1.6.2 JVM/.NET 多线程补丁 – HPC-QuantLib

> 来源：[`hpcquantlib.wordpress.com/2015/09/20/quantlib-1-6-2-multithreading-patch-for-jvm-net/#0001-01-01`](https://hpcquantlib.wordpress.com/2015/09/20/quantlib-1-6-2-multithreading-patch-for-jvm-net/#0001-01-01)

更新 2015 年 11 月 23 日：修改后的补丁现在已是量子库官方发布 1.7 的一部分。

量子库观察者模式的实现不允许多线程的并行垃圾回收器运行。这可能会导致随机崩溃或在使用 JVM 和.NET 语言（例如 Java/Scala 和 C#/F#）通过 SWIG 接口使用量子库时产生“纯虚函数调用”。关于这个问题的原始描述可以例如在这里找到[](https://hpcquantlib.wordpress.com/2012/02/27/quantlib-swig-and-a-thread-safe-observer-pattern-in-c/)和参考文献中。

从版本 1.58 开始，boost 库扩展了类 boost::enable_shared_from_this<T>的接口，增加了方法

```
weak_ptr<T> weak_from_this() noexcept;

```

该方法提供了对实现“从 this 获取共享指针”功能的底层弱指针的访问。现在，这个补丁使得量子库的观察者模式线程安全变得更为干净、更容易安装。特别是，不再需要定义预处理器定义或编辑 boost 文件。

实现得到了 boost::signals2 的支持，以线程安全的方式实现观察者模式。boost::signals2 库完全基于 shared_ptr。因此，第一步是向量子库的观察者中添加一个 Observer::Proxy 类，该类可以注册到 boost::signals2，并将其更新调用转发给相应的观察者。此外，类 Observer 现在从 boost::enable_shared_from_this 派生。

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

原始实现中竞态条件的关键路径是在观察者的析构函数被调用时，同时可观察对象触发更新调用。现在，如果观察者的析构函数能够获取与代理的更新方法相同的互斥锁，观察者的析构函数将禁用代理。如果代理被禁用，它将不会将任何更新调用转发给即将被删除的观察者。

如果更新调用成功获取了互斥锁，那么它将延迟任何并发观察者的析构函数调用。因此，尝试从第 27 行的与代理关联的观察者中获取底层弱指针是安全的。如果以前没有从观察者创建共享指针，这个弱指针可能是空的。如果存在弱指针，代理将尝试获取共享指针并从那里调用更新方法。这一部分遵循了[1]中概述的方法论。剩余的实现继承了 boost signals2 库的线程安全性。

针对 QuantLib 1.6.2 的补丁可在此[链接](http://hpc-quantlib.de/src/observer-1.6.2.zip)找到。该补丁还包括 Riccardo 的线程安全单例补丁，并需要 boost 版本 1.58 或更高。

陈硕的演讲稿《析构函数与线程的相遇](http://www.slideshare.net/chenshuo/where-destructors-meet-threads)》
