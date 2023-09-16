This sends a list of emails through a mail service. Depending on the backend, the resulting process may involve sending all the mails at once, or one by one.

If all the mails are sent with success, the callback specified as a parameter will be called.

See [MailServiceInterface::set_error_callback] to see how to manage the errors that may occur when sending mail.
