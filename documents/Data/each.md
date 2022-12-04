Loops over the direct children of the current node, calling the parameter [std::function] for each of them.

```c++
DataTree root = DataTree().from_json("{\"a\": 1, \"b\": 2, \"c\": 3});
Data node = root.as_data();

node.each([](Data child)
{
  cout << child.as<int>() << ' ' << endl;
  return true;
});
cout << endl;
// prints: 1 2 3
```

The callback can break the loop by returning `false`:

```c++
DataTree root = DataTree().from_json("{\"a\": 1, \"b\": 2, \"c\": 3});
Data node = root.as_data();

node.each([](Data child)
{
  cout << child.as<int>() << ' ';
  return child.as<int> < 2;
});
cout << endl;
// prints: 1 2
```

Also works to iterate over arrays:

```c++
DataTree root = DataTree().from_json("[1,2,3]");
Data node = root.as_data();

node.each([](Data child)
{
  cout << child.as<int>() << ' ';
  return true;
});
cout << endl;
// prints: 1 2 3
```
