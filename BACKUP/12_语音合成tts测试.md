# [语音合成tts测试](https://github.com/cutepig123/gitblog/issues/12)

语音合成tts测试

微软的edge tts

```bash
# https://pypi.org/project/edge-tts/
pip install edge-tts
path %path%;F:\Users\cutepig\Downloads\mpv-x86_64-20230402-git-0f13c38

edge-tts --text "Hello, world!" --write-media hello.mp3
edge-playback --text "Hello, world!"
edge-playback --text "你是谁 hello work" --voice zh-TW-HsiaoYuNeural
edge-playback -f 1.txt --voice zh-TW-HsiaoYuNeural

# 实时输出，而不是通过中间文件
F:\>edge-tts -f 1.txt --voice zh-TW-HsiaoYuNeural | mpv -
[file] Reading from stdin...
 (+) Audio --aid=1 (mp3 1ch 24000Hz)
AO: [wasapi] 48000Hz stereo 2ch float
A: 00:00:03 / 00:00:04 (74%)

```

