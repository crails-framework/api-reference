Exception thrown when a [Renderer] was requested to render a [Template] that does not exist.

Be mindful that a template isn't merely defined by its name, but also by the format it may answer to: this exception will be thrown both if no template with an adequate name was found, or if none of the renderers containing such a template support the format requested by the client in the `Accept` header.
