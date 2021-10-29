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

## Week 7 progress
### How other operating systems written in rust implement kernel modules or dynamic linker?
#### Theseus
Everything, including applications, system services, and core kernel components, exists and runs in a single address space and a single privilege level (in "kernel space"). However, every application lives in its own namespace. Theseus doesn't rely on hardware protection but rely on rust language features and compilers. The disadvantage is that it only allows safe code compiled by rustc. As kernel modules and user applications are cells in Theseus, there is no difference between those two. Most of the code is located in [loadc](https://github.com/theseus-os/Theseus/blob/theseus_main/applications/loadc/src/lib.rs).
1. If some dependencies are static and have been initialized in the current kernel, we should overwrite these sections in ELF to point them to the old one not the uninitialized one.
2. Then we just parse ELF, find symbols, modify the relocation and copy `.text` into RAM just like we do in C.
3. Applications are developed within the source tree. So we don't need to care about how to export header files like C and develop kernel modules out of tree like Linux.
#### Redox
Redox is an microkernel OS mainly aims at easy use.
Redox plans to use [dryad](https://github.com/m4b/dryad) as dynamic loader. However the author met some difficulties and haven't finished yet, details [here](https://gitlab.redox-os.org/redox-os/redox/-/issues/927). Dryad started as an experiment to write a parallel dynamic linker. Parallel isn't my purpose, so it may helps little.
### Todo
Port loadc of Theseus to zCore. Code isn't that much, and I don't think it's hard work.
