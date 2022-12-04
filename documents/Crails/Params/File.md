Represents a file uploaded by the client request.

Uploaded files are temporarily stored in a path specified by `Server::temporary_path` using a random filename.

Uploaded files are removed after a transactions ends, as the containing [Params] object gets destroyed.
