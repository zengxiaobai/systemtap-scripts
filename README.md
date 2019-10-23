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

**TODO**
Also we can change this script to trace some process's logs, if we donot kown whether some dynamic lib such as (rocketxclean uses rocketmq-cpp, librocketmq.so) logging at /root/logs/rocketmq-cpp/ silently until making the disk usage bombs at produce environment. Make this Check as a Tool Service when you start a new program,just like standard background services's core_check.sh 、core_clear.sh、delete_logs.sh、service_check.sh and so on.  Also we can use strace, but use systemtap can make tools more quickly.
```
START####################

         Process	     PID	   inode	   KB Read	KB Written	    Path
             dig	   14665	34072580	        10	         0	/etc/pki/tls/openssl.cnf
             dig	   14668	34072580	        10	         0	/etc/pki/tls/openssl.cnf
             srs	   13109	4026532015	         2	         0	    /proc/vmstat
            tail	   14666	    1359	         2	         0	/usr/share/locale/locale.alias
            grep	   14667	    1359	         2	         0	/usr/share/locale/locale.alias

END###################


START####################

         Process	     PID	   inode	   KB Read	KB Written	    Path
    rocketxclean	    4015	34313132	         0	         6	/root/logs/rocketmq-cpp/4015_rocketmq-cpp.log.0
       PullMsgTP	    4016	58426974	         0	         4	/root/logs/rocketmq-cpp/4016_rocketmq-cpp.log.0
      DispatchTP	    4016	58426974	         0	         4	/root/logs/rocketmq-cpp/4016_rocketmq-cpp.log.0
      DispatchTP	    4015	34313132	         0	         3	/root/logs/rocketmq-cpp/4015_rocketmq-cpp.log.0
            lpqd	   14680	    1359	         2	         0	/usr/share/locale/locale.alias

END###################
```

## nginx_https.stap
capture https flow when service with nginx. other service's stap script need to make a change. This is diffrent way with ssldump or tcpdump and wireshark

**TODO**
1. capture ssl handshark infos
2. coordinate with goreplay to make a mirror of https follw. Also we can change it as http2 follow

curl -voa https://127.0.0.1:8443 -H "aaa.fjsdn.com" -k
```
GET / HTTP/1.1
User-Agent: curl/7.29.0
Host: 127.0.0.1:8443
Accept: */*

 1024
 ```
