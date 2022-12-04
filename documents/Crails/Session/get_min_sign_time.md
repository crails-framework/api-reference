Returns the timstamp of the oldest valid session. Any session opened before that time will be discarded.

The result is based on `USER::session_duration`, which should be defined by your `USER` model.
