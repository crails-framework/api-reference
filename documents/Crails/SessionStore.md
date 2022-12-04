Interface for `SessionStore` backends, providing session data based on cookies - or anything else depending on the implementation.

A `SessionStore` implementation must implement three methods:

- `load` takes an [HttpRequest] as parameter, allowing the implementation to inspect the request and extract data related to the current session,
- `finalize` takes a [BuildingResponse] as parameter, allowing the implementation to modify the underlying [HttpResponse] and provide its own HTTP headers and such,
- `to_data` which returns a [Data] object which can then be used to access or store variables into the session.
