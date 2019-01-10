# systemtap-scripts
## mem_leak_libc.stap
trace glibc malloc andd free to find leak function
## mem_static.stap
trace glibc malloc calloc realloc function to find the top malloc funtion which may cause memory fragmentation
## io_static.stap
find the process and file who makes io top 
