Reset the connection to a single database that was started within the single thread. This method can be useful to clear up dynamically created databases:

```c++
Crails::Odb::Database& sql_database = CRAILS_DATABASE_FROM_SETTINGS(Crails::Odb, "new_db", {
  {"type", "pgsql"},
  {"name", "mydatabase"}
});

Crails::databases.cleanup_database(sql_database);
```

If the database handle specified as parameter wasn't created in the current thread, will throw [boost_ext::out_of_range].
