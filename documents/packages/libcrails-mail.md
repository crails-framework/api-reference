Sends email using SMTP or MailGrid.

The mail module provides classes to represent emails, use view to render an email's body, and send them to their recipients through various backends.

You can add this module to your Crails application using the following command:

```
crails plugins mail install
```

This will create the `config/mailers.cpp` file, which can be used to define the mail services
your application will use: see the [Crails::MailServer] documentation for more details.
 
Once your server are configured, you may then interact with them through a [Crails::MailServiceInterface], obtained
by using the [Crails::MailServers] singleton, or through a [Crails::Mailer]. The latter is designed to be used from
a [Crails::Controller] and allows you to render Crails Views as emails.

The mailing API is asynchronous, and you're responsible for making sure that the objects calling the API
aren't deleted until the sending process is over. This can easily be achieved by encapsulating [std::shared_ptr]
objects within the callback sent to the [Crails::Mailer::send] or [Crails::MailServiceInterface::send] methods.
