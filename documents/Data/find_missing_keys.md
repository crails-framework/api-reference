Filter a list of keys, and returns only the ones that don't match a direct child of the current node.

```c++
DataTree root = DataTree().from_json("{\"hello\": 1, \"world\": 2}");
Data node = root.as_data();
std::vector<std::string> missing_keys;

missing_keys = node.find_missing_keys({"hello", "world", "!"}); // returns {"!"}
```
