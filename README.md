# ijkrtspdemo
ijkplayer open the rtsp &amp; h265 surpport android demo . 


### 引入项目调用
## 1. 引入私有库地址.
```groovy
allprojects {
    repositories {
        maven {
            url "https://dl.bintray.com/media/maven"
        }
        google()
        jcenter()
    }
}
```

## 2. 在主项目中build.gradle引入以下库
```groovy
    implementation 'com.github.jdpxiaoming:ijkplayerview:0.0.6'
    implementation 'com.github.jdpxiaoming:ijkplayer-java:0.0.5'
    implementation 'com.github.jdpxiaoming:ijkplayer-armv7a:0.0.5'
    //看情况如果需要64位so则引入.
    implementation 'com.github.jdpxiaoming:ijkplayer-arm64:0.0.5'
```

### 根据播放地址类型设置不同的类型 .
```java
    public static final int IJK_TYPE_LIVING_WATCH = 1; //实时监控，要求首开速度,延迟略高一点
    public static final int IJK_TYPE_LIVING_LOW_DELAY = 2; //实时直播要求低延迟，不要求首开熟读 .
    public static final int IJK_TYPE_HTTP_PLAY = 3;//录播 mp4 /hls/flv...
    public static final int IJK_TYPE_FILE_PLAY = 10;//本地文件播放 .
    public static final int IJK_TYPE_PLAY_DEFAULT = IJK_TYPE_LIVING_WATCH;//默认播放类型.
```

- example 点播
```java
 mVideoView.setVideoPath(mVideoPath, IjkVideoView.IJK_TYPE_HTTP_PLAY);
```



# 编译了[ijk0.8.8](https://github.com/bilibili/ijkplayer)
打开了rtsp的开关

```
#rtsp支持. 
export COMMON_FF_CFG_FLAGS="$COMMON_FF_CFG_FLAGS --enable-demuxer=rtsp"
export COMMON_FF_CFG_FLAGS="$COMMON_FF_CFG_FLAGS --enable-demuxer=mjpeg"
export COMMON_FF_CFG_FLAGS="$COMMON_FF_CFG_FLAGS --enable-demuxer=sdp"
export COMMON_FF_CFG_FLAGS="$COMMON_FF_CFG_FLAGS --enable-demuxer=rtp"

export COMMON_FF_CFG_FLAGS="$COMMON_FF_CFG_FLAGS --enable-decoder=mjpeg"
export COMMON_FF_CFG_FLAGS="$COMMON_FF_CFG_FLAGS --enable-protocol=rtp"
export COMMON_FF_CFG_FLAGS="$COMMON_FF_CFG_FLAGS --enable-protocol=tcp"
```

# 运行demo
> 直接运行ijkplayer-example即可。

# 我编译时选择了target-25 
> 所以你的targetAPI <= 25 最好，如果有高版本需求请自行编译. 

# rtsp首开速度优化 
>配置1. 速度首开50
```配置1. 速度首开50
IJKMEDIA: ===== options =====
IJKMEDIA: player-opts : opensles                     = 1
IJKMEDIA: player-opts : overlay-format               = 842225234
IJKMEDIA: player-opts : mediacodec                   = 1
IJKMEDIA: player-opts : mediacodec-hevc              = 1
IJKMEDIA: player-opts : packet-buffering             = 0
IJKMEDIA: player-opts : fast                         = 1
IJKMEDIA: player-opts : mediacodec-handle-resolution-change = 0
IJKMEDIA: player-opts : framedrop                    = 1
IJKMEDIA: player-opts : start-on-prepared            = 1
IJKMEDIA: player-opts : reconnect                    = 5
IJKMEDIA: format-opts : ijkapplication               = -1284518032
IJKMEDIA: format-opts : ijkiomanager                 = -1414032000
IJKMEDIA: format-opts : rtsp_transport               = tcp
IJKMEDIA: format-opts : rtsp_flags                   = prefer_tcp
IJKMEDIA: format-opts : http-detect-range-support    = 1
IJKMEDIA: format-opts : buffer_size                  = 1316
IJKMEDIA: format-opts : max-buffer-size              = 0
IJKMEDIA: format-opts : infbuf                       = 1
IJKMEDIA: format-opts : analyzemaxduration           = 100
IJKMEDIA: format-opts : probesize                    = 1024
IJKMEDIA: format-opts : flush_packets                = 1
IJKMEDIA: codec-opts  : skip_loop_filter             = 48
IJKMEDIA: ===================
```
>配置2. 首开速度20左右
```
===== options =====
SDL_RunThread: [30113] ff_msg_loop
player-opts : opensles                     = 1
player-opts : overlay-format               = 842225234
message_loop
player-opts : mediacodec                   = 1
player-opts : mediacodec-hevc              = 1
player-opts : packet-buffering             = 0
player-opts : fast                         = 1
player-opts : mediacodec-handle-resolution-change = 0
player-opts : framedrop                    = 1
player-opts : start-on-prepared            = 1
player-opts : reconnect                    = 5
format-opts : ijkapplication               = -1351159456
format-opts : ijkiomanager                 = -1078774656
format-opts : rtsp_transport               = tcp
format-opts : rtsp_flags                   = prefer_tcp
format-opts : http-detect-range-support    = 1
format-opts : buffer_size                  = 1024
format-opts : max-buffer-size              = 0
format-opts : max-fps                      = 20
format-opts : infbuf                       = 1
format-opts : analyzemaxduration           = 80
format-opts : probesize                    = 800
format-opts : flush_packets                = 1
codec-opts  : skip_loop_filter             = 48
===================
```
