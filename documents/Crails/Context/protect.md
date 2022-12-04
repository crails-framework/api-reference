Protects the parameter callback against thrown exceptions using [ExceptionCatcher].

This method also locks the Context's `mutex` field, using [std::lock_guard].
