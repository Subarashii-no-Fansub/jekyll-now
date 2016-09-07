---
layout: post
title: Adding fonts to a Linux OS
excerpt: <!--more-->
---
{{post.excerpt}}
* Open a console
* Go in your home folder
* Create a ```.local/share/fonts``` folder if it doesn't exist
* Copy the font files in this location
  * you can extract the font from a mkv using this [script](https://raw.githubusercontent.com/Subarashii-no-Fansub/Extraction/master/fonts_mkv.sh)
* Update your font cache by executing on your console : ```$ fc-cache -fv```
* Done :-)
