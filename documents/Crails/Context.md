The `Context` object is at the core of the Crails Framework, and represents a Request/Response transaction with an HTTP client. It provides both a [Params] and a [BuildingResponse] as attributes, so you can inspect the content of a request, and provide the details of your response.

You may access the request and response objects as provided by [Beast](https://www.boost.org/doc/libs/1_73_0/libs/beast/doc/html/beast/introduction.html) through the [Connection] object.

If the `Context` object gets destroyed before you manually send a response, then the response will be sent as-is.

This is important for asynchronous applications: when performing an asynchronous response, you must keep a reference to the request `Context` at least until the response is ready to be sent. This can be easily achieved by keeping an instance of [std::shared_ptr] around, using:

```c++
void handle_async_request(Crails::Context& context)
{
  std::shared_ptr<Crails::Context> ptr = context.shared_from_this();

  your_asynchronous_method([ptr]() // capturing shared_ptr as a copy
  {                                // will maintain the context alive
    ptr->response.send();          // at least until the lambda returns
  });
}
```


