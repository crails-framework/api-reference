Interface for targets of a [Renderer]. A render target can be a file, a string, an HTTP response, a mail.

Render targets can include a body and a set of headers: the [Renderer] will call `set_body` to send the content of a rendered [Template] to the `RenderTarget`. It will also call `set_headers` to specify HTTP headers related to the rendered content, such as `Content-Type`.

Example of implementations: [StringTarget], [FileTarget] or [BuildingResponse].
