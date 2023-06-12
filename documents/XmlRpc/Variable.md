The [Variable] class represents any parameter or return value in the [XML-RPC](https://en.wikipedia.org/wiki/XML-RPC) protocol, and gives you tools to easily convert them to native C++ types, or to directly interact with them.

## Native types

When you intend to send values to a remote XML-RPC service, you may instantiate this class yourself by passing one of the following native C++ type to the class constructor:

- int
- double
- bool
- std::string

When you received such a value from a remote XML-RPC service, you may then convert it to a native type using the following methods:

- as_int()
- as_double()
- as_boolean()
- as_string()

Note that a [Variable] can also be implicitely cast from any of these types.

### Dates

The `dateTime.iso8601` XML-RPC type is also supported and can be retrieved as `std::time_t` using the `as_date()` method.

You may also create such a variable from `std::time_t` using [Variable::from_date]:

```cpp
XmlRpc::Variable now = XmlRpc::Variable::from_date(
  std::chrono::system_clock::to_time_t(std::chrono::system_clock::now())
);
```

## Struct

This class can also be used to represent `<struct>` elements. You may directly interact with such structures by using the `[]` operator overload:

```cpp
XmlRpc::Variable variable = xmlrpc_client.call("method_returning_struct");
XmlRpc::Variable struct_attribute = variable["title"];

std::cout << struct_attribute.as_string() << std::endl;
```

Or, for a more rigorous approach, you may also describe the layout of the `<struct>` you expect to send or receive by overloading the [Struct] class, and instantiate such objects using a [Variable]:

```cpp
XmlRpc::Variable variable = xmlrpc_client.call("method_returning_struct");
MyCustomStruct my_struct(variable);

std::cout << my_struct.get_title() << std::endl;
```

## Arrays

Variables may also be arrays. You may create them from the [std::vector] container, or convert them to one using the [Variable::as_array] template method. Due to the limitations of the vector container, this will however only work if every variable contained in the array itself has the proper expected type. Otherwise, an exeption will be thrown. Example:

```c++
std::vector<int> values{1,2,3,4};
XmlRpc::Variable xmlrpc_array(values);

values = xmlrpc_array.as_array<int>();
```

If your array should contain values with different types, you should read or set it by directly interacting with the [Variable::array] attributes, which is itself a list of [Variable] objects. Example:

```c++
XmlRpc::Variable xmlrpc_array;
std::time_t now = std::chrono::system_clock::to_time_t(std::chrono::system_clock::now());

xmlrpc_array.name = "array"; // do not forget to set the `name` attribute to `array`
xmlrpc_array.array.push_back(1);
xmlrpc_array.array.push_back("string of characters implicitely cast to Variable");
xmlrpc_array.array.push_back(XmlRpcArray::from_date(now));
```
