---
layout: post
title: Compile x264 with l-smash
excerpt: <!--more-->
---

I'll explain you how to compile x264 with l-smash to have mp4 video on linux system (eg: Fedora).

{{post.excerpt}}

It's easy:

## Install l-smash

 * install `git`
 * do `git clone https://github.com/l-smash/l-smash.git`
 * `cd l-smash`
 * `./configure --prefix='/usr' --enable-shared --disable-static`
 * `make`
 * `sudo make install`

## Compile x264

 * do `git clone git://git.videolan.org/git/x264.git`
 * `cd x264`
 * `./configure --prefix='/usr' --enable-shared --enable-pic --enable-lto`
 * here check that you have the line `mp4: lsmash`
 * and then build it: `make`

In case you want to use x264 with l-smash, choose the `x264` file from the folder x264 build above!

## Bonus: Blender

Blender is not build with ffmpeg on Fedora, so you can use the binarie from Blender themself, located here: 
[https://www.blender.org/download/](https://www.blender.org/download/)
