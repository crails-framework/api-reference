Sets a redirect status on the response and immediately sends it, immediately ending the current transaction. The client will be redirected to the url specified as a parameter:

```c++
void MyController::index()
{
  // Redirect to your own webapp:
  redirect_to("/local-path");
  // Redirect to another website:
  redirect_to("https://duckduckgo.com");
}
```

By default, `redirect_to` uses the [303 See Other](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/303) response status. You may override this behaviour by using `redirect_to`'s overload and specifying a custom response status using [Crails::HttpStatus]:

```c++
void MyController::index()
{
  redirect_to(Crails::HttpStatus::moved_permanently, "/local-path");
}
```
