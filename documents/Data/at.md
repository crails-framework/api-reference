Returns a node by index. It can be used to iterate over a list of nodes:

```c++
DataTree root = DataTree().from_json("{\"first\": 1, \"second\": 2, \"third\": 3}");
Data node = root.as_data();

for (int i = 0 ; i < node.count() ; ++i)
{
  Data node_at = node.at(i);
  cout << node_at.get_key() << " -> " << node_at.as<int>() << endl;
}
// prints
//  first -> 1
//  second -> 2
//  third -> 3
```

It's also the only way to iterate over an array node, where sub-nodes have no key:

```c++
DataTree root = DataTree().from_json("{\"array\":[ 1, 2, 3]});
Data node = root["array"];

for (int i = 0 ; i < node.count() ; ++i)
{
  Data node_at = node.at(i);
  cout << node_at.get_key() << " -> " << node_as<int>() << endl;
}
// prints
//  -> 1
//  -> 2
//  -> 3
```
