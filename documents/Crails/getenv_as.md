Returns an environment variable as the specified type.

Parameters:

- variable name
- default value

Example:

```
#include <crails/getenv.hpp>
#include <iostream>

int main()
{
  using namespace std;
  using namespace Crails;

  cout << getenv_as<int>("UNDEFINED_VARIABLE_NAME", 21) << endl; // prints "21"
  cout << getenv_as<string>("USER", "") << endl; // prints the username from your environment
  return 0;
}
```
