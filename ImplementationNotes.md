# Implementation Notes #
> A quick read through the NDMP API docs has shown me that in relation to LVM integration, there are 2 functions which will interest us most.
  1. [ModuleStartFunc](ModuleStartFunc.md) - Indicates to the server that a backup operation is beginning
  1. [NdmpdDoneFunc](NdmpdDoneFunc.md) - Indicates to the server that a backup operation is finished

> It is my opinion that the ModuleStartFunc should be extended to add the following capabilities:
  1. Make a call to the Linux VFS to sync all disks
  1. Create a new snapshot via LVM2
  1. Mount the snapshot to a directory name defined in the server configuration file

> Furthermore, the NdmpDoneFunc should be extended to perform the following operations:
  1. Unmount the snapshot from the filesystem
  1. Release the snapshot from the LVM2 mapper


> Beyond the LVM2 integration, we should provide support for integrating arbitrary application plugin APIs for things like PostgreSQL, MySQL, HSQLDB, etc.... This would allow the NDMP server to be a fully functional and flexible Linux backup agent on par with agents available for other operating systems and applications. The plugins would extend/override the Read/Seek functions and allow access to application data using native APIs for the given application.