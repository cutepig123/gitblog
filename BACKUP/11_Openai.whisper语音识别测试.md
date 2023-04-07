# [Openai whisper语音识别测试](https://github.com/cutepig123/gitblog/issues/11)

Openai whisper语音识别测试



```
pip install git+https://github.com/openai/whisper.git 
path %path%;F:\sw\ffmpeg-4.1.4-win64-static\bin

whisper \\192.168.1.124\MyShare\podsync\stone\_apS6CxV_e0.mp3 --language Chinese --model medium
```

下载的Model在这里

```
C:\WINDOWS\system32>dir C:\Users\cutepig\.cache\whisper
 Volume in drive C is ssd
 Volume Serial Number is EB71-E2FB

 Directory of C:\Users\cutepig\.cache\whisper

2023/04/07  21:31    <DIR>          .
2023/04/07  21:31    <DIR>          ..
2023/04/07  21:23     1,528,008,539 medium.pt
2023/04/07  21:31       483,617,219 small.pt
               2 File(s)  2,011,625,758 bytes
               2 Dir(s)  53,389,697,024 bytes free
```

测试

```
C:\Users\cutepig>whisper \\192.168.1.124\MyShare\podsync\stone\_apS6CxV_e0.mp3 --language Chinese
f:\users\cutepig\appdata\local\programs\python\python38\lib\site-packages\whisper\transcribe.py:114: UserWarning: FP16 is not supported on CPU; using FP32 instead
  warnings.warn("FP16 is not supported on CPU; using FP32 instead")
[00:00.000 --> 00:02.560] 大家好 今天是2020年的3月1号星期日
[00:02.560 --> 00:04.160] 9天前我们报了一个消息
[00:04.160 --> 00:06.320] 说美国和塔利班要签署和平前议
[00:06.320 --> 00:07.200] 但是要等9天
[00:07.200 --> 00:10.240] 要看塔利班那边能不能控制他们下巴的恐怖分子
[00:10.240 --> 00:11.840] 9天过去了 控制得还不错
[00:11.840 --> 00:12.800] 听伙搞得还挺好
[00:12.800 --> 00:13.760] 美国也比较满意
[00:13.760 --> 00:18.800] 美国国务卿蓬佩奥已经从华盛顿争飞机抵达了卡塔尔的首都
[00:18.800 --> 00:20.480] 现在协议应该已经签完了
[00:20.480 --> 00:21.200] 因为到3月1号了
[00:21.200 --> 00:22.240] 协议应该已经签完了
[00:22.240 --> 00:25.040] 结束了美国在阿富汗的18年的战争
[00:25.040 --> 00:28.320] 那么从2001年的9月11号1911之后
```


测试whisper.cpp，失败

```bash
cutepig@DESKTOP-CM4NK5L MINGW64 ~
$ cd /F/_codes/whisper.cpp

cutepig@DESKTOP-CM4NK5L MINGW64 /F/_codes/whisper.cpp
#下载模型
$ bash ./models/download-ggml-model.sh base.en
Downloading ggml model base.en from 'https://huggingface.co/ggerganov/whisper.cpp' ...
ggml-base.en.bin         100%[==================================>] 141.11M  9.55MB/s    in 13s
Done! Model 'base.en' saved in 'models/ggml-base.en.bin'
You can now use it like this:

  $ ./main -m models/ggml-base.en.bin -f samples/jfk.wav


cutepig@DESKTOP-CM4NK5L MINGW64 /F/_codes/whisper.cpp
# 编译代码
$ make
I whisper.cpp build info:
I UNAME_S:  MINGW64_NT-10.0-19044
I UNAME_P:  unknown
I UNAME_M:  x86_64
I CFLAGS:   -I.              -O3 -DNDEBUG -std=c11   -fPIC -mfma -mf16c -mavx -mavx2
I CXXFLAGS: -I. -I./examples -O3 -DNDEBUG -std=c++11 -fPIC
I LDFLAGS:
I CC:       cc (GCC) 11.3.0
I CXX:      g++ (GCC) 11.3.0

cc  -I.              -O3 -DNDEBUG -std=c11   -fPIC -mfma -mf16c -mavx -mavx2   -c ggml.c -o ggml.o
g++ -I. -I./examples -O3 -DNDEBUG -std=c++11 -fPIC -c whisper.cpp -o whisper.o
whisper.cpp: In function ‘void dft(const std::vector<float>&, std::vector<float>&)’:
whisper.cpp:2200:29: error: ‘M_PI’ was not declared in this scope
 2200 |             float angle = 2*M_PI*k*n/N;
      |                             ^~~~
whisper.cpp: In function ‘void fft(const std::vector<float>&, std::vector<float>&)’:
whisper.cpp:2251:25: error: ‘M_PI’ was not declared in this scope
 2251 |         float theta = 2*M_PI*k/N;
      |                         ^~~~
whisper.cpp: In function ‘bool log_mel_spectrogram(whisper_state&, const float*, int, int, int, int, int, int, const whisper_filters&, bool, whisper_mel&)’:
whisper.cpp:2286:39: error: ‘M_PI’ was not declared in this scope
 2286 |         hann[i] = 0.5*(1.0 - cos((2.0*M_PI*i)/(fft_size)));
      |                                       ^~~~
make: *** [Makefile:194: whisper.o] Error 1

cutepig@DESKTOP-CM4NK5L MINGW64 /F/_codes/whisper.cpp
$ code .
-bash: code: command not found

cutepig@DESKTOP-CM4NK5L MINGW64 /F/_codes/whisper.cpp
$ code .
-bash: code: command not found

cutepig@DESKTOP-CM4NK5L MINGW64 /F/_codes/whisper.cpp
$ make
I whisper.cpp build info:
I UNAME_S:  MINGW64_NT-10.0-19044
I UNAME_P:  unknown
I UNAME_M:  x86_64
I CFLAGS:   -I.              -O3 -DNDEBUG -std=c11   -fPIC -mfma -mf16c -mavx -mavx2
I CXXFLAGS: -I. -I./examples -O3 -DNDEBUG -std=c++11 -fPIC
I LDFLAGS:
I CC:       cc (GCC) 11.3.0
I CXX:      g++ (GCC) 11.3.0

g++ -I. -I./examples -O3 -DNDEBUG -std=c++11 -fPIC -c whisper.cpp -o whisper.o
g++ -I. -I./examples -O3 -DNDEBUG -std=c++11 -fPIC examples/main/main.cpp examples/common.cpp ggml.o whisper.o -o main
./main -h

usage: ./main [options] file0.wav file1.wav ...

options:
  -h,        --help              [default] show this help message and exit
  -t N,      --threads N         [4      ] number of threads to use during computation
  -p N,      --processors N      [1      ] number of processors to use during computation
  -ot N,     --offset-t N        [0      ] time offset in milliseconds
  -on N,     --offset-n N        [0      ] segment index offset
  -d  N,     --duration N        [0      ] duration of audio to process in milliseconds
  -mc N,     --max-context N     [-1     ] maximum number of text context tokens to store
  -ml N,     --max-len N         [0      ] maximum segment length in characters
  -sow,      --split-on-word     [false  ] split on word rather than on token
  -bo N,     --best-of N         [5      ] number of best candidates to keep
  -bs N,     --beam-size N       [-1     ] beam size for beam search
  -wt N,     --word-thold N      [0.01   ] word timestamp probability threshold
  -et N,     --entropy-thold N   [2.40   ] entropy threshold for decoder fail
  -lpt N,    --logprob-thold N   [-1.00  ] log probability threshold for decoder fail
  -su,       --speed-up          [false  ] speed up audio by x2 (reduced accuracy)
  -tr,       --translate         [false  ] translate from source language to english
  -di,       --diarize           [false  ] stereo audio diarization
  -nf,       --no-fallback       [false  ] do not use temperature fallback while decoding
  -otxt,     --output-txt        [false  ] output result in a text file
  -ovtt,     --output-vtt        [false  ] output result in a vtt file
  -osrt,     --output-srt        [false  ] output result in a srt file
  -owts,     --output-words      [false  ] output script for generating karaoke video
  -fp,       --font-path         [/System/Library/Fonts/Supplemental/Courier New Bold.ttf] path to a monospace font for karaoke video
  -ocsv,     --output-csv        [false  ] output result in a CSV file
  -oj,       --output-json       [false  ] output result in a JSON file
  -of FNAME, --output-file FNAME [       ] output file path (without file extension)
  -ps,       --print-special     [false  ] print special tokens
  -pc,       --print-colors      [false  ] print colors
  -pp,       --print-progress    [false  ] print progress
  -nt,       --no-timestamps     [true   ] do not print timestamps
  -l LANG,   --language LANG     [en     ] spoken language ('auto' for auto-detect)
             --prompt PROMPT     [       ] initial prompt
  -m FNAME,  --model FNAME       [models/ggml-base.en.bin] model path
  -f FNAME,  --file FNAME        [       ] input WAV file path

g++ -I. -I./examples -O3 -DNDEBUG -std=c++11 -fPIC examples/bench/bench.cpp ggml.o whisper.o -o bench

#执行测试，失败
cutepig@DESKTOP-CM4NK5L MINGW64 /F/_codes/whisper.cpp
$ ./main -f samples/jfk.wav
whisper_init_from_file_no_state: loading model from 'models/ggml-base.en.bin'
whisper_model_load: loading model
whisper_model_load: n_vocab       = 51864
whisper_model_load: n_audio_ctx   = 1500
whisper_model_load: n_audio_state = 512
whisper_model_load: n_audio_head  = 8
whisper_model_load: n_audio_layer = 6
whisper_model_load: n_text_ctx    = 448
whisper_model_load: n_text_state  = 512
whisper_model_load: n_text_head   = 8
whisper_model_load: n_text_layer  = 6
whisper_model_load: n_mels        = 80
whisper_model_load: f16           = 1
whisper_model_load: type          = 2
whisper_model_load: mem required  =  218.00 MB (+    6.00 MB per decoder)
whisper_model_load: adding 1607 extra tokens
whisper_model_load: model ctx     =  140.60 MB
Illegal instruction (core dumped)

cutepig@DESKTOP-CM4NK5L MINGW64 /F/_codes/whisper.cpp

```



TODO

- [x ] 跑的太慢了，测一下https://github.com/ggerganov/whisper.cpp
- [ x] 除了语音识别，还有啥local的语音生成的tts lib？或者能免费用微软的tts也行
- [ ] 如何支持语音直接输入，而不是文件输入

---

在我的电脑跑的太慢了