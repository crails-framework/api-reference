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

To configure the Sentry server, you'll need to set a few environment variables:
`SENTRY_PROJECT_ID`, `SENTRY_KEY` and `SENTRY_SECRET`. You can find the values
for two of these variables in your DSN URL. Given the following DSN:

```
https://abc15de242fa392bc37ef420ab9720cd@o114303.ingest.us.sentry.io/4850190234743225
```

The values for the configuration variables would be:

- `SENTRY_PROJECT_ID` = `4850190234743225`
- `SENTRY_KEY` = `abc15de242fa392bc37ef420ab9720cd@o114303`

As for the third `SENTRY_SECRET` variable, its value can be found in Sentry's
project settings under the "Security Token" field.
