Represents a connection with an HTTP client. When a query is received, the connection instantiates a [Context] and let it run the query through the [Request Pipeline](https://crails-framework.github.io/website/request_pipeline).

Unlike the [Context] object, the [Connection] object may outlive a single transaction, if the client used the [Connection: Keep-Alive](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Connection) header.
