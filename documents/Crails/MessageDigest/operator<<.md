Performs a digest update using [EVP_DigestUpdate](https://www.openssl.org/docs/man3.0/man3/EVP_DigestUpdate.html).

Note that `digest << "Hello" << "world"` isn't the same as `digest << "Helloworld"`, as a single digest update will be applied for each strings.
