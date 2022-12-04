Represents the parameters of an HTTP query as an arbitrarily deeply neested tree of values. `Params` extends on the [DataTree] class, using the same API to access its contents.

##### Params within the Crails Framework

`Params` objects are typically provided by a [Crails::Context] or a [Crails::ActionController]:

```c++
// Using Context
void MyRequestHandler::operator()(Crails::Context& context, std::function<void(bool)> callback)
{
  const Crails::Params& params = context.params;

  if (params["number"].as<int>() > 50)
  {
    context.response.set_response(Crails::HttpStatus::ok, "Hello, world!");
    callback(true);
  }
  else
    callback(false);
}

// Using Controllers
class MyController : public Crails::Controller
{
public:
  MyController(Crails::Context& context) : Controller(context) {}

  void show()
  {
    if (params["number"].as<int>() > 50)
      render(TEXT, "Hello world!");
  }
};
```

##### How data is added to Params

What will be aggregated within a `Params` object depends on the [RequestParser] implementations that have been added to your [Request Pipeline](https://crails-framework.github.io/website/request_pipeline/).

For instance, when the [RequestUrlParser] is enabled, URL parameters will be aggregated:

```c++
// GET /path?param=value&number=51 HTTP/1.1
void inspect_params(Crails::Params& params)
{
  cout << params["param"].as<std::string>() << endl; // prints: value
  cout << params["number"].as<std::string>() << endl; // prints: 51
}
```

##### File uploads

The `Params` object also holds references to uploaded files. File uploads can be handled by the [RequestMultipartParser].

The uploaded files can be accessed using the field name that was used by the client using `get_upload`:

```c++
// For <input type="file" name="myfile" />:
Params::File* file = params.get_upload("myfile");

if (file != nullptr)
  std::filesystem::copy_file(file.temporary_path, "/var/www/persistent-storange/myfile");
```

You can also access the list of all the files uploaded within the query using `get_files`:

```c++
for (const Params::File& file : params.get_files())
  std::filesystem::copy_file(file.temporary_path, "/var/www/persistent-storage/" + file.name);
```
