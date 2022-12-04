The `DataTree` class provides a data structure that stores an arbitrarily deeply nested tree of values, indexed at each level by some key. Each node of the tree stores its own value, or a list of subnodes and their keys.

The content of a `DataTree` can be explored using [Data] nodes, referenced either by key or index:

```c++
DataTree root;
Data node = root["path"]["to"]["a"]["node"];

node = "Hello, world!";
```

A `DataTree` can be populated programmatically, or can be loaded from JSON and XML strings or files:

```c++
DataTree root;

root.from_json_file("/tmp/file.json");
// or
root.from_json("[1,2,3]");
```

Two implementations of `DataTree` co-exists:
- The _Crails_ implementation is based on [boost's property_tree library](https://www.boost.org/doc/libs/master/doc/html/property_tree.html)
- The _Comet_ implementation is based on JavaScript's [Object](https://developer.mozilla.org/fr/docs/Web/JavaScript/Reference/Global_Objects/Object)

This documentation targets the _Crails_ implementation, but both provide the same API, except for the methods allowing access to the underlying _property tree_ or _JavaScript Object_.
