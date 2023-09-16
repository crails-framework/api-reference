This singleton class is used to create instances of mail services, used to send mails through one of the provided backends.

Mail services are created using a [MailServers::Conf] object, which can be easily generated using the [MailServer] helper class.

```c++
std::shared_ptr<Crails::MailServiceInterface> service;

service = Crails::MailServers::singleton::require().create(Crails::MailServer()
  .backend(MailServers::SMTP)
  .hostname("mail.gandi.net")
  .port(587)
  .use_tls(true)
);
```

You can also pre-define a set of configuration in the `config/mailers.cpp` file. See the documentation for [MailServer] for further details. The configurations defined this way can then be used as following:

```c++
std::shared_ptr<Crails::MailServiceInterface> service;

service = Crails::MailServers::singleton::require().create("Your configuration name goes here");
```
