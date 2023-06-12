Returns a value from [SharedVars] as a given type, or throw an exception.

Parameters:
- [SharedVars] object,
- Name of the variable to fetch
- Default value (optional)

Throws [boost_ext::out_of_range] if the variable does not exist.

Throws [boost::bad_any_cast] exception if the variable exists, but the requested type didn't match the variable type.

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

  Crails::cast<const char*>(vars, "hello-world"); // returns a pointer to "Hello world"

  Crails::cast<std::string>(vars, "as-string"); // returns a copy of the "as-string" string

  Crails::cast<int>(vars, "as-int"); // returns 12

  Crails::cast<int>(vars, "other-number", 42); // returns 42

  Crails::cast<std::string>(vars, "undefined"); // throws boost_ext::out_of_range

  Crails::cast<int>(vars, "hello-world", ""); // throw boost::bad_any_cast

  return 0;
```

The cast function is usually very strict about types and qualifiers, but it can be more tolerant with string types.
For instance, the following casts are all valid:

- From `const char*`, `std::string`, `const std::string` and `std::string_view` to either `const std::string` or `std::string`.
- From `const char*` to `std::string_view`
- From `std::string_view` to `const char*`

Which means the following calls would return valid strings as intended:

```c++
Crails::SharedVars vars{
  {"hello-world", "Hello world"},
  {"as-string", std::string("Hello world")},
  {"as-string_view", std::string_view("Hello world")}
};

Crails::cast<const std::string>(vars, "hello-world");
Crails::cast<std::string>(vars, "hello-world");
Crails::cast<std::string_view>(vars, "hello-world");
Crails::cast<const char*>(vars, "as-string-view");
Crails::cast<std::string>(vars, "as-string-view");
```

