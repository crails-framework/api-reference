Controller component providing the [DataTree] `flash` protected property for controllers.

The `flash` property can be used to communicate data from one http request to the other using cookies. Anything you place in the flash [DataTree] will be exposed to the very next action and then cleared out. This is a great way of doing notices and alerts, such as a create action that sets `flash["notice"] = "Post successfully created"` before redirecting to a display action that can then expose the flash to its template. Actually, that exposure is automatically done.

```c++
class PostController : public Crails::FlashController
{
public:
  PostController(Crails::Context& c) : FlashController(c) {}

  void create()
  {
    // save post
    flash["notice"] = "Post successfully created";
    redirect_to("/posts/" + std::to_string(post.get_id()));
  }

  void show()
  {
    // doesn't need to assign the flash notice to the controller's shared variables, that's done automatically
    render("posts/show");
  }
};
```
Then, in `app/views/posts/show.html`:

```html
DataTree& @flash;
// END LINKING

<% if (flash["notice"].exists()) do -%>
  <div class="notice"><%= flash["notice"].as<std::string>() %></div>
<% end -%>
```

This example places a string in the flash. And of course, you can put as many as you like at a time too. If you want to pass non-primitive types, you will have to handle that in your application.

Just remember: They’ll be gone by the time the next action has been performed.
