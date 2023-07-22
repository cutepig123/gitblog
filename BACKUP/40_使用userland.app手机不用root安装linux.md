# [使用userland app手机不用root安装linux](https://github.com/cutepig123/gitblog/issues/40)

使用userland app手机不用root安装linux

目的
测试能否编译rust程序
测试性能


流程
install userland app
selet ssh to the debian environment -> wait finished -> passwd to set password
ssh to the 192.168.1.108:2022m root:your password

测试能否编译rust程序
安装rust便宜省略
cargo new
cargo run成功

性能测试

```
                          PassMark PerformanceTest Linux


Cortex-A53 (aarch64)
6 cores @ 1401 MHz  |  5.7 GiB RAM
Number of Processes: 8  |  Test Iterations: 1  |  Test Duration: Medium
--------------------------------------------------------------------------
CPU Mark:                          907
  Integer Math                     14142 Million Operations/s
  Floating Point Math              3821 Million Operations/s
  Prime Numbers                    6.2 Million Primes/s
  Sorting                          4302 Thousand Strings/s
  Encryption                       219 MB/s
  Compression                      6507 KB/s
  CPU Single Threaded              316 Million Operations/s
  Physics                          149 Frames/s
  Extended Instructions (NEON)     416 Million Matrices/s

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


Use ESC or CTRL-C to exit
A: Run All Tests   C: Run CPU Tests   M: Run Memory Tests   U: Upload Test Results
```

性能差了些，本来1900现在成900了


---

NAS内部的linux虚拟机

```
                          PassMark PerformanceTest Linux


Westmere E56xx/L56xx/X56xx (Nehalem-C) (x86_64)
1 cores @ 1996 MHz  |  1.9 GiB RAM
Number of Processes: 1  |  Test Iterations: 1  |  Test Duration: Medium
--------------------------------------------------------------------------
CPU Mark:                          270
  Integer Math                     1479 Million Operations/s
  Floating Point Math              400 Million Operations/s
  Prime Numbers                    0.7 Million Primes/s
  Sorting                          488 Thousand Strings/s
  Encryption                       104 MB/s
  Compression                      4230 KB/s
  CPU Single Threaded              308 Million Operations/s
  Physics                          21.8 Frames/s
  Extended Instructions (SSE)      128 Million Matrices/s

Memory Mark:                       286
  Database Operations              79.5 Thousand Operations/s
  Memory Read Cached               3002 MB/s
  Memory Read Uncached             2017 MB/s
  Memory Write                     1934 MB/s
  Available RAM                    655 Megabytes
  Memory Latency                   173 Nanoseconds
  Memory Threaded                  2318 MB/s
--------------------------------------------------------------------------

Results not submitted
Upload results to cpubenchmark.net? [Y/n]:

Use ESC or CTRL-C to exit
A: Run All Tests   C: Run CPU Tests   M: Run Memory Tests   U: Upload Test Results
```

NAS主机

```
                         PassMark PerformanceTest Linux


 ()
1 cores @ 0 MHz  |  9.6 GiB RAM
Number of Processes: 2  |  Test Iterations: 1  |  Test Duration: Medium
--------------------------------------------------------------------------
CPU Mark:                          893
  Integer Math                     4160 Million Operations/s
  Floating Point Math              1070 Million Operations/s
  Prime Numbers                    2.7 Million Primes/s
  Sorting                          1616 Thousand Strings/s
  Encryption                       589 MB/s
  Compression                      13614 KB/s
  CPU Single Threaded              809 Million Operations/s
  Physics                          71.6 Frames/s
  Extended Instructions (SSE)      360 Million Matrices/s

Memory Mark:                       771
  Database Operations              300 Thousand Operations/s
  Memory Read Cached               5976 MB/s
  Memory Read Uncached             4464 MB/s
  Memory Write                     4209 MB/s
  Available RAM                    3161 Megabytes
  Memory Latency                   74 Nanoseconds
  Memory Threaded                  6577 MB/s
--------------------------------------------------------------------------

Results submission disabled
Unable to get CPU model, upload disabled

Use ESC or CTRL-C to exit
A: Run All Tests   C: Run CPU Tests   M: Run Memory Tests   U: Upload Test Results
```
