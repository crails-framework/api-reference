Sets a status on a response and immediately send it to the client. Example:

```c++
void MyController::show()
{
  respond_with(Crails::HttpStatus::not_found);
}
```

The `respond_with` method concludes the transaction with the client, meaning that if you want to send a body along with the response, you must provide the body _before_ calling `respond_with`:

```c++
// Valid implementation
void MyController::show()
{
  response.set_header(Crails::HttpHeader::content_type, "text/plain");
  response.set_body("Oops ! Resource not found !");
  respond_with(Crails::HttpStatus::not_found);
}

// Invalid implementation
void MyController::show()
{
  respond_with(Crails::HttpStatus::not_found);
  // The following lines will be ignored:
  response.set_header(Crails::HttpHeader::content_type, "text/plain");
  response.set_body("Oops ! Resource not found !");
}
```
