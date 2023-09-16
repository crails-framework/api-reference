This class helps you define mail server configurations for the [MailServers] class.

This class is typically used in the `config/mailers.cpp` file, and can be used to define configurations
for any supported backend.

Here are a few examples using this class for various backends:

### Smtp server

```c++
#include <crails/mail_servers.hpp>

using namespace Crails;

const MailServers::servers = {
  {
    "smtp", MailServer()
      .hostname("mail.gandi.net")
      .port(587)
      .use_tls(true)
      .use_authentication(true)
      .username("username@domain.org")
      .password("password")
  }
};
```

### MailGun HTTP API

```c++
#include <crails/mail_servers.hpp>

using namespace Crails;

const MailServers::servers = {
  {
    "mailgun", MailServer()
      .backend(MailServers::MailGun)
      .hostname("mg.domain.org")
      .username("API Key ID")
      .password("API Key")
};
