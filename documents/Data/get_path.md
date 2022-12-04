Returns the entire path from the root node to the current node. The result is returned as [std::string], with each node key separated by a dot.

```c++
DataTree root = DataTree().from_json("{\"a\": {\"b": { \"c\": 1 } } }");
Data node = root["a"]["b"]["c"];

cout << node.get_path() << " = " << node.as<int>() << endl; // prints: "a.b.c = 1"
```
