Takes a list of pointers as parameter, and returns a list of the same type cleared out of any null pointers.

Examples:
```c++
#include <crails/utils/arrays.hpp>
#include <vector>
#include <string>
#include <memory>

int main()
{
  using namespace std;
  using namespace Crails;

  // Safely deletes a list of raw pointers:
  vector<string*> a = {
    "Hello", nullptr, "world"
  };

  for (string* str : exclude_nullptr(a))
    delete str;

  // Safely prints a list of smart pointers:
  vector<shared_ptr<string>> b = {
    make_shared<string>("Hello"),
    nullptr,
    make_shared<string>("world")
  };

  for (const auto& str : exclude_nullptr(b))
    cout << str << endl;

  return 0;
}
```
