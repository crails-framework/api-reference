Implements [Crails::Renderer] and [Crails::Template] for RSS documents, using XML templates generated using the [ecpp](https://github.com/crails-framework/ecpp) generator:

```xml
#include "model.hpp"
const std::vector<Article>& @article_list;
// END LINKING
<%= xml_header("UTF-8") %>
<rss version="2.0" xmlns:atom="http://www.w3.org/2005/Atom">
  <channel>
    <%= title("My RSS feed") %>
    <%= link("http://localhost:3001/rss") %>

    <% for (const auto& article : article_list) do -%>
      <item>
        <%= guid(article.get_id()) %>
        <%= title(article.get_title()) %>
        <%= link(article.get_url()) %>
        <%= description() yields %>
          <img src="<%= article.get_thumbnail_url() %>" />
          <p><%= article.get_description() %></p>
        <%= yields-end %>
      </item>
    <% end -%>
  </channel>
</rss>
```

The `libcrails-rss-views` package can be added to a Crails project by using the following command:

```sh
crails templates formats --add rss
```

A file located at `app/views/articles/index.rss` will then be rendered like this:

```c++
void render(Crails::RenderTarget& target, const std::vector<Article>& articles)
{
  Crails::SharedVars vars;

  vars["article_list"] = &articles;
  Renderer::render("articles/index", "application/rss+xml", target, vars);
}
```

Or from a Crails controller:

```c++
void MyController::index(const std::vector<Article>& articles)
{
  vars["article_list"] = &articles;
  render("articles/index");
}
```
