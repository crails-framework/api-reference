Helper class to store and check encrypted passwords. It extends [std::string], but encrypts any content assigned to it using `operator=`.

Default encrypting algorithm is `AES-256`. You can override this behavior by extending on `Password` and overloading the `encrypt` method.

You can then use the `==` comparator to check it against crypted or uncrypted passwords:

```c++
std::string unencrypted_password("hello");
Crails::Password encrypted_password(unencrypted_password);

encrypted_password == unencrypted_password; // evaluates to true

encrypted_password == Crails::Password("hello"); // evaluates to true

encrypted_password == "hello"; // evaluates to true

encrypted_password == encrypted_password.c_str(); // evaluates to false
```
