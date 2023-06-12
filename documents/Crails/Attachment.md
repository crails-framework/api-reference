Represents a file in a persistent storage. The reference to that file can be stored in database using a string of characters.

The attachment can be initialized from a [Params] object using the [Attachment::use_uploaded_file] method:

- the file will be stored with a randomly generated filename in the folder pointed at by the [Attachment::get_store_path] - you may overload this
method to store files in a custom folder.

- a UID will be generated which can be stored in a database, to assign the attachment to a given model.

The file can then be removed from storage using the [Attachment::cleanup_files] method.
