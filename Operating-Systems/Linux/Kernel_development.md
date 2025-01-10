# TO many arguemnts for class_create


In my case this happend when compiling fmem 1.6.0
```error
 error: too many arguments to function ‘class_create’
  381 |         mem_class = class_create(THIS_MODULE, "fmem");

```

the specific call is listed in the error that caused the problem. 
[A explenation can be found here](https://kb.meinbergglobal.com/kb/driver_software/driver_software_for_linux/troubleshooting_build_problems/build_error_related_to_calling_class_create_function) it boils down to a change in kernel 6.4. 

in my case the following c code fixed it 

```c
	#if(LINUX_VERSION_CODE >=KERNEL_VERSION(6, 4, 0))
	mem_class = class_create("fmem");
	#else
	mem_class = class_create(THIS_MODULE, "fmem");
	#endif
```
