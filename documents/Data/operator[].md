Returns a node based on its name. The node is returned and probed deeper, even if it doesn't exist: when modified, missing nodes will be recursively created.

```c++
DataTree root;
Data node = root["recursively"]["get"]["a"]["node"];

node = 42;
cout << root.to_json() << endl; // prints {"recursively":{"get":{"a":{"node":42}}}}
```
