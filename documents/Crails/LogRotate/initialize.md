Initializes the [Logger] with rotating logs. The two parameters are pathes to the files that are to be used for event and error logs respectively.

If the error log path is left empty, error logs will be redirected to the event log.

If the event log path is left empty, event logs won't be redirected anywhere, and will be printed in the standard output instead.
