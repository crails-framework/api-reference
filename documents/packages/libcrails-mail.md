Sends email using SMTP or MailGrid.

The mail module provides classes to represent emails, use view to render an email's body, and send them to their recipients through various backends.

You can add this module to your Crails application using the following command:

```
crails plugins mail install
```

This will create the `config/mailers.cpp` file, which can be used to define the mail services
your application will use. The following example shows how you'd configure your mail servers
for an SMTP server and a MailGrid account:

```c++
#include <crails/mail_servers.hpp>

using namespace Crails;

const MailServers::List MailServers::servers = {
  {
    "smtp", MailServer()
      .hostname("mail.gandi.net")
      .port(587)
      .use_tls(true)
      .use_authentication(true)
      .authentication_protocol(Smtp::Server::PLAIN)
      .username("you@domain.es")
      .password("YOPASSWORD")
  },
  {
    "mailgun", MailServer()
      .backend(MailServers::MailGun)
      .hostname("mg.domain.es")
      .username("Your API key's id")
      .password("Your API key")
  }
};
```

Once your server are configured, you may then interact with them through a [Crails::MailServiceInterface]
or a [Crails::Mailer]. The latter is designed to be used from a [Crails::Controller].

The mailing API is asynchronous, and you're responsible for making sure that the objects calling the API
aren't deleted until the sending process is over. This can easily be achieved by encapsulating [std::shared_ptr]
objects within the callback sent to the [Crails::Mailer::send] or [Crails::MailServiceInterface::send] methods.

#### Examples
##### Using a Mailer object
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

