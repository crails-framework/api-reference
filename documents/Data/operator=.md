Assigns a value to the current node. If the value has the `Data` type, then instead of changing the value of the current node, it changes the node which the `Data` object points to.

Value assignment:

```c++
DataTree root = DataTree().from_json("{\"a\": {\"b\": 1, \"c\": 2 } }");
Data b = root["a"]["b"];
Data c = root["a"]["c"];

cout << b.as<int>() << endl; // prints 1

b = c.as<int>();

cout << b.as<int>() << endl; // prints 2

cout << root.to_json() << endl; // prints {"a":{"b":2,"c":2}}
```

Node assignment:

```c++
DataTree root = DataTree().from_json("{\"a\": {\"b\": 1, \"c\": 2 } }");
Data b = root["a"]["b"];
Data c = root["a"]["c"];

cout << b.get_path() << endl; // prints a.b

b = c;

cout << b.get_path() << endl; // prints a.c

cout << root.to_json() << endl; // prints {"a":{"b":1,"c":2}} (the data hasn't been modified)
```
