---
layout: post
title: Convert VobSub file into .srt file
excerpt: <!--more-->
---
So first at all, you should have a MKV file, with a VobSub subtitle file.
{{post.excerpt}}<br>When running ```$ mkvmerge -i mkvfile.mkv```, you should see ```Track ID x: subtitles (VobSub)``` (where **x** is a number).

> Do not forget to install the **mkvtoolnix** package, which contains mkvmerge.

Extract this vobsub file from your mkv by using [my script from here](https://github.com/Subarashii-no-Fansub/Extraction/blob/master/sub_mkv.sh).

 1. ```chmod +x sub_mkv.sh```
 1. ```./sub_mkv.sh mkvfile.mkv```. When it asks "Numéro des sous-titres :", write the number **x** see above.
 1. Normally you'll now have two files: a ```.idx``` and a ```.sub``` (and optionnaly a ```.ifo```)
 1. Then install [vobsub2srt](https://github.com/ruediger/VobSub2SRT) and a *tesseract* lang package (see all the lang package available [here](https://github.com/tesseract-ocr/langdata))
   * I install ```tesseract-data-eng``` and ```tesseract-data-fre```
   * vobsub2srt converts subtitles in VobSub (.idx / .sub) format into subtitles in .srt format.
   * execute it by using ```vobsub2srt mkvfile``` where mkvfile is the filename of the subtitle files WITHOUT the extension (.idx / .sub).
   * vobsub2srt writes the subtitles to a file called ```mkvfile.srt```
   * It's finished.

> If a subtitle file contains more than one language you can use the ```--lang``` parameter to set the correct language. More info [here](https://github.com/ruediger/VobSub2SRT#usage)
> <br>If you want to dump the subtitles as images (e.g. to check for correct ocr) you can use the --dump-images flag.
