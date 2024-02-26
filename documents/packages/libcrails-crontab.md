A simple utility library for programmatically managing [Cron](https://fr.wikipedia.org/wiki/Cron) jobs.

#### Examples
##### Scheduling a job
```c++
#include <crails/crontab.hpp>

int main()
{
  Crails::Crontab crontab;

  crontab.load();
  crontab.set_variable("TMP_DIRECTORY", "/tmp");
  crontab.set_task("wipe-tmp-directory", "0 * * * *", "rm -rf $TMP_DIRECTORY/*");
  return crontab.save() ? 0 : 1;
}
```
