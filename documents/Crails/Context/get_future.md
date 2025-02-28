Returns a [std::future] allowing you to asynchronously access the status code for the response sent to the client.

Trying to read the value contained in this [std::future] can also help you wait until the HTTP query managed by this context has been entirely handled. At which point, the Context object will be destroyed: if you intend to safely interract with a Context object after the [std::future] object has been read, make sure to keep an instance of [std::shared_ptr] alive, by using `context.shared_from_this()`.
