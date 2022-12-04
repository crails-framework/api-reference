Simple interface for encrypting [std::string] using OpenSSL.

Example:

```c++
#incude <crails/message_digest.hpp>

int main(int argc, const char** argv)
{
  Crails::MessageDigest digest(EVP_sha512());
  std::string result;

  for (int i = 1 ; i < argc ; ++i)
    digest << argv[i];
  digest >> result;
  std::cout << resutl << std::endl;
  return 0;
}
```

The first argument of the default constructor may either be a pointer to a `EVP_MD` structure, which contains the
implementation of a cipher. Examples be [md5](https://www.openssl.org/docs/man1.1.1/man3/EVP_md5.html), [sha](https://www.openssl.org/docs/man1.1.1/man3/EVP_sha256.html),
[ripemd](https://www.openssl.org/docs/man3.0/man3/EVP_ripemd160.html), etc.

You may also pass a string as parameter to MessageDigest's constructor. In which case, it will try to find
a cipher using [EVP_get_digestbyname](https://www.openssl.org/docs/manmaster/man3/EVP_get_digestbyname.html).
