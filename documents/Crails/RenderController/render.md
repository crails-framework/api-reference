The render method is designed to conclude a transaction with a client. When called, it will set the body on your [HttpResponse] and directly send it to the client. Note that changes you make to the response afterwards will not reach the client.

The render method also sets the `Content-Type` header on your response.

There are two ways to use the render method:

#### Rendering a view template

If you have defined view templates for your [Renderer], you can render them by calling the `render` method with the template's name:

```c++
void MyController::show()
{
  render("resources/show");
}
```

##### Shared variables

The `RenderController` provides its own [SharedVars] instance, which will be provided to all the templates rendered through the controller.

```c++
void MyController::show()
{
  vars["variable"] = (int)42;
  render("resources/show");
}
```

If you want to provide additional variables for your template, you may also specify those as a parameter:

```c++
void MyController::show()
{
  render("resources/show", {
    {"variable", (int)42}
  });
}
```

#### Rendering custom data

If you are not using a [Renderer], you can also provide your data directly as a [std::string]:

```c++
void MyController::show()
{
  render(TEXT, "rendering text");

  render(JSON, "{ \"key\": \"value\" }");
}
```

Or a [Data] object:

```c++
void MyController::show()
{
  DataTree data;

  data["key"] = "value";
  render(TEXT, data["key"]); // will render: value

  render(JSON, data); // will render: {"key":"value"}
}
```
