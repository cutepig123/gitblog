# [shadowsocks](https://github.com/cutepig123/gitblog/issues/36)

```

 2332  cargo install shadowsocks-rust
 2333  wget https://github.com/shadowsocks/shadowsocks-rust/releases/download/v1.15.3/shadowsocks-v1.15.3.x86_64-unknown-linux-gnu.tar.xz
 2334  ls shadowsocks-v1.15.3.x86_64-unknown-linux-gnu.tar.xz
 2335  tar xvzf  shadowsocks-v1.15.3.x86_64-unknown-linux-gnu.tar.xz
 2336  tar -xf  shadowsocks-v1.15.3.x86_64-unknown-linux-gnu.tar.xz
 2337  ls
 2338  ls sha*
 2339  tar -xf  shadowsocks-v1.15.3.x86_64-unknown-linux-gnu.tar.xz
 2340  ./sslocal
 2341  ./ssservice
 2342  ./ssservice server
 2343  nano ssocks.cfg
 2344  nano ssocks.json
 2345  ./ssservice server -c ssocks.json
 2346  ./sserver -c ssocks.json
 2347  ./ssserver -c ssocks.json
 2348  nano ssocks.json
 2349  ./ssserver -c ssocks.json
 2350  ./ssservice server -c ssocks.json
➜  ~ ls ss*
sslocal  ssmanager  ssocks.json  ssserver  ssservice  ssurl
➜  ~ cat ssocks.json
{
    "server":"0.0.0.0",
    "server_port":8388,
    "local_port":1080,
    "password":"barfoo!",
    "method":"chacha20-ietf-poly1305"
}

```