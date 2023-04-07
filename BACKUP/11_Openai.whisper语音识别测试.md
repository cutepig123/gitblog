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



TODO

- [ ] 跑的太慢了，测一下https://github.com/ggerganov/whisper.cpp
- [ ] 除了语音识别，还有啥local的语音生成的tts lib？或者能免费用微软的tts也行
- [ ] 如何支持语音直接输入，而不是文件输入

---

在我的电脑跑的太慢了