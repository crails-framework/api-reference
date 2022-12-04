Implementation of the [RequestParser] interface designed to intercept requests using the `crails/archive` format. The archive's content will be stored in the [Params] object under the `archive_data` key.

You may then initialize your [IArchive] objects as following:

```c++
void Router::initialize()
{
  match("POST", "/archive", [](Crails::Context& context, std::function<void()> callback)
  {
    IArchive archive;
    std::string raw_data = params["archive_data"].as<std::string>();

    archive.set_data(raw_data);
  });
}
```
