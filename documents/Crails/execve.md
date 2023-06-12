Multiplatform implementation of [execve](https://www.man7.org/linux/man-pages/man2/execve.2.html). Replaces the current process with a new one running the command and parameters sent as parameters.

Returns zero if the command paramerer was invalid. Otherwise, returns the return value of the system-provided `execve` function ([Windows](https://learn.microsoft.com/en-us/cpp/c-runtime-library/reference/execve-wexecve?view=msvc-170), [Linux](https://www.man7.org/linux/man-pages/man2/execve.2.html), [FreeBSD](https://www.freebsd.org/cgi/man.cgi?query=execve&sektion=2)).
