Defines the behaviour to apply when a user is required and wasn't found. You may call this method on your own, and may also be called by `initialize_current_user`.

By defaults, responds with a header-only answer with a `403 Forbidden` status. You may override this method to upgrade this behaviour.
