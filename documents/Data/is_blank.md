Returns `true` if the current node is undefined or empty.

```c++
DataTree data = DataTree().from_json("{\"empty\": "", \"null\": null}");

cout << data["empty"].is_blank() << endl; // prints 1

cout << data["undefined"].is_blank() << endl; // prints 1

cout << data["null"].is_blank() << endl; // prints 0
```
