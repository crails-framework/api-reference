The struct class helps you interact, send and receive `<struct>` elements from the XML-RPC protocol.

[Struct] can be implicitely casted to [Variable], allowing you to pass them as parameters to XML-RPC methods. You may also create a [Struct] from a [Variable] by passing the variable as a parameter to the constructor.

You can define your own custom structs using a series of macro to define its XML-RPC attributes, as demonstrated in the following example:

```cpp
struct MyCustomStruct : public XmlRpc::Struct
{
  MyCustomStruct() {}
  MyCustonStruct(const XmlRpc::Variable& variable) : XmlRpc::Struct(variable) {}

  XmlRpc_string_property(title)
  XmlRpc_string_property(description)
  XmlRpc_date_property(updated_at)
  XmlRpc_string_array_property(usernames)
};
```

You can then set these properties using setters as such:

```cpp
MyCustomStruct my_struct;
std::vector<std::string> usernames{"Roger","Hanin"};

my_struct.set_title("Event name");
my_struct.set_description("Some boring kind of event");
my_struct.set_date(std::chrono::system_clock::to_time_t(std::chrono::system_clock::now()));
my_struct.set_usernames(usernames);
```

Or access them using getters as such:

```cpp
if (my_struct.is_title_nil())
  cout << "No title" << endl;
else
  cout << my_struct.get_title() << endl;
```

The macros available to define your attributes are:

- XmlRpc_string_property
- XmlRpc_int_property
- XmlRpc_double_property
- XmlRpc_date_property
- XmlRpc_bool_property
- XmlRpc_string_array_property
- XmlRpc_int_array_property
- XmlRpc_double_array_property
