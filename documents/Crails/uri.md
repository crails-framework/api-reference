Builds an [URI](https://developer.mozilla.org/fr/docs/Glossary/URI) from a list of arguments. Each parameter will be URI-encoded and appended as a fragment of the newly built URI:

```
#include <crails/url.hpp>
#include <iostream>

int main()
{
  using namespace std;
  cout << Crails::uri("resource", 51) << endl; // prints "/resources/51"
  cout << Crails::uri("&ncod&d content?") << endl; // prints "/%26ncod%26d%20content%3F"
  return 0;
}
```
