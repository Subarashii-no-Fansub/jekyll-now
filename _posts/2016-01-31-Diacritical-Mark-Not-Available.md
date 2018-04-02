---
layout: post
title: Diacritical Mark Not Available
---
I sometimes write in french my subtitles, and in french we have a lot of [diacritical Mark](https://en.wikipedia.org/wiki/Diacritic) (*[signe diacritique](https://fr.wikipedia.org/wiki/Diacritique) comme les accents, tréma et cédille*).
<br>In rare case, the font does not support the [acute accent](https://en.wikipedia.org/wiki/Acute_accent) or other diacritals marks.

## How to know if a font support these marks

### Check if the font is adding to the sytem

The first thing I do is I write it normally in [aegisub](http://www.aegisub.org/). 
<br>After I add my font on my OS (see [Adding fonts to a Linux OS](https://subarashii-no-fansub.github.io/Subbing-Tutorial/Adding-Font/)), I check it with Aegisub (File > Fonts Collector > Check fonts for availability and click on **start**).

When a font is not available (```Could not find font 'xxxx'. Used on lines: xxx```), just [add it](../Adding-Font/).

![A font is missing!](https://cloud.githubusercontent.com/assets/6844060/18314994/abebb2e8-7515-11e6-8964-ccf4fadf117c.png)
![With the font](https://cloud.githubusercontent.com/assets/6844060/18314975/959d46dc-7515-11e6-80b1-c7d73c378703.png)

In these two examples, I put the font in `.font` folder, that's a **bad** practice!<br>They must be on `.local/share/fonts`.

### See that the font isn't available for the glyph
<br>Else if the font can't show your mark, it's written ```Found 'xxx' at '/home/xxx/.fonts/font.ttf' 'xxx' is missing the following glyphs used: ’. Used on lines: xx"```.
<br>And at the end: ```One font was found, but was missing glyphs used in the script.```.

## Some glyphes
* For ```é```, write a `e` and add `\frz127.1\` with `'`
* For ```è```, write a `e` and add `\frz13.67\` with `'`
* For ```œ```, write `{\fsp-5}o{\fsp1}e`
