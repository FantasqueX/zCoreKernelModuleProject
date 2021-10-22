# zCoreKernelModuleProject
kernel module implementation for zCore

## Week 5 progress
### Reference for kernel module
+ https://en.wikipedia.org/wiki/Loadable_kernel_module
+ https://en.wikipedia.org/wiki/VDSO

### Reference for zCore
+ https://github.com/rcore-os/zCore-Tutorial
+ https://en.wikipedia.org/wiki/Fuchsia_(operating_system)
+ https://fuchsia.dev/fuchsia-src/concepts/kernel/concepts

## Week 6 progress
### Toy loader
+ https://blog.cloudflare.com/how-to-execute-an-object-file-part-1/
+ https://blog.cloudflare.com/how-to-execute-an-object-file-part-2/
+ https://blog.cloudflare.com/how-to-execute-an-object-file-part-3/

I implemented a toy loader in C learning from Cloudflare blog.

### Real kernel module
A kernel module is just a relocatable object file, and I can load it just like normal binary files.
Questions: How to define the convention of zCore module, for example init and exit? How to build our kernel module without kbuild system? And how about `ftrace`?

Reference: https://blog.linuxplumbersconf.org/2014/ocw/system/presentations/1773/original/ftrace-kernel-hooks-2014.pdf
