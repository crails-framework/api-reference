Splits a string in several pieces delimited by a separator. Parameters are:

- *value* to split, typically using [std::string]
- *separator* given as a `char`
- *repetitions* a boolean value specifying whether the function should generate empty fragments when the value contains consecutive separators. Set to `true` to include empty fragments. Defaults to `false`

Examples:
```c++
#include <iostream>
#include <string>
#include <vector>
#include <crails/utils/split.hpp>

int main()
{
  using namespace std;
  using namespace Crails;

  // {"a", "few", "words"}
  list<string> parts = split("a few words", ' ');

  // {"hello", "", "", "world", "!"}
  list<string> parts = split("hello   world !");

  // returning std::vector instead:
  vector<string> parts = split<string, vector<string>>("hello world !");

  return 0;
}
```
