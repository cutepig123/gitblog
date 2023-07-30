# [oracle could的免费cpu性能差了点，但是好在永久免费](https://github.com/cutepig123/gitblog/issues/42)

### PassMark 

```
                          PassMark PerformanceTest Linux


Neoverse-N1 (aarch64)
1 cores @ 0 MHz  |  5.5 GiB RAM
Number of Processes: 1  |  Test Iterations: 1  |  Test Duration: Medium
--------------------------------------------------------------------------
CPU Mark:                          739
  Integer Math                     4504 Million Operations/s
  Floating Point Math              3426 Million Operations/s
  Prime Numbers                    8.7 Million Primes/s
  Sorting                          2859 Thousand Strings/s
  Encryption                       149 MB/s
  Compression                      4549 KB/s
  CPU Single Threaded              1151 Million Operations/s
  Physics                          183 Frames/s
  Extended Instructions (NEON)     710 Million Matrices/s

Memory Mark:                       Incomplete
  Database Operations              0.0 Thousand Operations/s
  Memory Read Cached               0.0 MB/s
  Memory Read Uncached             0.0 MB/s
  Memory Write                     0.0 MB/s
  Available RAM                    0 Megabytes
  Memory Latency                   0 Nanoseconds
  Memory Threaded                  0.0 MB/s
--------------------------------------------------------------------------

Results not submitted


```

### 如何申请

https://www.oracle.com/hk/cloud/free/

如何设置

如何ssh连接

### 其他厂商的免费产品

https://github.com/cloudcommunity/Cloud-Free-Tier-Comparison

###  oracle cloud TCP public port setting

1. cloud web site setting, ref https://dev.to/armiedema/opening-up-port-80-and-443-for-oracle-cloud-servers-j35
2. iptable setting

[opc@instance-20230730-2144 ~]$ sudo firewall-cmd --add-port=8000/tcp --permanent
success
[opc@instance-20230730-2144 ~]$ sudo firewall-cmd --reload
success

test it
[opc@instance-20230730-2144 ~]$ python -m http.server

### orcale cloud check balance
