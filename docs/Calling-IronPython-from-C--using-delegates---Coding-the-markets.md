<!--yml

category: 未分类

date: 2024-05-12 19:44:53

-->

# 从 C# 中使用委托调用 IronPython | 编码市场

> 来源：[`etrading.wordpress.com/2007/10/30/calling-ironpython-from-c-using-delegates/#0001-01-01`](https://etrading.wordpress.com/2007/10/30/calling-ironpython-from-c-using-delegates/#0001-01-01)

## 从 C# 中调用 IronPython 使用委托

### 2007 年 10 月 30 日

我想将一个 C# WinForms 对象封装在一个 Python 字典中，这样我就可以通过使用 hasattr() 和 getattr() 来实现 __getitem__ 和 __contains__，使其看起来像一个字典。到目前为止，我一直很愉快地使用通用的 EventHandlers 来从 C# 分派到 Python。但是 __contains__ 的实现需要返回一个布尔值，这与事件处理程序模型不符。[这篇文章](http://www.mail-archive.com/users@lists.ironpython.com/msg01986.html) 给了我指引。这是代码…

```
 using IronPython.Runtime.Operations;

// DictAdapter puts a read only C# dictionary interface on any
// Python object, which may actaully be a C# object in turn.
public class CsDictAdapter : IDictionary {

#region Delegates
public delegate object  GetItem( object key);
public delegate bool    HasItem( object key);

public GetItem __getitem__;
public HasItem __contains__;
#endregion

#region Constructors
public CsDictAdapter( object gi, object hi) {
this.__getitem__ = ( GetItem)Ops.GetDelegate(gi, typeof(GetItem));
this.__contains__ = ( HasItem)Ops.GetDelegate(hi, typeof(HasItem));
}
#endregion

#region Properties
public object this[object key] {
get { return __getitem__(key); }
set { }
}

public ICollection Keys {
get { return null; }
}

public ICollection Values {
get { return null; }
}

public int Count {
get { return 0; }
}

public bool IsReadOnly {
get { return true; }
}

public bool IsFixedSize {
get { return true; }
}

public Object SyncRoot {
get { return this; }
}

public bool IsSynchronized {
get { return false; }
}
#endregion

// Delegating implementations of all other methods.

#region Interface methods
public void Remove(Object key) { }
public void Add(Object key, Object value) { }

public bool ContainsKey( Object key) {
return __contains__( key);
}

public bool Contains( Object key) {
return __contains__( key);
}

public void Clear() { }

public int Add(Object item) {
return 0;
}

public void CopyTo(Object[] array, int arrayIndex) { }

public void CopyTo( System.Array array, int arrayIndex ) { }

IDictionaryEnumerator IDictionary.GetEnumerator( ) {
return null;
}

IEnumerator IEnumerable.GetEnumerator( ) {
return null;
}
#endregion
} 

```
