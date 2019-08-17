---
layout: post
title: OCR Hardsub Videos
excerpt: <!--more-->
---

I'll explain you how to easily OCR videos.

{{post.excerpt}}

For that, I'll use:
 * [YoloCR](https://bitbucket.org/YuriZero/yolocr)
   * that uses `FFmpeg`, `Vapoursynth` (and some plugins), `Vapoursynth Editor`, `Tesseract`
 * [Sushi](https://github.com/tp7/Sushi)
   * that uses `MkvExtract`

## OCR the video

You can follow the [README of YoloCR](https://bitbucket.org/YuriZero/yolocr/src/88fd5422aa35610d8b68ecbe18a583260e24d32d/README_EN.md?fileviewer=file-view-default#markdown-header-how-to-use) but to be a short version of the README:

 - Open the `YoloCR.vpy` file and edit:
   - **FichierSource** for the source file to OCR
   - **DimensionCropBox** that is the dimension of the cropbox to limit the zone to OCR
   - **HauteurCropBox** that is the height of the cropbox
   - **HauteurCropBoxAlt**, use it if some text is on the top of the video
   - **SeuilI**
   - **SeuilO**

The CropBox dimension and height is important, and SeuilI/SeuilO are the most important part of how will be the OCR result.
Here some help:
 - SeuilI > SeuilO
 - *generally*, SeuilI is between 170 and 230, and SeuilO is between 20 and 120
 - SeuilI represent the **maximum** value you put to have a subtitle correctly visible
 - SeuilO represent the **minimum** value you put to have a subtitle correctly visible

## Time the video

As sometimes the video to OCR is not timed at the same time than your destination video (because of for example the presence of an introduction), we're going to use [Sushi](https://github.com/tp7/Sushi).

To install it, visit [the Github Sushi](https://github.com/tp7/Sushi/blob/master/README.md#requirements).

Here the command line for automatic retiming:

```
$ python2 sushi.py --src [OCRedVideo].mp4 --src-audio 1 --dst "[DestinationVideo].mkv" --dst-audio 1 --script [Subtitle].srt
```
Replace the value:
 + `--src [OCRedVideo].mp4`: the video you've just OCRed
 + `--src-audio 1`: The audio pist number of [OCRedVideo].mp4, using `mkvmerge -i` to guess it
 + `--dst [DestinationVideo].mkv`: the destination video, where subtitle will be mux
 + `--dst-audio 1`: same than `--src-audio 1` but for [DestinationVideo].mkv
 + `--script [Subtitle].srt`: your subtitle file
