Provides the [Crails::Renderer] and [Crails::RenderTarget] interfaces. Applications can then register renderers for various `Content-Type` target, and for each of those, register a series of [Crails::Renderer::Generator] callbacks.

The [Crails::Renderer::Generator] callbacks then generate the content of a template into a [Crails::RenderTarget] which can be a string, a file, an HTTP response, or any of your own implementations of RenderTarget.

Example of Renderer implementation:

```c++
class MyRenderer : public Crails::Renderer
{
public:
  MyRenderer()
  {
    templates.emplace("my-view", [](
      const Crails::Renderer& renderer,
      Crails::RenderTarget& target,
      Crails::SharedVars& properties)
    {
      target.set_header(Crails::HttpHeader::content_type, "text/plain");
      target.set_body("Hello, world!");
    });
  }

  bool can_render(const std::string& accept, const std::string& view) const override
  {
    sregex_iterato
    return accept.find("text/plain") != std::string::npos
        && templates.find(view) != templates.end();
  }

  void render_template(
    const std::string& view,
    Crails::RenderTarget& target,
    Crails::SharedVars& properties) const override
  {
    auto generator = templates.find(view);

    if (generator != templates.end())
      generator->second(*this, target, properties);
    else
      throw Crails::MissingTemplate(view);
  }
};
```

Adding this renderer to a Crails application would imply modifying the `config/renderers.cpp` file:

```c++
void Renderer::initialize()
{
  renderers.push_back(new MyRenderer);
}
```

You'll then be able to use the renderer through a [Crails::RenderController], or manually:

```c++
auto* renderer = Renderer::pick_renderer("my-view", "text/plain");
Crails::RenderString target;

if (renderer != nullptr)
  renderer->render_template("my-view", target, {});
std::cout << target.c_str() << std::endl;
```
