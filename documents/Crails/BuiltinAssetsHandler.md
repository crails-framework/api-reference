Implementation of [RequestHandler] that serves assets from a [BuiltinAssets] object. It is meant to serve a role similar to [FileRequestHandler], but for handling small static files in the most efficient fashion possible.

The following theorical example shows how to manually create a [BuiltinAssets] object containing a simple `index.html` file, and use [BuiltinAssetsHandler] to serve it when receiving a `GET /scope/index.html` request:

```c++
#include <crails/request_handlers/builtin_assets.hpp>
#include "server.hpp"

Crails::BuiltinAssets assets("/scope", "");

const std::string_view index_html = "<html><head><title>Hi</title></head><body>Hello World!</body></html>";

void ApplicationServer::initialize_request_pipe()
{
  assets.add("index.html", index_html.data(), index_html.length()); 
  add_request_handler(new Crails::BuiltinAssetsHandler(assets));
}
```

Note that while [BuiltinAssets] can be manually created, as shown in the previous example, they are designed to be generated using the `crails-builtin-assets` command from the [crails-assets](https://github.com/crails-framework/crails-assets) tool. See the [BuiltinAssets] documentation for more details.

A BuiltinAssetsHandler can typically be built into a shared library, allowing some assets to be permanently loaded into memory, and shared between several Crails application, making them very quickly accessible with the smallest possible footprint.
