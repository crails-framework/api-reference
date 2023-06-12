Object-Oriented wrapper for [libssh](https://www.libssh.org) with stream redirection.

#### Examples
##### Executing commands
```c++
#include <crails/ssh/session.hpp>
#include <sstream>
#include <iostream>

int main()
{
  Crails::Ssh::Session ssh;
  std::stringstream stream;

  ssh.should_accept_unknown_hosts(true);
  ssh.authentify_with_pubkey("password");
  ssh.connect("ubuntu", "192.168.0.15");

  // Store the output of stdout and stderr into stream
  ssh.exec("ls -lah", stream);

  // Display the output of the remote stdout and stderr to the current process' stdout and stderr
  ssh.exec("ls -lah", std::cout, std::cerr);

  return 0;
}
```

##### Uploading files
```c++
#include <crails/ssh/session.hpp>

int main()
{
  Crails::Ssh::Session ssh;

  ssh.should_accept_unknown_hosts(true);
  ssh.authentify_with_password("password");
  ssh.connect("ubuntu", "192.168.0.15");

  // Creates the file "/home/ubuntu/filename" with contents "Hello, world!"
  auto scp = ssh.make_scp_session("/home/ubuntu", Crails::Ssh::WriteMode);
  scp->push_text("Hello, world!", "filename");

  // Outputs the contents of "/home/ubuntu/filename" to the standard output
  ssh.make_scp_session("/home/ubuntu/filename", Crails::Ssh::ReadMode)
    ->pull_file(std::cout);
}
```
