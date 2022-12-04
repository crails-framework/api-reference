Returns `true` when all the keys specified as parameters are defined in the current node.

```c++
DataTree root = DataTree().from_json("{\"hello\": 1, \"world\": 2});
Data node = root.as_data();

node.require({"hello", "world"}); // evaluates to true
node.require({"hello", "world", "!"}); // evaluates to false
```
