Adds error monitoring by capturing exceptions and sending them to a [Sentry](https://sentry.io) server.

##### How to use

To add the plugin to your crails application, you can use the `crails` command:

```sh
crails plugins sentry install
```

You may then add an exception catcher in `config/request_pipe.cpp`:

```c++
void Server::initialize_request_pipe()
{
  ...
  exception_catcher.add_exception_catcher<std::exception&>(
    [this](Crails::Context& context, const std::exception& error)
    {
      std::stringstream stream;

      Sentry::capture_exception(context.params.as_data(), error);
      stream << boost_ext::trace(error); // if the exception type supports it, generates a backtrace
      exception_catcher.default_exception_handler(context, typeid(error).name(), error.what(), stream.str());
    }
  );
}
```

To configure the Sentry server that'll be collecting your errors, see the `config/sentry.cpp` file.
