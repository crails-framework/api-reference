RouterBase is a template allowing you to quickly build routing systems for your application.

The two template parameters for this class are:

- `PARAMS`, defining the type that will store the route parameters. It's required to implement assignation of parameters through `operator[](const std::string&)`
- `ACTION`, defining the object that will be stored for each route, and returned when one of those has matched an URI.

Here's an example of a simple implementation:

```c++
typedef std::map<std::string, std::string> MyParams;
typedef std::string MyAction;

class MyRouter : public Crails::RouterBase<MyParams, MyAction>
{
};
```

To initialize such a router, you should add routes:

```c++
MyRouter router;

router.match("/simple_route", MyAction("route1"));
router.match("/route/with/:param", MyAction("route2"));
```

Afterwards, you'll be able to match routes using functions such as:

```c++
static void display_action_for(const MyRouter& router, const std::string& uri)
{
  MyParams params;
  MyAction* action;

  action = router.get_action(uri, params);
  if (action != nullptr)
    std::cout << "Found action " << *action << std::endl;
  else
    std::cerr << "Action not found for uri " << uri << std::endl;
}
```

When a route matches, the `params` argument gets populated with the route parameters:

```c++
action = router.get_action(uri, params);
if (action && params.find("param") != params.end())
{
  std::string value = params.at("param");
  std::cout << "Called a route with parameter `param`=" << value << std::endl;
}
```
