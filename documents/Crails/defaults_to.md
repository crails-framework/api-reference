Returns a value from [SharedVars], or fallbacks to a default value.

Parameters:
- [SharedVars] object,
- Name of the variable to fetch
- Default value to use when the variable does not exist

This function will throw [boost::bad_any_cast] exception if the variable exists, but the requested type didn't match the variable type.

Examples:

```c++
#include <crails/any_cast.hpp>
#include <crails/shared_vars.hpp>
#include <string>

int main()
{
  int number = 12;
  Crails::SharedVars vars{
    {"hello-world", "Hello world"},
    {"as-string", std::string("Hello world")},
    {"as-int", number}
  };

  Crails::defaults_to<const char*>(vars, "hello-world", ""); // returns a pointer to "Hello world"

  Crails::defaults_to<std::string>(vars, "as-string", ""); // returns a copy of the "as-string" string

  Crails::defaults_to<std::string>(vars, "undefined", "defaults"); // returns "defaults" as a string

  Crails::defaults_to<int>(vars, "as-string", 21); // throw boost::bad_any_cast

  return 0;
}
```
