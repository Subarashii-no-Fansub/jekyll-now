---
layout: post
title: Diacritical Mark Not Available
---
I sometimes write in french my subtitles, and in french we have a lot of [diacritical Mark](https://en.wikipedia.org/wiki/Diacritic) (*[signe diacritique](https://fr.wikipedia.org/wiki/Diacritique) comme les accents, tréma et cédille*).
<br>In rare case, the font does not support the [acute accent](https://en.wikipedia.org/wiki/Acute_accent) or other diacritals marks.

## How to know if a font support these marks

The first thing I do is I write it normally in [aegisub](http://www.aegisub.org/). 
<br>After I add my font on my OS (see [Adding fonts to a Linux OS](../Adding-Font/)), I check it with Aegisub (File > Fonts Collector > Check fonts for availability and click on **start**).

When a font is not available (```Could not find font 'xxxx'. Used on lines: xxx```), just add it.
<br>Else if the font can't show your mark, it's written ```Found 'xxx' at '/home/xxx/.fonts/font.ttf' 'xxx' is missing the following glyphs used: ’. Used on lines: xx"```.
<br>And at the end: ```One font was found, but was missing glyphs used in the script.```.
