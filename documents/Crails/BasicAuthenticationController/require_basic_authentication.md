Use this method to force the client's browser to send an `Authentication` user. The expected client's credentials (user and password) are specified in the two parameters of the function.

Instead of directly specyfing a user and a password, you can also send a callback in the form of [std::function<bool(const std::string&,const std::string&)>]: the callback receive the user and password sent by the client, and it is expected to return `true` or `false` depending on whether the authentication is successful or not.

In case of failure, the `require_basic_authentication` method sets directly sends a response to the client (using either the _Unauthorized_ or _Unprocessable entity_ status), meaning you do not have to set a response status yourself. You may still provide a body for the response.
