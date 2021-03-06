# [流媒体协议](https://cloud.tencent.com/developer/article/1174457)

## SDP: Session Description Protocol(会话描述协议)

SDP也是MMUSIC工作组的一个产品,在MBONE内容中用得很多。其目的就是在媒体会话中，传递媒体流信息，允许会话描述的接收者去参与会话。 SDP基本上在internet上工作。他定义了会话描述的统一格式,但并不定义多播地址的分配和SDP消息的传输,也不支持媒体编码方案的协商,这些功 能均由下层传送协议完成.典型的会话传送协议包括:SAP(Session Announcement Protocol 会话公告协议),SIP,RTSP,HTTP,和使用MIME的E-Mail.(注意:对SAP只能包含一个会话描述,其它会话传诵协议的SDP可包含多 个会话描述)

SDP包括以下一些方面：

1. 会话的名称和目的
2. 会话存活时间
3. 包含在会话中的媒体信息，包括：
   - 媒体类型(video, audio, etc)
   - 传输协议(RTP/UDP/IP, H.320, etc)
   - 媒体格式(H.264 video, MPEG video, etc)
   - 多播或远端（单播）地址和端口
4. 为接收媒体而需的信息(addresses, ports, formats and so on)
5. 使用的带宽信息
6. 可信赖的接洽信息（Contact information）

## 协议

- [协议解析](https://blog.csdn.net/machh/article/details/51873690)

```c
v=0
o=64010000002020000001 0 0 IN IP4 192.168.1.102
s=Play
c=IN IN4 192.168.1.102
t=0 0
m=video 6000 RTP/AVP 96 98 97
a=rtpmap:96 PS/90000
a=rtpmap:98 H264/90000
a=rtpmap:97 MPEG4/90000
a=recvonly
```

- 会话描叙格式介绍
  - 协议版本： v=0 给出sdp的版本号，目前为0版本，无子版本号
  - 会话源: o=(用户名)（会话标识）（版本）（网络类型）（地址类型）（地址）
    - 如果不存在用户登录名，该字段标志位“-”
    - 会话标识为一随机数字串
    - 版本为该会话公告的版本
    - 网络类型为文本串，“IN”表示internet
    - 地址类型为文本串，目前定义为“IP4”和“IP6”两种地址
  - 会话名： s=(会话名) 每个会话描述必须只有一个会话名
    - “Play”代表实时点播；“Playback”代表历史回放；“Download”代表文件下载；“Talk”代表语音对讲。
  - 会话信息： i=(会话信息) 此字段并非必须，建议包括进来用于描叙相应会话文字性说明，每个会话描叙最多只能有一个
  - URL: u=(URL) 此字段并非必须,提供url的描叙信息
  - 连接数据： c=(网络类型)（地址类型）（连接地址）
- 时间描述
  - t = （会话活动时间）
  - r = * （0或多次重复次数）
- 媒体描述
  - m=(媒体)（端口）（传送层）（格式列表）
    - 媒体类型：音频（audio）,视频(video),应用，数据和控制
    - 端口：媒体传送层端口
    - 传送层：ip4上大多基于rtp/udp上传送（RTP/AVP）IETF RTP协议，在udp上传输
    - 格式列表： 对应对应的音频负载类型（PT）
    - s为Play、媒体为audio时表示语音对讲。
  - i = * （媒体标题）
  - c = * （连接信息 — 如果包含在会话层则该字段可选）
  - b = * （带宽信息）
  - k = * （加密密钥）
  - a = * （0 个或多个会话属性行）
    - a=rtpmap:（净荷类型）（编码名）/（时钟速率）[/(编码参数)]
    - a=sendonly     //说明本端媒体流的方向，取值包括sendonly/recvonly/sendrecv/inactive
      - 如果请求某媒体流的方向为sendonly，那么响应中对应媒体的方向必须为recvonly；
      - 如果请求某媒体流的方向为recvonly，那么响应中对应媒体的方向必须为sendonly；
      - 如果请求某媒体流的方向为sendrecv，那么响应中对应媒体的方向可以为sendrecv/sendonly/recvonly/inactive中的一种；
      - 如果请求某媒体流的方向为inactive，那么响应中对应媒体的方向必须为inactive；

## PS 流

PS--Program Stream(节目流)PS流由PS包组成，而一个PS包又由若干个PES包组成（到这里，ES经过了两层的封装）。PS包的包头中包含了同步信息与时钟恢复信息。一个PS包最多可包含具有同一时钟基准的16个视频PES包和32个音频PES包。

## PES

PES--Packetized  Elementary Streams  (分组的ES)，ES形成的分组称为PES分组，是用来传递ES的一种数据结构。PES流是ES流经过PES打包器处理后形成的数据流，在这个过程中完成了将ES流分组、打包、加入包头信息等操作（对ES流的第一次打包）。PES流的基本单位是PES包。PES包由包头和payload组成。

## 名词解释

- `npt`:(`Normal Play Time--正常播放时间`)播放位置离文件开始部分的相对时间
