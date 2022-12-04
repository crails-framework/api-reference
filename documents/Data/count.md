Counts the amount of children nodes for the current node.

```c++
DataTree root = DataTree().from_json("{\"array\": [1,2,3]");
Data node = root.as_data();

cout << node.count() << endl; // prints 1
cout << node["array"].count() << endl; // prints 3
```
