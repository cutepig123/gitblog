# [alpaca.cpp](https://github.com/cutepig123/gitblog/issues/6)

alpaca.cpp



这是啥：一个基于llama微调后的模型

如何本地运行？

- 下载code https://github.com/antimatter15/alpaca.cpp
- 下载模型 `Torrent: `magnet:?xt=urn:btih:053b3d54d2e77ff020ebddf51dad681f2a651071&dn=ggml-alpaca-13b-q4.bin&tr=udp%3A%2F%2Ftracker.opentrackr.org%3A1337%2Fannounce&tr=udp%3A%2F%2Fopentracker.i2p.rocks%3A6969%2Fannounce&tr=udp%3A%2F%2Ftracker.openbittorrent.com%3A6969%2Fannounce&tr=udp%3A%2F%2F9.rarbg.com%3A2810%2Fannounce``
- 编译运行

```
git clone https://github.com/antimatter15/alpaca.cpp
cd alpaca.cpp

cmake .
cmake --build . --config Release
.\Release\chat.exe
```



