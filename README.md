# systemtap-scripts
## mem_leak_libc.stap
trace glibc malloc andd free to find leak function



## mem_static.stap
trace glibc malloc calloc realloc function to find the top malloc funtion which may cause memory fragmentation
```
bytes(not free yet): 16280320000
 value |-------------------------------------------------- count
  8192 |                                                        0
 16384 |                                                        0
 32768 |@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@  317975
 65536 |                                                        0
131072 |                                                        0

ngx_alloc+0xf [nginx]
ngx_palloc_large+0x13 [nginx]
ngx_palloc+0x42 [nginx]
ngx_create_temp_buf+0x27 [nginx]
ngx_http_subs_match+0xa99 [nginx]
```

## io_static.stap
find the process and file who makes io top 
