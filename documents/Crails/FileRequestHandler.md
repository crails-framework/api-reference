Implementation of [RequestHandler] that tries to respond to a query by looking up files in the application's _public_ directory (matching a [Server]'s `public_path` attribute).

`RequestFileHandler` supports the following HTTP headers:

- [Accept-Encoding](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept-Encoding) header for the `brotli` and `gzip` formats, and will serve the compressed version of a file if it is available. Compressed files should share the same name as their uncompressed version, with the suffix `gz` for gzip or `br` for brotli.
- [If-Modified-Since](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-Modified-Since), which will respond with [304 Not Modified](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/304) if the file hasn't been modified since the last visit.
- [Range](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Range), which allows clients to request for specific chunks of a file, rather than the entire file.

If caching is enabled, requested files will also be stored in memory to speed up further request. Caching files that are frequently requested by clients will significantly improve your response time. But if you use it to serve big files, it may also have a significat memory footprint.

You may toggle caching by calling the `set_cache_enabled` method. Caching is enabled by default.
