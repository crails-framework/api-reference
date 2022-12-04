Template implementation for the [Singleton design pattern](https://en.wikipedia.org/wiki/Singleton_pattern). It can be used on its own,
or with the [SingletonInstantiator].

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
  MyClass::singleton::initialize("string param", 12.f);

  MyClass::singleton::get()->method();

  MyClass::singleton::finalize();
  return 0;
}
```
