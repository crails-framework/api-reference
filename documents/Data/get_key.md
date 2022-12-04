Returns the key of the current node as a [std::string].

```c++
DataTree root = DataTree().from_json("{\"a\": {\"b\": {\"c\": 1} } }");

cout << root["a"]["b"] << endl; // prints b
cout << root["a"]["b"]["c"] << endl; // prints c
cout << root["a"]["undefined"] << endl; // prints undefined
```
