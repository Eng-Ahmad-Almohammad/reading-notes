# shutil

## Copying Files
### copyfile() copies the contents of the source to the destination and raises IOError if it does not have permission to write to the destination file.

### Because the function opens the input file for reading, regardless of its type, special files (such as Unix device nodes) cannot be copied as new special files with copyfile().

### The implementation of copyfile() uses the lower-level function copyfileobj(). While the arguments to copyfile() are filenames, the arguments to copyfileobj() are open file handles. The optional third argument is a buffer length to use for reading in blocks.

### The copy() function interprets the output name like the Unix command line tool cp. If the named destination refers to a directory instead of a file, a new file is created in the directory using the base name of the source.
## Copying File Metadata
### By default when a new file is created under Unix, it receives permissions based on the umask of the current user. To copy the permissions from one file to another, use copymode().

### To copy other metadata about the file use copystat().
## Working With Directory Trees
### shutil includes three functions for working with directory trees. To copy a directory from one place to another, use copytree(). It recurses through the source directory tree, copying files to the destination. The destination directory must not exist in advance.

### The symlinks argument controls whether symbolic links are copied as links or as files. The default is to copy the contents to new files. If the option is true, new symlinks are created within the destination tree.

### copytree() accepts two callable arguments to control its behavior. The ignore argument is called with the name of each directory or subdirectory being copied along with a list of the contents of the directory. It should return a list of items that should be copied. The copy_function argument is called to actually copy the file.

## Finding Files
### The which() function scans a search path looking for a named file. The typical use case is to find an executable program on the shell’s search path defined in the environment variable PATH.

## Archives
### Python’s standard library includes many modules for managing archive files such as tarfile and zipfile. There are also several higher-level functions for creating and extracting archives in shutil. get_archive_formats() returns a sequence of names and descriptions for formats supported on the current system.
### Use make_archive() to create a new archive file. Its inputs are designed to best support archiving an entire directory and all of its contents, recursively. By default it uses the current working directory, so that all of the files and subdirectories appear at the top level of the archive. To change that behavior, use the root_dir argument to move to a new relative position on the filesystem and the base_dir argument to specify a directory to add to the archive.

## File System Space
### It can be useful to examine the local file system to see how much space is available before performing a long running operation that may exhaust that space. disk_usage() returns a tuple with the total space, the amount currently being used, and the amount remaining free.