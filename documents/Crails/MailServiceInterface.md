The [MailServiceInterface] allows you to connect to a mail service and use it to send mails, without having to care about which backend you're using.

Instances implementing [MailServiceInterface] can be created using the [MailServers] singleton. The object will be provided within a [std::shared_ptr].

The methods defined by [MailServiceInterface] may be asynchronous: you are responsible for keeping a reference to the [std::shared_ptr] until the completion of any task you've started.
