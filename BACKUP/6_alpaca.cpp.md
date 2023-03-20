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

E:\>F:\_codes\alpaca.cpp\build\debug\chat.exe
main: seed = 1679276051
llama_model_load: loading model from 'ggml-alpaca-7b-q4.bin' - please wait ...
llama_model_load: ggml ctx size = 6065.34 MB
llama_model_load: memory_size =  2048.00 MB, n_mem = 65536
llama_model_load: loading model part 1/1 from 'ggml-alpaca-7b-q4.bin'
llama_model_load: ....... done
llama_model_load: model size =   842.06 MB / num tensors = 59

system_info: n_threads = 4 / 4 | AVX = 1 | AVX2 = 1 | AVX512 = 0 | FMA = 0 | NEON = 0 | ARM_FMA = 0 | F16C = 0 | FP16_VA = 0 | WASM_SIMD = 0 | BLAS = 0 | SSE3 = 0 | VSX = 0 |
main: interactive mode on.
sampling parameters: temp = 0.100000, top_k = 40, top_p = 0.950000, repeat_last_n = 64, repeat_penalty = 1.300000

```



