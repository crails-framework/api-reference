Adds or update a named cron job with the given name.

The following call:

```c++
crontab.set_task("mytask", "0 * * * *", "rm -rf /tmp/*");
```

Would generate this cron job:

```shell
0 * * * * rm -rf /tmp/* #name=mytask
```
