
##### 前言

本demo是使用的mp4v2来将h264、aac封装成mp4文件的，目前demo提供的.a静态库文件是在x86_64架构的Ubuntu16.04编译得到的，如果想在其他环境下测试demo，可以自行编译mp4v2并替换相应的库文件（libmp4v2.a）。

注：目前生成的mp4文件能在potplayer、vlc上播放了，但个别播放器未能正常播放（没有声音），还需定位问题，问题解决后会在这里补充相应说明。


###  1. 编译

```bash
$ make
```

如果想编译mp4v2，则可以参考以下步骤：

```bash
$ tar xjf mp4v2-2.0.0.tar.bz2
$ cd mp4v2-2.0.0/
$ ./configure --prefix=$PWD/_install # 交叉编译可参考加上选项: --host=arm-linux-gnueabihf
$ make -j96
$ make install
```


### 2. 使用

注：示例2中的音视频测试文件是不同步的，所以封装得到的mp4文件音视频不同步是正常现象。

```bash
$ ./mp4v2_demo
(Note: Only support H.264 and AAC(LC) in this demo.)
examples:
    ./mp4v2_demo -h
    ./mp4v2_demo --help
    ./mp4v2_demo -a ./avfile/test1_44100_stereo.aac -r 44100 -c 2 -v ./avfile/test1_856x480_24fps.h264 -W 856 -H 480 -f 24 -o ./test1_out.mp4
    ./mp4v2_demo --audio_file=./avfile/test2_44100_mono.aac --audio_samplerate=44100 --audio_channels=1 --video_file=./avfile/test2_960x544_25fps.h264 --video_width=960 --video_height=544 --video_fps=25 --output_mp4=./test2_out.mp4
```


### 附录（demo目录结构）

```
.
├── avfile
│   ├── test1_44100_stereo.aac
│   ├── test1_856x480_24fps.h264
│   ├── test1_out.mp4
│   ├── test2_44100_mono.aac
│   ├── test2_960x544_25fps.h264
│   └── test2_out.mp4
├── docs
│   ├── mp4文件格式解析 - 简书.mhtml
│   ├── MP4格式详解_DONGHONGBAI的专栏-CSDN博客.mhtml
│   ├── 从零开始写一个RTSP服务器（5）RTP传输AAC_JT同学的博客-CSDN博客.mhtml
│   ├── 使用mp4v2封装H.264成mp4最简单示例_JT同学的博客-CSDN博客_mp4v2.mhtml
│   ├── 使用mp4v2封装mp4_LiaoJunXiong的博客-CSDN博客.mhtml
│   └── 使用mp4v2将H264+AAC合成mp4文件 - 楚 - 博客园.mhtml
├── include
│   └── mp4v2
│       ├── chapter.h
│       ├── file.h
│       ├── file_prop.h
│       ├── general.h
│       ├── isma.h
│       ├── itmf_generic.h
│       ├── itmf_tags.h
│       ├── mp4v2.h
│       ├── platform.h
│       ├── project.h
│       ├── sample.h
│       ├── streaming.h
│       ├── track.h
│       └── track_prop.h
├── lib
│   └── libmp4v2.a
├── main.c
├── Makefile
└── README.md
```

