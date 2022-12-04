Attempts to initialize the [Session] stored in the `user_session` attribute. If the client request didn't provide a data for an on-going session, the method returns `false` and calls `on_user_authenticated`.

If the method returns `true`, you can safely call `user_session.get_current_user()` and expect it to return a valid pointer to one of your `USER` model.
