Utility class to load, edit and save [crontab](https://fr.wikipedia.org/wiki/Cron) files.

Cron jobs managed by this class are typically affected to a `name` variable, allowing you to quickly fetch, update or remove them with the `get_task`, `set_task` and `remove_task` methods.

You may also read and write environment variables which were setup in the crontab using the `get_variable`, `set_variable` and `remove_variable` methods.

Cron jobs created with other software will be unnamed, but can still be accessed by iterating through jobs using Crontab's iterators, with a for loop:

```c++
// Overwriting the content of all jobs:
Crails::Crontab crontab;

crontab.load();
for (Crails::Crontab::Task& job : crontab)
{
    job.name = "";
    job.schedule = "* * * * *";
    job.command = "rm -rf /tmp";
}
```

Or directly using iterators:

```c++
// Removing all unnamed jobs:
Crails::Crontab crontab;
Crails::Crontab::iterator it;

crontab.load();
it = crontab.begin();
while (it != crontab.end())
{
  if (it->name == "")
    it = crontab.erase(it);
  else
    it++;
}
```
