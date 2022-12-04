Route handler for [WebSocket].

Usage:

```c++
struct MySocket : public Crails::WebSocket
{
  MySocket(Crails::Context& context) : Crails::WebSocket(context) {}

  void action_method()
  {
    send("Hello, world !");
  }
};

void Router::initialize()
{
  using namespace Crails;
  using namespace std;

  match("GET", "/websocket", [](Context& context, function<void()> callback)
  {
    WebSocketRoute<MySocket>::trigger(context, &MySocket::action_method, callback);
  });

  // Alternatively:
  match("GET", "/alt-websocket",
    bind(
      SocketRoute<MySocket>::trigger,
      placeholders::_1,
      &MySocket::action_method,
      placeholders::_2
    )
  );
}
```

The `WebSocketRoute` header also defines the `match_websocket` macro to facilitate route declaration:

```c++
void Router::initialize()
{
  match_action("GET", "/websocket", MySocket, action_method);
}
```
