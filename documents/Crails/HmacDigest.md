[HMAC](https://en.wikipedia.org/wiki/HMAC) is a [MAC](https://en.wikipedia.org/wiki/Message_authentication_code) (message authentication code) involving a cryptographic hash function and a secret cryptographic key. It may be used both to verify data integrity and the authenticity of a message.

The [HmacDigest] class takes three parameters as its constructor:

- A cryptographic function, provided by the OpenSSL library (such as [EVP_sha1](https://www.openssl.org/docs/man1.1.1/man3/EVP_sha1.html), [EVP_sha3-224](https://www.openssl.org/docs/man1.1.1/man3/EVP_shake256.html), [MD5](https://www.openssl.org/docs/man1.1.1/man3/EVP_md5.html)),
- The secret cryptographic key,
- The message to be hashed.

HMAC does not encrypt the message. Instead, the message (encrypted or not) must be sent alongside the HMAC hash. Parties with the secret key will hash the message again themselves, and if it is authentic, the received and computed hashes will match.

#### Example

The following example checks the authenticity of a message:

```c++
#include <crails/hmac.hpp>

bool verify_message(const std::string& message, const std::string& hashed_message)
{
  static const std::string secret_key("4142912351.13828282@deusto.edu");
  Crails::HmacDigest challenge(EVP_sha256(), secret_key, message);

  return challenge.to_string() == hashed_message;
}
```

In this example, the `hashed_message` value by a 3rd party is represented as an hexadecimal string.
If the hashed_message had been encoded in Base64 instead, we'd replace `digest.to_string()` with `digest.to_base64()`.

#### Other

See [HmacMd5Digest] from `crails/md5.hpp` to implement HMAC-MD5 with less verbose code.
