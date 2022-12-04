Loads `application/json` request bodies into [Crails::Params] with an implementation of [Crails::RequestParser].

For instance, the following document:

```json
{
  "hash": {
    "key": "value"
  },
  "array": [1, 2, 3]
}
```

Will be accessed with [Crails::Params] as such:

```c++
void output_json(const Crails::Params& params)
{
  std::string value = params["hash"]["key"].as<std::string>();

  std::vector<int> array = params["array"].to_vector<int>();
}
```
