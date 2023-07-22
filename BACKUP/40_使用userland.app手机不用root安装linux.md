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
