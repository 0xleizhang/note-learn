

硬解 https://github.com/nyanmisaka/docker-jellyfin

docker build -t seven4d/jellyfin:arm64 .


cd /usr/lib/jellyfin-ffmpeg/
ffmpeg -hwaccels


播放到某个时间点报错：

![[jellyfin-error.png]]





转码

```
[09:56:49] [INF] [10] Jellyfin.Api.Controllers.DynamicHlsController: Current HLS implementation doesn't support non-keyframe breaks but one is requested, ignoring that request

[09:56:49] [INF] [10] Jellyfin.Api.Helpers.TranscodingJobHelper: /usr/lib/jellyfin-ffmpeg/ffmpeg -analyzeduration 200M -ss 00:25:54.000  -i file:"/mnt/sda1/movies/不_(2022)/不_(2022)_1080p_AAC.mp4" -map_metadata -1 -map_chapters -1 -threads 0 -map 0:0 -map 0:1 -map -0:s -codec:v:0 libx264 -preset veryfast -crf 23 -maxrate 4968713 -bufsize 9937426 -profile:v:0 high -level 40 -x264opts:0 subme=0:me_range=4:rc_lookahead=10:me=dia:no_chroma_me:8x8dct=0:partitions=none -force_key_frames:0 "expr:gte(t,1554+n_forced*3)" -sc_threshold:v:0 0 -vf "setparams=color_primaries=bt709:color_trc=bt709:colorspace=bt709,scale=trunc(min(max(iw\,ih*a)\,min(1920\,872*a))/2)*2:trunc(min(max(iw/a\,ih)\,min(1920/a\,872))/2)*2,format=yuv420p" -codec:a:0 copy -copyts -avoid_negative_ts disabled -max_muxing_queue_size 2048 -f hls -max_delay 5000000 -hls_time 3 -hls_segment_type mpegts -start_number 518 -hls_segment_filename "/config/transcodes/be1fc02aefb853fd374d926edec1aa44%d.ts" -hls_playlist_type vod -hls_list_size 0 -y "/config/transcodes/be1fc02aefb853fd374d926edec1aa44.m3u8"
```

```
11:23:30] [INF] [44] Jellyfin.Api.Helpers.TranscodingJobHelper: /usr/lib/jellyfin-ffmpeg/ffmpeg -analyzeduration 200M  -i file:"/mnt/sda1/movies/不_(2022)/不_(2022)_1080p_AAC.mp4" -map_metadata -1 -map_chapters -1 -threads 0 -map 0:0 -map 0:1 -map -0:s -codec:v:0 libx264 -preset veryfast -crf 23 -maxrate 4968713 -bufsize 9937426 -profile:v:0 high -level 40 -x264opts:0 subme=0:me_range=4:rc_lookahead=10:me=dia:no_chroma_me:8x8dct=0:partitions=none -force_key_frames:0 "expr:gte(t,0+n_forced*3)" -sc_threshold:v:0 0 -vf "setparams=color_primaries=bt709:color_trc=bt709:colorspace=bt709,scale=trunc(min(max(iw\,ih*a)\,min(1920\,872*a))/2)*2:trunc(min(max(iw/a\,ih)\,min(1920/a\,872))/2)*2,format=yuv420p" -codec:a:0 copy -copyts -avoid_negative_ts disabled -max_muxing_queue_size 2048 -f hls -max_delay 5000000 -hls_time 3 -hls_segment_type mpegts -start_number 0 -hls_segment_filename "/config/data/transcodes/dbfcdbd0160d837ec2db4265aafb6bae%d.ts" -hls_playlist_type vod -hls_list_size 0 -y "/config/data/transcodes/dbfcdbd0160d837ec2db4265aafb6bae.m3u8"
```


自制版本

```
[11:39:06] [INF] [7] Jellyfin.Api.Helpers.TranscodingJobHelper: /usr/lib/jellyfin-ffmpeg/ffmpeg -analyzeduration 200M -ss 00:00:12.000  -i file:"/mnt/sda1/movies/不_(2022)/不_(2022)_1080p_AAC.mp4" -map_metadata -1 -map_chapters -1 -threads 0 -map 0:0 -map 0:1 -map -0:s -codec:v:0 libx264 -preset veryfast -crf 23 -maxrate 4968713 -bufsize 9937426 -profile:v:0 high -level 40 -x264opts:0 subme=0:me_range=4:rc_lookahead=10:me=dia:no_chroma_me:8x8dct=0:partitions=none -force_key_frames:0 "expr:gte(t,12+n_forced*3)" -sc_threshold:v:0 0 -vf "setparams=color_primaries=bt709:color_trc=bt709:colorspace=bt709,scale=trunc(min(max(iw\,ih*a)\,min(1920\,872*a))/2)*2:trunc(min(max(iw/a\,ih)\,min(1920/a\,872))/2)*2,format=yuv420p" -codec:a:0 copy -copyts -avoid_negative_ts disabled -max_muxing_queue_size 2048 -f hls -max_delay 5000000 -hls_time 3 -hls_segment_type mpegts -start_number 4 -hls_segment_filename "/config/data/transcodes/44685f847acbdccd9f7b0326bb6451b9%d.ts" -hls_playlist_type vod -hls_list_size 0 -y "/config/data/transcodes/44685f847acbdccd9f7b0326bb6451b9.m3u8"
```

![[jellyfin-convert.png]]




# 硬件 未解决 求真历程


开始以为自己用的官方镜像没有驱动

用docker buildx 重新构建了https://hub.docker.com/r/nyanmisaka/jellyfin   这个镜像的arm64/v8版  ，不行

以为是启动权限问题 改了docker run 命令，不行

最后发现是ffmpeg的问题，https://github.com/jellyfin/jellyfin-ffmpeg/pull/160 
需要ffmpeg 支持R5S的CPU #[rkmpp](https://blog.csdn.net/fanyun_01/article/details/126089637)
完了用这个PR的版本build了ffmpeg 如最后PR下面留言的 及时ffmpeg支持了arm64还需要jellyfin后台要改，生成的ffmpeg命令需要带上对应的硬解参数。

这个R5用的显卡是是SOC集成在CPU中的，rockchip 瑞芯