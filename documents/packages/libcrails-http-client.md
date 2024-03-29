[Beast](https://www.boost.org/doc/libs/1_73_0/libs/beast/doc/html/index.html) based library providing HTTP clients with both synchronous and asynchronous request support.

Vanilla HTTP requests are done using the [Crails::Client] class, while HTTP requests with SSL are done using the [Crails::Ssl::Client] class.

#### Synchronous API:

Performing HTTP request synchronously is pretty simple. The types used for representing requests and responses are [Crails::HttpRequest] and [Crails::HttpResponse].

Don't forget to call the `connect` method before performing any query:

```c++
Crails::Ssl::Client http("duckduckgo.com", 443);
Crails::HttpRequest request{
  Crails::HttpVerb::get,
  "/?q=Hello%20World",
  11
};
Crails::HttpResponse response;

http.connect();
request.set(Crails::HttpHeader::host, "duckduckgo.com");
response = http.query(request);
```

#### Asynchronous API:

With the asynchronous API, you must remember to keep an instance of the `Client` object so that it doesn't get removed as it goes out of scope.

In the following example, we achieve this result by using `std::make_shared`, and storing the resulting smart pointer in the [closure](https://en.wikipedia.org/wiki/Closure_%28computer_programming%29) of our callback:

```c++
auto http = std::make_shared<Crails::Ssl::Client>("duckduckgo.com", 443);
Crails::HttpRequest request{
  Crails::HttpVerb::get,
  "/?q=Hello%20World",
  11
};

http.connect();
request.set(Crails::HttpHeader::host, "duckduckgo.com");
http.async_query(request, [http](const Crails::HttpRespones& response, boost::beast::error_code ec)
{
  ...
});
```

#### Controller component:

This package also includes [Crails::QueryController], a _controller component_ that you may use with the [libcrails-controllers package](#/packages/libcrails-controllers/namespaces)
to safely run both synchronous or asynchronous HTTP queries from your controllers:

```c++
class MyController : public Crails::QueryController<>
{
public:
  MyController(Crails::Context& context) : Crails::QueryController(context) {}

  void my_query_action()
  {
    auto url = Crails::Url::from_string("https://duckduckgo.com/q?=Hello%20World");
    http_async_query(url, [this](const Crails::HttpResponse& response, boost::beast::error_code)
    {
      render(HTML, response.body());
    });
  }
};
```
