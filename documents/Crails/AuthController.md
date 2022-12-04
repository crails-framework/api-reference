Controller component for access-protected content, where the access is granted to users that have an opened [Session]. The `USER` model should implement the [AuthenticableModel] component.

A [Session] object is provided using the `user_session` protected attribute.

Usage example:

```c++
struct MyUser : public AuthenticableModel
{
  std::string username;
};

struct MyController : public Crails::AuthController<MyUser, Crails::Odb::Controller>
{
  MyController(Crails::Context& context) : Crails::AuthController<MyUser, Crails::Controller>(context) {}

  void action_method()
  {
    if (initialize_current_user())
      render(TEXT, "Authenticated user: " + user_session.get_current_user()->username);
  }
};
```
