Helper method generating an HTML link in a concise manner:

```c++
<%= link("http://duckduckgo.com", "DuckDuckGo") %>
<!-- Renders: <a href="http://duckduckgo.com">DuckDuckGo</a> -->
```

Extra HTML attributes can be provided as well:

```c++
<%= link("https://duckduckgo.com", "DuckDuckGo", {{"class","btn"}}) %>
```

The `yields/yields-end` keywords are also supported:

```html
<%= link("https://duckduckgo.com") yields %>
  <i class="duck-icon"></i> DuckDuckGo
<% yields-end %>
```
