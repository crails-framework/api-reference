Writes a file if needed, and returns sucess status. Arguments are: `task_name`, an identifier for the process that's writing the file, a `path` defining where to write the file, and `contents` for the expected contents of the file.

Will recursively create the parent directories if needed.

If a file already exist at the given path, will first read the existing file. The file will only be overwritten if the content found differs from the expected contents.

This is useful when generating C++ files, to avoid needlessly re-compiling the same code after using a code generator.
