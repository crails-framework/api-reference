Loads file from the filesystem, and caches them until `garbage_collect` is called. The [FileCache::Lock] class should be used
as a [scope guard](https://stackoverflow.com/questions/31365013/what-is-scopeguard-in-c) to ensure thread safety when interacting
with this class.

Requested files are loaded into memory if they haven't been already. Subsequent requests for the same file will fetch
the file diretly from memory, which will speed up your application considerably if you often need to consult the same
files.

The Crails server provides an instance of `FileCache` available using the `Crails::Server::get_file_cache` method. This instance
is _never_ subject to garbage collection, as the amount of files present in your _public folder_ is finite and supposedly should
not take up to much space in memory.

If you intend to use [FileCache] for other purposes, don't forget to call on the `garbage_collect` method once in a while.
