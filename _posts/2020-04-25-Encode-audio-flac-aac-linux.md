---
layout: post
title: Encode audio from FLAC to AAC using fdkaac on Linux
excerpt: <!--more-->
---

Sadly, to encode from FLAC to AAC, you have the choice to use:
* QAAC (by using Wine and following [this tutorial](http://www.andrews-corner.org/qaac.html) for example)
* following this tutorial for fdkaac
* use another AAC encoder: http://wiki.hydrogenaud.io/index.php?title=AAC_encoders#Features
  * but according to [some people](https://twitter.com/kamedo2/status/1227925557309927426) `apple (QAAC) ≒ fdk-aac ＞ nero ≒ ffmpeg`

{{post.excerpt}}

It's easy:

## Extract the FLAC tracks from your videos

You need to have installed **mkvmerge** and **mkvextract** (for me, it's included in `mkvtoolnix-cli` package).

```
$ mkvmerge -i 'Your_Video.mkv' 
File 'Your_Video.mkv': container: Matroska
Track ID 0: video (MPEG-4p10/AVC/H.264)
Track ID 1: audio (FLAC)
Track ID 2: subtitles (SubStationAlpha)
Attachment ID 1: type 'application/x-truetype-font', size 4288364 bytes, file name 'KozGoPro-Bold.ttf'
Chapters: 5 entries
```
So here we need to extract the track number 1 (audio FLAC):

```
$ mkvextract tracks "Your_Video.mkv" 1:You_Video_audio.flac
```

## Then encode it!

You need to have installed **ffmpeg** and **fdkaac** packages

```
$ ffmpeg -i "You_Video_audio.flac" -acodec pcm_s24le -vn -sn -f wav - | fdkaac --bitrate-mode 5 --ignorelength -o "You_Video_audio.m4a" -
```

I use the highest quality using the highest possible value for `bitrate-mode` (which is 5)

Done!
