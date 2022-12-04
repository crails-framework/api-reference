Parses a database URL and provides an easy access to each individual fragment through the `type`, `hostname`, `username`, `password` and `database_name` attributes.

Example:
```c++
#include <crails/database_url.hpp>
#include <iostream>

using namespace std;
using namespace Crails;

int main()
{
  DatabaseUrl url("pgsql://user:password@localhost:1234/dbname");

  cout << url.type // pgsql
       << url.username // user
       << url.password // password
       << url.hostname // localhost
       << url.port // 1234
       << url.database_name // dbname
       << endl;
  return 0;
}
```

Components are not all mandatory. The bare minimum would include a scheme, hostname and port:

```c++
DatabaseUrl("redis://localhost:4321");
```

When the URL is malformed, throws [std::exception].
