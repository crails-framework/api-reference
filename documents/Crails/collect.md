Return a subset of an iterable list of objects or object pointers.

Parameters:
- A reference to a list of objects
- A method pointer to apply on each object in the list. The method should be marked as `const`, and should return `bool`.

The variadic arguments for this function templates, if there are any, will be used as arguments sent to the method pointer.

Examples:

```c++
#include <crails/utils/arrays.hpp>
#include <memory>

struct Item
{
  Item(int a) : value(a) {}
  int value;
  bool collectible() const { return value % 2 == 0; }
  bool still_collectible(int i) const { return value % i == 0; }
};

int main()
{
  using namespace std;
  using namespace Crails;

  vector<Item> listA = {
    Item{1}, Item{2}, Item{3}, Item{4}, Item{5}
  };

  vector<Item> listB = collect(listA, &Item::collectible); // returns {Item{2}, Item{4}}

  vector<Item> listC = collect(listA, &Item::still_collectible, 3); // returns {Item{3}}

  vector<shared_ptr<Item>> listD = {
    make_shared<Item>(1), make_shared<Item>(2)
  };

  vector<Item> listE = collect(listD, &Item::collectible); // returns {Item{2}}

  return 0;
}
```
