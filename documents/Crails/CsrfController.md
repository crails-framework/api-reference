Controller component providing tools to implement protection against [Cross-Site Request Forgery](https://fr.wikipedia.org/wiki/Cross-site_request_forgery).
When enabled, it will create a variable into the `session` [Data] object provided by the controller.

When CSRF security is enabled, any HTTP requests using the `POST`, `PUT`, `PATCH` or `DELETE` verb *must* include the CSRF token from the last request they made as a _parameter_, or their request will be dismissed.
What a _parameter_ can be depends on your [request parsers](https://crails-framework.github.io/website/request_pipeline/): URL parameters, variables in a `application/x-www-urlencoded` body, etc.

You may read the CSRF token in the following fashion:

```c++
void MyController::show()
{
  const std::string csrf_token = session["csrf-token"].as<std::string>();
}
```

When CSRF security is not relevant, you may disable it by overloading `must_protect_from_forgery`:

```c++
class MyController : public Crails::Controller
{
public:
  MyController(Crails::Context& context) : Crails::Controller(context) {}

  bool must_protect_from_forgery() const override { return false; } // disable CSRF protection
};
```
