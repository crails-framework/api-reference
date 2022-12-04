Interface for [RequestParser] implementations that need the body of an [HttpRequest] to be available before performing their task.

The [Request Pipe](https://crails-framework.github.io/website/request_pipeline/) may start evaluating an [HttpRequest] right when the headers of the request are fetch. At this point, the body of the request may not have been entirely received.

Implementations of `BodyParser` are expected to provide an implementation for the `body_received` method, which receives as parameters a reference to the current [Context], and the body of the request presented as [std::string].

When a parser needs to consult the body of a request, it _must_ call the `wait_for_body` method with the current [Context] and a callback. Once the body is available, the `body_received` virtual method will be called, followed by the callback sent as parameter.

Example:

```c++
class MyBodyParser : public Crails::BodyParser
{
  void operator()(
    Crails::Context& context,
    std::function<void(Crails::RequestParser::Status)> callback) const
  {
    wait_for_body(context, std::bind(callback, Crails::RequestParser::Stop));
  }

  void body_received(Crails::Context& context, const std::string& body) const
  {
    // parse the request body over here
  }
};
```
