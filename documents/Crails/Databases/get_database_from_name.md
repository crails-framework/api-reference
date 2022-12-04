Returns a pointer to a [Database] handle, based on its unique identifier, and if it has already been initialized. If the specified database hasn't been initialized yet, returns nullptr.

Databases can be initialized using the `CRAILS_DATABASE` and `CRAILS_DATABASE_FROM_SETTINGS` macro, or the `get_database` method templates.
