<!--yml
category: 未分类
date: 2024-05-12 19:44:53
-->

# Calling IronPython from C# using delegates | Coding the markets

> 来源：[https://etrading.wordpress.com/2007/10/30/calling-ironpython-from-c-using-delegates/#0001-01-01](https://etrading.wordpress.com/2007/10/30/calling-ironpython-from-c-using-delegates/#0001-01-01)

## Calling IronPython from C# using delegates

### October 30, 2007

I wanted to wrap a C# WinForms object in a Python dictionary, so I could make it look like a dictionary by implenting __getitem__ and __contains__ using hasattr() and getattr(). I’d been using generic EventHandlers to dispatch from C# to Python quite happily to date. But the __contains__ implementation needs to return a bool, which doesn’t fit with the event handler model. [This post](http://www.mail-archive.com/users@lists.ironpython.com/msg01986.html) showed me the way. Here’s the code…

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