Stores a collection of file cached in memory, designed to be served by the [BuiltinAssetsHandler] request handler. Every asset in this collection should be compressed using the same method (eg: gzip, brotli). Assets can also be served uncompressed,

# crails-builtin-assets

The Crails Framework comes with a tool to generate implementations of `BuiltinAssets` from assets found in your filesystem. The following command could be used to generate a `MyBuiltinAssets` class, able to serve all the files found under the `assets/stylesheets` folder, compressed using gzip.

```sh
crails-builtin-assets \
  --inputs "assets/stylesheets" \
  --output "lib/my_builtin_assets" \
  --classname "MyBuiltinAssets" \
  --compression "gzip" \
  --uri-root "/assets/"
```

This command will generate a header called `lib/my_builtin_assets.hpp` which will define the `MyBuiltinAssets` class. You would then be able to feed this asset library into your request pipe, such as:

```c++
#include <crails/request_handlers/builtin_assets.hpp>
#include "lib/my_builtin_assets.hpp"
#include "server.hpp"

const MyBuiltinAssets my_builtin_assets;

void ApplicationServer::initialize_request_pipe()
{
  add_request_handler(new Crails::BuiltinAssetsHandler(my_builtin_assets));
}
```

The final path for each of your assets is the concatenation of the `--uri-root` option with each file's path, relative to the input folder they were collected from. For instance, in this example, a file located at `assets/stylesheets/application.css` would be served when receiving a request for `/assets/application.css`.

Note that global constants are defined for each of the file pathes within a `BuiltinAssets` collection. For instance, if we wanted to include our `application.css` stylesheet into a layout view, we could define the `href` attribute of the `link` tag by using the `MyBuiltinAssets::application_css` constant:

```html
#include "lib/my_builtin_assets.hpp"
// END LINKING
<html>
  <head>
    <%= tag("link", {{"rel","stylesheet"}, {"href", MyBuiltinAssets::application_css}}) %>
  </head>
  <body>
    <% if (yield != nullptr) do %>
      <%= yield %>
    <% end -%>
  </body>
</html>
```
