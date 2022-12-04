Generates an HTML tag using the type specified as parameter:

```html
<%= tag("div") %> <!-- Renders: <div></div> -->
```

Optionally, the method can take a list of HTML attributes:

```html
<%= tag("div", {{"class","card"},{"data-model-id","15"}}) %>
<!-- Renders: <div class="card" data-model-id="15"></div> -->
```

You may also provide a [Yieldable] callback to render the element's contents.
When writing `ecpp` templates, this should be done using the `yields/yiends-end` keywords:

```html
<%= tag("div", {{"class","card"}}) do %>
  <h1>Title</h1>
  <p>Content</p>
<% yields-end %>
```
