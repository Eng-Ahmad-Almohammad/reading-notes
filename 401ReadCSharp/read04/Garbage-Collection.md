# Fundamentals of garbage collection

In the common language runtime (CLR), the garbage collector (GC) serves as an automatic memory manager. The garbage collector manages the allocation and release of memory for an application. For developers working with managed code, this means that you don't have to write code to perform memory management tasks. Automatic memory management can eliminate common problems, such as forgetting to free an object and causing a memory leak or attempting to access memory for an object that's already been freed.


## Benefits
The garbage collector provides the following benefits:

1- Frees developers from having to manually release memory.

2- Allocates objects on the managed heap efficiently.

3- Reclaims objects that are no longer being used, clears their memory, and keeps the memory available for future allocations. Managed objects automatically get clean content to start with, so their constructors don't have to initialize every data field.

4- Provides memory safety by making sure that an object cannot use for itself the memory allocated for another object.

