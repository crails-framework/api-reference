Determines whether the authenticated user should be required during controller initialization or not. If `true` is returned, and the client request is made without an opened session, the controller initializer will call the `on_user_not_authenticated` and abort the request - the action method will not be called.

Returns `false` by default. You may override this method to change this behaviour.
