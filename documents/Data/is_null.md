Returns `true` if the current node is undefined or equal to "null":

```c++
DataTree data = DataTree().from_json("{\"key\": null}");
Data node = data["key"];

cout << node.as<std::string>() << endl; // prints "null"

cout << node.is_null() << endl; // prints 1

node = 1;

cout << node.is_null() << endl; // prints 0

data.from_json("{\"key\": \"null\"}");

cout << node.is_null() << endl; // prints 1
```
