The [XmlRpc::Client] class allows you to call a remote function using the [XML-RPC](https://en.wikipedia.org/wiki/XML-RPC) protocol using C++ semantics.

Here are some examples of uses:

```cpp
int main()
{
  XmlRpc::Client service("https://localhost:3001/xmlrpc");

  {
    // Simple call with no parameters
    std::string response = service.call("function_name");
    std::cout << "function_name responded with " << response << std::endl;
  }

  {
    // Call with parameters using native C++ types
    int response = service.call("sum", 12, 24);
    std::cout << "sum responded with " << response << std::endl;
  }

  {
    // Call returning XmlRpc types
    XmlRpc::Variable response = service.call("current_date");
    std::time_t timestamp = response.as_date();
    std::cout << "current timestamp is: " << timestamp << std::endl;
  }

  {
    // Call with XmlRpc types as parameters
    std::time_t now = std::chrono::system_clock::to_time_t(std::chrono::system_clock::now());
    bool response = service.call("is_before_due_date", XmlRpc::Variable::from_date(now));
    std::cout << "is_before_due_date respondeed with: " << response << std::endl;
  }

  return 0;
}
```

XML-RPC arrays, structs, and various types are supported through the [XmlRpc::Variable] and [XmlRpc::Struct] classes, and can be used both as parameters and return values.

If and when an XML-RPC _fault_ occurs, an exception will be thrown using the type [XmlRpc::Fault].
