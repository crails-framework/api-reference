Implementation of [SessionStore] based on cookies. Session variables are stored within the [Cookie and Set-Cookie](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cookie) headers.

If `Crails::CookieData::use_encryption` is set to true, the `Cookie` headers will be encrypted using `AES-256`. Otherwise, they'll transit unencrypted, which can be considered a security flaw.
