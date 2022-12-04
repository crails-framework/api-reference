Removes the current node and all its children from the [DataTree].

```c++
DataTree root = DataTree().from_json("{\"a\": {\"b\": {\"c\": 42} } }");
Data node = root.as_data();

cout << root.to_json() << endl; // prints {"a":{"b":{"c":42}}}

node["a"]["b"].destroy();

cout << root.to_json() << endl; // prints {"a": ""}
```
