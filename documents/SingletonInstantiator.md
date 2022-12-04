[Scope guard](https://stackoverflow.com/questions/31365013/what-is-scopeguard-in-c) for singleton classes using the [Singleton] template.

Example:

```c++
// header
#pragma once
#include <crails/utils/singleton.hpp>

class MyClass
{
  SINGLETON(MyClass)
  MyClass(const std::string& param1, float param2); // private constructor

public:
  void method();
};

// usage
int main()
{
  SingletonInstantiator<MyClass, const std::string&, float> my_class("string param", 12.f);

  MyClass::singleton::get()->method();
  // or:
  my_class->method();

  return 0;
}
```
