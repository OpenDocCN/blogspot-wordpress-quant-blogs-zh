<!--yml

分类：未分类

date: 2024-05-18 15:43:03

-->

# Python 交易：如何：观察者模式

> 来源：[`tradingwithpython.blogspot.com/2011/12/howto-observer-pattern.html#0001-01-01`](http://tradingwithpython.blogspot.com/2011/12/howto-observer-pattern.html#0001-01-01)

The

[观察者模式](http://en.wikipedia.org/wiki/Observer_pattern)

在处理复杂系统时非常有用。它允许类与类之间进行通信，结构非常简单。更重要的是，它允许将功能分离到不同的模块中，例如运行一个单独的'经纪人'作为某些 API 的包装器，并让多个策略订阅相关经纪人的事件。有一些现成的模块可用，但理解这个过程的最好方法是从头写整个系统。在许多语言中这是非常繁琐的任务，但多亏了 Python 的力量，只需几行代码就可以完成。

以下示例代码创建了一个

*发送者*

类（名为 Alice）。发送者跟踪感兴趣的监听器并相应地通知它们。更详细地说，这是通过包含函数-事件映射的字典实现的，即发送者的监听器列表。

一个监听器类可以是任何类型，在这里我创建了一组

*示例监听器*

类，名为 Bob、Dave 和 Charlie。它们都有一个方法，那就是订阅了

*发送者*

。订阅方法的特殊之处在于，它应该包含三个参数：

*发送者、事件、消息*

。发送者是

*发送者*

类，因此监听器知道是谁发送的消息。事件是一个标识符，我通常使用字符串来表示。可选地，消息是传递给函数的数据。

一个好的细节是，如果一个监听器方法抛出异常，它会自动从进一步的事件中取消订阅。

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
