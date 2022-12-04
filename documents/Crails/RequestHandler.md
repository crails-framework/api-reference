Interface for request handlers. Request handlers are [functors](https://www.geeksforgeeks.org/functors-in-cpp) which receive a [Context] and a callback as parameters.

The request handler may then transform the content of a [BuildingResponse] object based on the contents of an [HttpRequest], both provided by the [Context].

Request handlers can be asynchronous. When they are, don't forget to keep a [std::shared_ptr<Context>] around. You can get a handle on one of those by calling `shared_from_this` on the [Context].

For more informations, check out the [Request Pipeline Manual](https://crails-framework.github.io/website/request_pipeline/#header_2).
