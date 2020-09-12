---
layout: post
title: Convert VobSub file into .srt file
excerpt: <!--more-->
---
{{post.exerpt}}

So first of all, you should have a MKV file, with a VobSub subtitle file; or a combinaison of idx/sub files.

## Extracting idx/sub files

When running ```$ mkvmerge -i mkvfile.mkv```, you should see ```Track ID x: subtitles (VobSub)``` (where **x** is a number).

> Do not forget to install the **mkvtoolnix** package, which contains mkvmerge.

Extract this vobsub file from your mkv by using [my script from here](https://raw.githubusercontent.com/Subarashii-no-Fansub/Extraction/master/sub_mkv.sh).

 1. ```chmod +x sub_mkv.sh```
 1. ```./sub_mkv.sh mkvfile.mkv```. When it asks "Subtitle Track ID:", write the number **x** see above.
 1. Normally you'll now have two files: a ```.idx``` and a ```.sub``` (and optionnaly a ```.ifo```)
 
 ## OCR the two files
 
 ### By using ffmes
 
 1. Install `ogmrip`, ```tesseract-data-eng``` and ```tesseract-data-fre``` packages
 1. Clone https://github.com/Jocker666z/ffmes
 1. Put your idx/sub files and move them alone in a folder
 1. Launch ffmes: `bash ffmes.sh [FOLDER OF IDX/SUB FILE]/`
 1. Choose option 18, and the language
 1. Done, you have the srt file!
 
 
 ### Old version: by using vobsub2srt
 
 1. Then install [vobsub2srt](https://github.com/bubonic/VobSub2SRT) and a *tesseract* lang package (see all the lang package available [here](https://github.com/tesseract-ocr/langdata))
   * install ```tesseract-data-eng``` and ```tesseract-data-fre```
   * vobsub2srt converts subtitles in VobSub (.idx / .sub) format into subtitles in .srt format.
   * execute it by using ```vobsub2srt mkvfile``` where mkvfile is the filename of the subtitle files WITHOUT the extension (.idx / .sub).
   * vobsub2srt writes the subtitles to a file called ```mkvfile.srt```
   * It's finished.

> If a subtitle file contains more than one language you can use the ```--lang``` parameter to set the correct language. More info [here](https://github.com/ruediger/VobSub2SRT#usage)
> <br>If you want to dump the subtitles as images (e.g. to check for correct ocr) you can use the --dump-images flag.
