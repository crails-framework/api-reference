Checks if a file can be written on or overwritten. Arguments are: `task_name`, identifier for the process that's prompting the file writing, and `path` which is the path of the file to write.

If no file exist at the given path, this function will return `true`.

If a file already exists at the given path, a prompt will appear on the terminal to ask the user whether they want the file overwritten or not.  This function will return `true` or `false` depending on the user's answer.
