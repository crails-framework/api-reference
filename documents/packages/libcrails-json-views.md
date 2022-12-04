Implements [Crails::Renderer] and [Crails::Template] for JSON documents, including a Domain-Specific Language for generating JSON with the [ecpp](https://github.com/crails-framework/ecpp) generator:

```c++
json("key", "value");

json_array("array", std::vector<int>{
  1, 2, 3, 4
});

json_map("map", std::map<std::string, std::string>{
  {"1", "One"}, {"2", "Two"}, {"3", "Three"}
});
```

This template would result in the following JSON document:

```json
{"key":"value","array":[1,2,3,4],"map":{"1":"One","2":"Two","3":"Three"}}
```

When generating object arrays or object maps, use a callback with `json_array` or `json_map`:

```c++
std::vector<int> array = std::vector<int>{1,2,3,4};
std::map<std::string, std::string> map = std::map<std::string, std::string>{
  {"1", "One"}, {"2", "Two"}, {"3", "Three"}
};

// END LINKING

json_array("custom_array", array, [&](int value)
{
  json("number", value);
});

json_map("custom_map", map, [&](int value)
{
  json("number", value);
});
```
