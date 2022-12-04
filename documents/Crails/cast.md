Returns a value from [SharedVars] as a given type, or throw an exception.

Parameters:
- [SharedVars] object,
- Name of the variable to fetch

Throws [boost_ext::out_of_range] if the variable does not exist.

Throws [boost_ext::bad_any_cast] exception if the variable exists, but the requested type didn't match the variable type.

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

  Crails::cast<const char*>(vars, "hello-world", ""); // returns a pointer to "Hello world"

  Crails::cast<std::string>(vars, "as-string", ""); // returns a copy of the "as-string" string

  Crails::cast<std::string>(vars, "undefined"); // throws boost_ext::out_of_range 

  Crails::defaults_to<std::string>(vars, "hello-world", ""); // throw boost_ext::bad_any_cast

  return 0;
```
