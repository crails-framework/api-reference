Renders anoter template within the current template.

Parameters:
- Path to the template to render
- Optional [SharedVars] containing variables to use when rendering the template

The called template will be rendered using the same set of variables that was provided for the template calling `partial`. If a [SharedVars] parameter is provided, it will only overwrite variables that are present in both the current template variable and the parameter.
