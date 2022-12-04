Text-based serializer, providing a concise way to exchange messages over HTTP, with an Object-Oriented API making it easy to serialize and unserialize:

##### Serializing simple types
###### Serializing
```c++
OArchive out;
long long variableA = 64;
std::string variableB = "Hello, world!";

out & variableA & variableB;
```

###### Unserializing
```c++
IArchive in;
in.set_data(out.as_string());
long long variableA;
std::string variableB;

in & variableA & variableB;
```

###### Supported types
Types that are natively serializable include:

```
bool
char
int
long
short
unsigned char
unsgined long
unsigned int
unsigned short
std::string
double
long double
long long
unsigned long long
```

Some standard containers are also supported:

```
std::list
std::vector
std::set
std::map
```

Containers will work with any serializable type, including custom ones.

###### Pointers

Pointers and smart pointers are supported as well, although there are some specifics you need to know before serializing and unserializing data using pointers.

Archives will only allocate pointers using the [std::shared_ptr] or [std::unique_ptr] types. Other pointers types, you must allocate on your own. If a null pointer is used in an unserializing process, an exception will be thrown.

Serializing null pointers is tolerated, but it is not a great practice: unserializing the data won't result in a null pointer, but rather in an uninitialized value.

Here are some valid examples:

```c++
OArchive out;
IArchive in;

// Valid use of pointers
shared_ptr<string> out_value = make_shared<string>("Hello world");
shared_ptr<string> in_value;

out & out_value;
in.set_data(out.as_string());
in & in_value;

// or:
string out_value("Hello world");
string* in_value = new string;

out & (&out_value);
in.set_data(out.as_string());
in & in_value;
```

And here are examples of what not to do:

```c++
OArchive out;
IArchive in;

// Using unallocated pointers
string out_value("Hello world"),
string* in_value;

out & (&out_value);
in.set_data(out.as_string());
in & in_value; // Segmentation fault

// Unserializing null pointers
int* out_value = nullptr;
int* in_value = new int;

out & out_value;
in.set_data(out.as_string());
in & in_value; // in_value remains uninitialized
```

##### Serializing custom types
You may also implement serializers for your own types, making it very straightforward to include or extract such types from an `Archive`. The simplest way to do so is by using the `ARCHIVE_SERIALIZER` macro:

```c++
#include <libtext-archive/archivable.hpp>

struct MyType : public Archivable // <- add the Archivable component
{
  long long variableA;
  std::string variableB;

  ARCHIVE_SERIALIZER(variableA & variableB)
};
```

Sometimes, you may need to implement more complex custom serializers. In these cases, you may replace the `ARCHIVE_SERIALIZER` with implementations for the two `serialize` virtual methods from [Archivable]:

```c++
struct MyType : public Archivable
{
  long long variableA;
  std::string variableB;

  void serialize(OArchive& archive) const override
  {
    bool hasVariableB = variableB == "undefined";

    archive & variableA & hasVariableB;
    if (hasVariableB)
      archive & true & variableB;
  }

  void serialize(IArchive& archive) override
  {
    bool hasVariableB;

    archive & variableA & hasVariableB;
    if (hasVariableB)
      archive & variableB;
    else
      variableB = "undefined";
  }
};
```
