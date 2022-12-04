Returns `true` if a node is defined, `false` otherwise.

```c++
DataTree root = DataTree().from_json("{\"a\":1, \"b\":null}");
Data node = root.as_data();

node.exists(); // returns true
node["a"].exists(); // returns true
node["b"].exists(); // returns true
node["c"].exists(); // returns false
```
