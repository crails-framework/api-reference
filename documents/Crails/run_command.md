Runs a single shell command, wait for it to end, and returns `true` if the exit status was zero. Standard and error output will be displayed on the terminal.

Optionaly, a reference to a [std::string] can be used as second parameter: in which case, the _standard output_ won't be displayed on the terminal, and will be stored in the string parameter instead.
