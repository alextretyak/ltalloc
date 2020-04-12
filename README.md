Overview
--------

Simple (yet very efficient) multi-threaded memory allocator based on free lists.

It is best suited for applications doing a lot of small (<256B) memory allocations (as usually C++ stl containers do), and from many simultaneously running threads.

Features
--------

* O(1) cost for alloc, free (for blocks of size <56KB)
* Low fragmentation
* Near zero size overhead for small allocations (no header per allocation, just one common 64 bytes header for all blocks inside 64KB chunk)
* High efficiency and scalability for multi-threaded programs (almost lock-free, at maximum one spin-lock per 256 alloc/free calls for small allocations, even if all memory allocated in one thread then freed inside another thread)

Usage
-----

To use ltalloc in your C++ application just add [ltalloc.cc](https://github.com/alextretyak/ltalloc/blob/master/ltalloc.cc) source file into your project's source files list. It overrides global operators new and delete, which is a fully C++ standard compliant way to replace almost all memory alocation routines in C++ applications (as stl container's default allocators call global operator new). But if this way is not well suilable for you, the other options of plug-in ltalloc into your application are exists as well. Actually, ltalloc.cc source is written in C (and overriding of operators new/delete is disabled automatically if `__cplusplus` is not defined), so it can be compiled both as C and C++ code.

[Here is a more detailed description.](http://alextretyak.github.io/ltalloc/wiki.htm)

[Описание на русском.](http://alextretyak.github.io/ltalloc/wiki_ru.htm)
