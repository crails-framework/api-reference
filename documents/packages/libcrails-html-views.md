Implements [Crails::Renderer] and [Crails::Template] for HTML documents, including several helpers for building form
HTML templates can be generated using the [ecpp](https://github.com/crails-framework/ecpp) generator:

```html
#include "model.hpp"
Article& @article;
// END LINKING
<h1><%= article.get_title() %></h1>
<%= tag("p", {{"class",article.get_css_class()}}) do %>
  <%= html_escape(article.get_content()) %>
<% end %>
</p>
```

The `libcrails-html-views` package can be added to a Crails project by using the following command:

```sh
crails templates formats --add html
```

This will add `libcrails-html-views` to your `CMakeLists.txt`, and register [Crails::HtmlRenderer] in the `config/renderers.cpp` file.

Once the package has been added to your project, the `crails build` command will use [ecpp](https://github.com/crails-framework/ecpp) and generate templates from all the html files found in the various `views` folder of your application.

For instance, a file located at `app/views/resource/show.html` could then be rendered like this:

```c++
void render(Crails::RenderTarget& target, Article& article)
{
  Crails::SharedVars vars;

  vars["article"] = &article;
  Renderer::render("resources/show", "text/html", target, vars);
}
```

Alternatively, in a class implementing [Crails::RenderController] or [Crails::Controller]
from [libcrails-controllers](#/packages/libcrails-controllers), you should render your template
using the `RenderController::render` method:

```c++
void MyController::show(Article& article)
{
  Crails::SharedVars properties;

  vars["article"] = &article;
  render("resources/show");
}
```
