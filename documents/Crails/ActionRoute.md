Route handler for controllers based on the [ActionController].

Usage:

```c++
struct MyController : public Crails::ActionController
{
  MyController(Crails::Context& context) : Crails::ActionController(context) {}

  void action_method()
  {
    render(TEXT, params["param"]);
  }
};

void Router::initialize()
{
  using namespace Crails;
  using namespace std;

  match("GET", "/route/:param", [](Context& context, function<void()> callback)
  {
    ActionRoute<MyController>::trigger(context, &MyController::action_method, callback);
  });

  // Alternatively:
  match("GET", "/alt-route/:param",
    bind(
      ActionRoute<MyController>::trigger,
      placeholders::_1,
      &MyController::action_method,
      placeholders::_2
    )
  );
}
```

The `ActionRoute` header also defines the `match_action` macro to facilitate route declaration:

```c++
void Router::initialize()
{
  match_action("GET", "/route/:param", MyController, action_method);
}
```
