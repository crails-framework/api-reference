Helper to generate a create or update form for a Model from Crails MVC pattern.

```c++
<%= form_for<Article>(article, "/articles") yields %>
  <textarea name="content"></textarea>
  <input type="submit" value="send" />
<% yields-end %>
```

For a persistant model (saved in database), this will generate the following html:

```html
<form action="/articles/{article id}" method="put">
  <input type="hidden" name="csrf-token" value="{generated csrf token}" />
  <textarea name="content"></textarea>
  <input type="submit" value="send" />
</form>
```

For a non-persistent model, the following will be generated instead:

```html
<form action="/articles" method="post">
  ...
</form>
```
