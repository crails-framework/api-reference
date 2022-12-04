Dynamic try/catch mechanism. Define catch blocks using [std::function], then run protected code anywhere else in your application.

##### Request Pipeline

`ExceptionCatcher` is used in the [Request Pipeline](https://crails-framework.github.io/website/request_pipeline) to catch exceptions thrown when parsing or handling a request.

Exception catchers can typically be added in the `config/request_pipe.cpp` file, when defining the `initialize_request_pipe` method, such as:

```c++
void Server::initialize_request_pipe()
{
  exception_catcher.add_exception_catcher<std::logic_error>(
    [](Crails::Context& context, const std::logic_error&)
    {
      context.response.set_header(Crails::HttpHeader::content_type, "text/plain");
      context.response.set_response(Crails::HttpStatus::internal_server_error, "Oh snap!");
      context.response.send();
    }
  );
}
```

##### Asynchronous usage

When handling responses asynchronously, you should remember to wrap your asynchronous code in an exception catcher. This should be done using [Context::protect](#/classes/::Crails::Context/protect):

```c++
class MyRequestHandler : public Crails::RequestHandler
{
public:
  MyRequestHandler() : Crails::RequestHandler("my-request-handler") {}

  void operator()(Crails::Context& context, std::function<void(bool)> callback) const override
  {
    auto async_callback = std::bind(async_code, context_ref.shared_from_this(), callback);

    std::thread([&context, async_callback]()
    {
      context->protect(async_callback);
    }).detach();
  }

  static void async_code(std::shared_ptr<Crails::Context> context, std::function<void(bool)> callback)
  {
    context->response.set_response(Crails::HttpHeader::ok, "ok");
    callback(true);
  }
};
```

Note that before exception catcher callbacks are run, the `mutex` field from the [Context] class is locked using [std::lock_guard]. Similarly, the `protect` method also locks the same mutex. This means that by using the `protect` method within your own threads, you can interact with the [Context] object in a thread-safe fashion.

###### Issues

An exception catcher may be called several times for the same [Context]. This will happen when a thread throws an exception after having handed the [Context] instance to another thread. The results might be unexpected, as each `catch` callback may provide their own HTTP response.

To take this into account, you may check whether a response has already been provided by using the [BuildingResponse::sent](#/classes/::Crails::BuildingResponse/sent) method, through the [Context::response](#/classes/::Crails::Context/response) field.

##### Re-entrency

The catching mechanism won't trigger multiple times if you make consecutive calls to the `protect` method from the same thread. It will only trigger again whenever you're swaping from one thread to another.

