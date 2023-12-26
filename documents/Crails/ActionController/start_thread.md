Starts a thread for the current [Context]. The thread is returned in a detached state.

The callback parameter won't be called immediately, as only one thread at a time can run on a given [Context]. It will also be protected from thrown exceptions: note that if the context request hasn't received an answer yet, throwing an exception from the thread will send an error response to the client. If the request already received a repsonse however, the exception will only be recorded in the logs.

The following example uses `start_thread` to provide a delayed response:

```c++
void MyController::action()
{
  auto self = shared_from_this();

  start_thread([this, self]()
  {
    respond_with(HttpStatus::ok);
  });
}
```

Note that we created the `self` variable to keep a reference to `MyController`, so it doesn't get removed until the thread's task ends. This is only useful because we use the controllers' methods to send a response to the client. Otherwise, a call to `start_thread` can be even simpler: here's an example using `start_thread` to run a command:

```c++
void MyController::action()
{
  respond_with(HttpStatus::ok);
  start_thread([]()
  {
    boost::process::child process("ffmpeg -i attachment.ogg -acodec libmp3lame attachment.mp3");

    process.wait();
    if (process.exit_code() != 0)
      Crails::logger << Crails::Logger::Error << "Failed to convert attachment.ogg" << Crails::Logger::endl;
  });
}
```
