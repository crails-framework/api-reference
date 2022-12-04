Runs the `callback` parameter within a `try/catch` block that will catch every kind of exception. When that happens, it will provide an HTTP response through the `context` parameter.

Note that the `mutex` from the [Context] object will be locked until the callback returns.

Custom behaviours can be defined by adding exception catchers with `add_exception_catcher`.
