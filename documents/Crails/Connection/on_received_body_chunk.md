Designed to be used by implementations of [RequestParser], this method allows you to set a callback that will be called once a chunk of the current request body has been received.

There are some limitations to this way of retrieving a request body:

- Only the first [RequestParser] requiring a body may receive the request body. Typically, a [RequestParser] receiving a request body should be the last parser from the pipeline to run on a request. This is implemented by having such a parser calling back the context with [RequestParser::Stop].

- If this method is not immediately called after a [Context] is created, the request's body will be (at least partially) ignored. This means that no asynchronous [RequestParser] should run before the one that will receive the body. 
