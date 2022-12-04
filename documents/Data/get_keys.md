Returns the keys of all the direct children of the current node.

```c++
DataTree root = DataTree().from_json("{\"a\": {\"b\": 21, \"c\": 42}}");
Data node = root["a"].as_data();

node.get_keys(); // returns {"b","c"}

root.as_data().get_keys(); // returns {"a"}
```
