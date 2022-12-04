Concatenates a iterable list as a single string. The parameters are :

- iterator from
- iterator to
- separator (defaults to a single space)

Examples:
```c++
#include <crails/utils/join.hpp>
#include <vector>
#include <iostream>

int main()
{
  using namespace std;
  using namespace Crails;
  vector<string> parts{"Hello", "world", "!");

  cout << join(parts.begin(), parts.end()) << endl; // prints "Hello world !"

  cout << join(parts.begin(), parts.end(), '-') << endl; // prints "Hello-world-!"

  cout << join(parts.begin(), parts.end(), "%20") << endl; // prints "Hello%20world%20!"

  cout << join(parts.begin(), parts.end(), "") << endl; // prints "Helloworld!"

  return 0;
}
```
