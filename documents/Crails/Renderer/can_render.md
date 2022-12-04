Should deduce if a Renderer can render a view template for the given mimetype format pattern.

Parameters:
- Name of the view template
- The value of a [Accept](https://developer.mozilla.org/fr/docs/Web/HTTP/Headers/Accept) HTTP header

This method should return `false` if the given template does not exist for the Renderer, or if the format used by the renderer does not satisfy the request made by the `Accept` header.
