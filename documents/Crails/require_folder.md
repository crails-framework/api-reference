Recursively creates a given folder. Arguments are: `task_name`, identifier for the process that's creating the directories, and `path` which is the path of the final directory to create.

Returns `true` on success, `false` if it was impossible to create the folder (which can happen when you don't have the right permission, or if a file already exists at the exact path of one of the directories to create).
