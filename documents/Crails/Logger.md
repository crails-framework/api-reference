Handles logging for Crails applications. Each log is provided with a `log_level`. The logger is thread-safe, and can aggregate the logs from several threads into a single [std::ostream].

Usage:

```c++
#include <crails/logger.hpp>

using namespace Crails;

int main()
{
  logger << Logger::Info << "Logging text" << Logger::endl;
  return 0;
}
```

Use the `Logger::Info`, `Logger::Debug`, `Logger::Warning`, `Logger::Error` symbols to change the `log_level` in your current thread.

Afterwards, anything sent to the `operator<<` will be written in a buffer. Sending `Logger::endl` or switching `log_level` will flush the buffer and print its content on the output stream (by default, stdout or stderr).

##### Performance

Logging can take a toll on performance, and there are no good ways to save from it. The best way to improve performance is simply to avoid useless logging, which you can do in two different ways.

###### Log levels

The logger only displays log that have a lower level than the global `log_level` that was set for the logger.

In order, the levels are:
```
Debug
Info
Warning
Error
```

You can set the log level by changing the `Crails::Logger::log_level` global variable, typically present in the `config/logger.cpp` file.

###### Lambdas

When using log levels to filter logs, you may execute useless code. For instance, if you want to log a [Data] object using the JSON format, you would do something like this:

```c++
logger << Logger::Info << data.to_json() << Logger::endl;
```

In this example, assuming the `log_level` is set to `Error`, nothing will print on the screen... however, `data.to_json()` will be called, pointlessly taking CPU time.

You can fix that by using lambdas instead:

```c++
logger << Logger::Info << ([]() { return data.to_json(); }) << Logger::endl;
```

In this alternative version, `data.to_json()` will only be called when the log level isn't filtered out, saving precious time for production environments which may ignore `Info` logs.
