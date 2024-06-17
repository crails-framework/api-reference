Simple Captcha generator with support for custom captchas using [libcapt](https://github.com/crails-framework/libcapt) or [reCAPTCHA](https://developers.google.com/recaptcha).

You may add this module to your Crails application using the following command:

```sh
crails plugins extra -a libcrails-captcha
```

## Setting up custom captchas

The only thing you need to setup custom captcha is to download a font for the captcha and initialize it
within the main function of your server.

The font must use the CPF format. Examples of such fonts can be found in the [libcapt repository](https://github.com/crails-framework/libcapt/tree/master/fonts).

Setup these fonts in your main function as following:

```cpp
  Crails::Captcha::Default::set_font_file("./latin.cpf");
```

The filepath (here, `./latin.cpf`) must be relative to the directory in which the server runs. Keep that in mind when deploying your applications to production.

## Setting up Google reCAPTCHA

**TODO**

## Including a captcha in a form

The first step is to generate a captcha input and share it with your view, from your controller:

```cpp
#include <crails/captcha/default.hpp>

void MyController::form()
{
  Crails::Captcha::Default captcha;

  vars["captcha_form"] = captcha.render(params);
  render("my/form");
}
```

Then render the captcha input into your form:

```html
const std::string @captcha_form;
// END LINKING
<form action="/my-controller/submit" method="post">
  <div class="form-group">
    <label for="input">Input</label>
    <input type="text" name="input" />
  </div>

  <div class="form-group">
    <%= captcha_form %>
  </div>

  
</form>
```

Lastly, use the `check` method to verify whether the captcha was properly filled
by the user:

```cpp
void MyController::submit()
{
  Crails::Captcha::Default captcha;
  auto self = shared_from_this(); // as the process may be asynchronous, you must
                                  // keep a shared_ptr stored within your callback
                                  // to ensure the request won't be closed by the server.

  captcha.check(params, [this, self](bool success)
  {
    if (success)
      render(TEXT, "Yay, it works");
    else
      render(TEXT, "Captcha was invalid");
  });
}
```

These examples are written using the default captcha generator. If you want to use reCAPTCHA instead,
just replace `#include <crails/captcha/default.hpp>` with `#include <crails/captcha/google.hpp>` and
`Crails::Captcha::Default` with your custom overload of the `Crails::Captcha::Google` class.
