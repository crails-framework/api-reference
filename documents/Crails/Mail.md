Represents an email with its various attributes: content, sender, recipients...

The mail object is a [RenderTarget], making it possible to use as the target for calls to the [Renderer].

The represented mail can then be sent using one of the implementations for [MailServiceInterface].

#### Example

Here's a simple example of sending an email using [MailServers] and [MailServiceInterface]:

```c++
#include <crails/mail.hpp>
#include <crails/mail_servers.hpp>

void send_mail()
{
  Crails::Mail mail;
  std::shared_ptr<MailServiceInterface> service;

  service = MailServers::singleton::require().create("smtp");
  mail.set_sender("greeter@domain.org", "The Name of the Platform");
  mail.set_reply_to("admin@domain.org");
  mail.add_recipient("user@aol.com", "Pilip Edmund 1st of the name");
  mail.set_subject("Hello World");
  mail.set_body("<h1>Greetings</h1>, universe !.");
  mail.set_header("Content-Type", "text/html");
  service->connect([mail, service]()
  {
    service->send(mail, [service]()
    {
      // Mail sent successfully
    });
  });
}
```
