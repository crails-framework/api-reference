Initializes and maintains a connection to remote databases represented by the [Database] interface, in a multi-threading friendly fashion. Instances of [Database] are created for each thread as soon as they are required, and are maintained until the thread shuts down.

This design improves your application's response time by saving the time that would otherwise be spent on repeatedly opening and closing connections to your databases.

`Databases` is implementation-agnostic, and you can use it to manage your connection with several types of databases at the same time, such as MySQL, PostgreSQL, Sqlite, Redis, MongoDB, etc.

#### Pre-configured databases

Available databases are configured by defining the static [Databases::Settings] `settings` attribute. Configurations are mapped by [Crails::Environment]:

```c++
const Crails::Databases::Settings = {
  {
    Crails::Development, {
      {
        "my_database", { // <-- Database unique identifier
          {"type", "sqlite"},
          {"name", "application-db"}
        }
      },
      {
        "sync_database, {
          {"type", "redis"}
        }
      }
      // ...
    }
  }
};
```

Database handles are then aquired using the `CRAILS_DATABASE` macro:

```
Crails::Odb::Database& sql_database = CRAILS_DATABASE(Crails::Odb,  "my_database");
Crails::Redis::Database& redis_database = CRAILS_DATABASE(Crails::Redis, "sync_database);
```

#### Dynamic database creation

Some application may actually want to dynamically configure databases at runtime. This is also possible, using the `CRAILS_DATABASE_FROM_SETTINGS` macros:

```c++
Crails::Odb::Database& sql_database = CRAILS_DATABASE_FROM_SETTINGS(Crails::Odb, "unique_identifier", {
  {"type", "pgsql"},
  {"host", "localhost"},
  {"name", "mydatabase"}
});
```

When using this macro, the database manager will first check for an existing database matching the `"unique_identifier"` used as parameter. If it exists, the existing database handle will be returned. If it doesn't exist, a new database handle will be created with the settings used as parameters.

Here are some important facts to take into accounts when creating databases dynamically:
- Database handles are only garbage collected when the thread that created them are destroyed
- Threads from the [Server] thread-pool are _never_ destroyed

You may compensate these flaws by using the `cleanup_database` method to clear away databases that were created dynamically.
