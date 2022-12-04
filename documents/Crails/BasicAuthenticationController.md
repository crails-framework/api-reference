The basic authentication controller brings [HTTP Basic Authentication](https://developer.mozilla.org/en-US/docs/Web/HTTP/Authentication) to your controllers. It is typically used through the [Crails::Controller] class, which inherits this class.

Use the protected `require_basic_authentication` in the controller actions you wish to protect against unauthenticated users.
