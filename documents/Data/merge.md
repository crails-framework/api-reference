Recursively merges the contents of the parameter node or tree into the current node.

```c++
DataTree rootA = DataTree().from_json("{\"a\": {\"b\": {\"c\": 42} } }");
DataTree rootB = DataTree().from_json("{\"d\": {\"e\": {\"f\": 42} } }");
Data node = rootA.as_data();

cout << root.to_json() << endl; // prints: {"a":{"b":{"c":42}}}

node.merge(rootB);

cout << root.to_json() << endl; // prints {"a":{"b":{"c":42}},"d":{"e":{"f":42}}}

```

Merging a node with itself or one of its parents is safe:

```c++
DataTree root = DataTree().from_json("{\"a\": {\"b\": {\"c\": 42} } }");
Data node = root.as_data();

node.merge(node); // that does nothing

cout << root.to_json() << endl; // prints: {"a":{"b":{"c":42}}}
node["a"]["b"].merge(node["a"]); // merging a node with one of its own parents
cout << root.to_json() << endl; // prints: {"a":{"b":{"c":42,"b":{"c":42}}}}
```
