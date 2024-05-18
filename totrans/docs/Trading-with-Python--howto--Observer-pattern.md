<!--yml
category: 未分类
date: 2024-05-18 15:43:03
-->

# Trading with Python: howto: Observer pattern

> 来源：[http://tradingwithpython.blogspot.com/2011/12/howto-observer-pattern.html#0001-01-01](http://tradingwithpython.blogspot.com/2011/12/howto-observer-pattern.html#0001-01-01)

The

[observer pattern](http://en.wikipedia.org/wiki/Observer_pattern)

 comes very handy when dealing with complex systems. It allows for class-to class communication with a very simple structure. Even more important is the ability to separate functionality in different modules, for example running a single 'broker' as a wrapper to some api and letting multiple strategies subscribe to relevant broker events. There are some ready-made modules available, but the best way to understand how this process works is to write the whole system from scratch. In many languages this is a very tedious task, but thanks to the power of Python it only takes a couple of lines to do this.

The following example code creates a

*Sender*

 class (named Alice). Sender keeps track of interested listeners and notifies them accordingly. In more detail, this is achieved by a dictionary containing a function-event mapping, Sender.listeners.

A listener class can be of any type, here I make a bunch of

*ExampleListener*

 classes, named Bob,Dave & Charlie. All of them have a method, that is that is subscribed to

*Sender*

. The only special thing about the subscribed method is that it should contain three parameters:

*sender, event, message*

. Sender is the class reference of the

*Sender*

 class, so a listener would know who sent the message. Event is an identifier, for which I usually use a string. Optionally, a message is the data that is passed to a function.

A nice detail is that if a listener method throws an exception, it is automatically unsubscribed from further events.

```
'''
Created on 26 dec. 2011
Copyright: Jev Kuznetsov
License: BSD

sender-reciever pattern.

'''

import tradingWithPython.lib.logger as logger
import types

class Sender(object):
    """
    Sender -> dispatches messages to interested callables 
    """
    def __init__(self):
        self.listeners = {}
        self.logger = logger.getLogger()

    def register(self,listener,events=None):
        """
        register a listener function

        Parameters
        -----------
        listener : external listener function
        events  : tuple or list of relevant events (default=None)
        """
        if events is not None and type(events) not in (types.TupleType,types.ListType):
            events = (events,)

        self.listeners[listener] = events

    def dispatch(self,event=None, msg=None):
        """notify listeners """
        for listener,events in self.listeners.items():
            if events is None or event is None or event in events:
                try:
                    listener(self,event,msg)
                except (Exception,):
                    self.unregister(listener)
                    errmsg = "Exception in message dispatch: Handler '{0}' unregistered for event '{1}'  ".format(listener.func_name,event)
                    self.logger.exception(errmsg)

    def unregister(self,listener):
        """ unregister listener function """
        del self.listeners[listener]             

#---------------test functions--------------

class ExampleListener(object):
    def __init__(self,name=None):
        self.name = name

    def method(self,sender,event,msg=None):
        print "[{0}] got event {1} with message {2}".format(self.name,event,msg)

if __name__=="__main__":
    print 'demonstrating event system'

    alice = Sender()
    bob = ExampleListener('bob')
    charlie = ExampleListener('charlie')
    dave = ExampleListener('dave')

    # add subscribers to messages from alice
    alice.register(bob.method,events='event1') # listen to 'event1'
    alice.register(charlie.method,events ='event2') # listen to 'event2'
    alice.register(dave.method) # listen to all events

    # dispatch some events
    alice.dispatch(event='event1')
    alice.dispatch(event='event2',msg=[1,2,3])
    alice.dispatch(msg='attention to all')

    print 'Done.'

```