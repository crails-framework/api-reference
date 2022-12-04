Adds a new type of exception to watch for.

The template parameter must match the type of exception you wish to catch.

For the second parameter:

- You may use a [std::string] to set a name for the exception, and have it handled by the default exception handler: this will provide a simple 500 response, and if your application is not in Production mode, will render an HTML view with more details about the exception (such as backtraces, if available).

- You may also use [std::function] to define your own exception handler. The handler will receive a [Context] object, which mutex will already have been locked, making it thread-safe for you to interact with. You may then provide your own HTTP response through the Context object.
