The Mailer class helps you quickly rendering emails using Crails views.
The relevant `render` methods provided in [Crails::RenderController] are also
implemented in the [Crails::Mailer] class.

The Mailer class is designed to be inherited from, as it provides virtual methods
that you can override to handle the success or failure of the mail sending process.

Its constructor takes a reference [Crails::Controller] as parameter, as well as the
name of a mail service configuration as defined in `config/mailers.cpp`.

### Examples

```c++
#include <crails/mailer.hpp>

class WelcomeMailer : public Crails::Mailer
{
public:
  WelcomeMailer(WelcomeController& controller) : Mailer(controller, "smtp")
  {
    mail.set_sender("My Application", "no-reply@myapplication.com");
  }

  void add_recipient(const std::string& name, const std::string& mail)
  {
    mail.add_recipient(name, mail);
  }

  void on_error_occured() override
  {
    reinterpret_cast<WelcomeController*>(controller)->on_welcome_failure();
  }
};

void WelcomeController::welcome()
{
  auto mailer = std::make_shared<WelcomeMailer>();

  mailer->add_recipient("Christophe Lambert", "c.lambert@wanadoo.fr");
  mailer->render("welcome/email", {
    {"message", "Hello World"}
  });
  mailer->send([this, mailer]()
  {
    on_welcome_success();
  });
}

void WelcomeController::on_welcome_success()
{
  render("welcome/view");
}

void WelcomeController::on_welcome_failure()
{
  render("welcome/failure");
}
```
