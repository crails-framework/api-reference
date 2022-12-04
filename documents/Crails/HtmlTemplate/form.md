Helper for generating forms. Supports the CSRF protection system from [CsrfController].

```html
<%= form({{"action","/search"},{"method","post"}}) yields %>
  <input type="text" name="query" />
<% yields-end %>
```

Which results to:
```html
<form action="search" method="post">
  <input type="hidden" name="csrf-token" value="{generated value}" />
  <input type="text" name="query" />
</form>
```
