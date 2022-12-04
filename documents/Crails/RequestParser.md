Interface for request parsers. Request parsers are [functors](https://www.geeksforgeeks.org/functors-in-cpp) which receive a [Context] and a callback as parameters.

The request parser may read the content of a [HttpRequest] object, and is expected to fill the [Params] object with the data they were able to glean from it. Once a request parser ends its task, it may report one of the three [RequestParser::Status] to the calling [Context]:

- `Continue` will keep parsing the request with other parsers,
- `Stop` will consider that the request is completely parsed, and move on to run the [RequestHandler]s.
- `Abort` will close the request, which may happen when the request is malformed. When that happens, the parser is expected to provide its own answer (error status or otherwise).

For more details on the implementation of a request parser, refer to the [Request Pipeline](https://crails-framework.github.io/website/request_pipeline/#header_3) manual.
