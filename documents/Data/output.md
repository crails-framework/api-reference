Prints debug information about the current node to the specified [std::ostream]. The content is serialized as JSON.

```c++
DataTree root = DataTree().from_json("{\"a\": 42}");
Data node = root.as_data();

node.output(std::cerr); // prints {"a":42} to the standard error stream
```
