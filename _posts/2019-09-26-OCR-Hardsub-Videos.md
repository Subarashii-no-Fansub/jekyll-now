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

You can follow the [README of YoloCR](https://bitbucket.org/YuriZero/yolocr/src/c013e6b74804251a253d00d820b4de668848f13f/README_EN.md?at=master#markdown-header-how-to-use) but here a short version of the README:

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

### Use the legacy version of Tesseract instead of the LSTM motor

Since the new tesseract version 4.0, LSTM is the new motor. It's generally more accurate in the OCR, but it's loooonger than the old motor.<br>
To use the legacy motor, simply download thieses traineddata from [here](https://github.com/tesseract-ocr/tessdata/) and save it in the folder `/usr/share/tesseract/tessdata` under the name `<lang>-legacy.traineddata`.

When using YoloCR, simply launch it in this way: `./YoloCR.sh Filetered_video.mp4 <lang>-legacy` instead of `./YoloCR.sh Filetered_video.mp4 <lang>` (else it'll use LSTM).

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
