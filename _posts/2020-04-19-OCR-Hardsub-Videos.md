---
layout: post
title: OCR Hardsub Videos
excerpt: <!--more-->
---

I'll explain you how to easily OCR videos.

{{post.excerpt}}

For that, I'll use:
 * [YoloCR](https://git.clapity.eu/Id/YoloCR)
   * that uses `FFmpeg`, `Vapoursynth` (and some plugins), `Vapoursynth Editor`, `Tesseract`
 * [Sushi](https://github.com/tp7/Sushi)
   * that uses `MkvExtract`

## OCR the video

You can follow the [README of YoloCR](https://git.clapity.eu/Id/YoloCR/src/e1b7a03d2c1bcc1adbbc8dd280eed5392553fe11/README_EN.md) but here a short version of the README:

### `YoloResize.py` script

Open the `YoloResize.vpy` file and edit:
  - **FichierSource** for the source file to OCR
  - **DimensionCropBox** that is the dimension of the cropbox to limit the zone to OCR
  - **HauteurCropBox** that is the height of the cropbox

The goal here is to identify the text cropbox by modifying the **DimensionCropBox** value, and by checking the previewing of the video.<br>
You can have one (at the bottom) or two (at the top and bottom of the video).<br>
In the second case, you'll have to do the operation twice.

Once your hardsub text is located in your **DimensionCropBox**, report the value to `YoloSeuil.vpy` script.

> if you have this kind of error: `Python exception: Crop: cropped area needs to have mod 2 height offset`, then check that the two numbers of your **DimensionCropBox** are multiples of two.

### `YoloSeuil.vpy` script

That's the most useful script, and the one who helps you a lot.

Open the `YoloSeuil.vpy` file and:
  - copy from `YoloResize.py`: **FichierSource**, **DimensionCropBox**, **HauteurCropBox**, **HauteurCropBoxAlt** (in case of some text in top of the video)
   - **Seuil**: try to find it with the vapoursynth preview (when equal to `-1`). Do not hesitate to change it to the value you've found to check if it's correct and subs are still visible.

These is two modes:
 - Luma mode: the most common, or when occuring OCR on subtitle in outline black and inline white (**ModeS='L'**)
 - RGB mode: useful when OCR older hard and fan subs video (eg when text is in blue) (3 sets of values are mandatory, **ModeS='R'**, **ModeS='B'**, **ModeS='G'**)

When doing Luma mode, only two values of **Seuil** are mandatory: the min and max value (used for **SeuilI** and **SeuilO** in `YoloCR.vpy` script).<br>
When doing RGB mode, 6 values of **Seuil** are mandatory: the min and max value for each R, G, B.

Theses values will be reported for **SeuilI** and **SeuilO** args in `YoloCR.vpy` script.

Here some help:
 - SeuilI > SeuilO
 - *generally*, SeuilI is between 170 and 230, and SeuilO is between 20 and 120
 - SeuilI represent the **maximum** value you put to have a subtitle correctly visible
 - SeuilO represent the **minimum** value you put to have a subtitle correctly visible

### `YoloCR.vpy` script

Open the `YoloCR.vpy` file and:
  - copy from `YoloSeuil.py`: **FichierSource**, **DimensionCropBox**, **HauteurCropBox**, **HauteurCropBoxAlt** (in case of some text in top of the video)
  - from `YoloSeuil.vpy` script, copy your min value of Seuil in **SeuilO** args, and your max value of Seuil in **SeuilI** args (in case of RGB mode, **SeuilO** and **SeuilI** would be a table of three value, eg `SeuilI=[140,150,160]` where 140 is the value for `ModeS='R'`, 150 is for `ModeS='G'`, 160 is for `ModeS='B'` )

### Launch `YoloCR.sh` script

#### Filter the video

```
$ vspipe -y YoloCR.vpy - | ffmpeg -i - -c:v mpeg4 -qscale:v 3 -y Filetered_video.mp4

```

#### And OCR it

```
$ ./YoloCR.sh Filetered_video.mp4
```

##### Use the legacy version of Tesseract instead of the LSTM motor

Since the new tesseract version 4.0, LSTM is the new motor. It's generally more accurate in the OCR, but it's loooonger than the old motor.<br>
To use the legacy motor, simply download theses traineddata from [here](https://github.com/tesseract-ocr/tessdata/) and save it in the folder `/usr/share/tesseract/tessdata` under the name `<lang>-legacy.traineddata`.

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
