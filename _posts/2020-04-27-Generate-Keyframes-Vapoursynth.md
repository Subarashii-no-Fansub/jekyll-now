---
layout: post
title: Generate Keyframes using Vapoursynth
excerpt: <!--more-->
---

{{post.excerpt}}

Prerequisite: Having `vapoursynth` installed

## Installed `vapoursynth-wwxd`

1. Download or clone https://github.com/dubhater/vapoursynth-wwxd
1. `gcc -o libwwxd.so -fPIC -shared -O2 -Wall -Wextra -Wno-unused-parameter $(pkg-config --cflags vapoursynth) src/wwxd.c src/detection.c` in the folder
1. Move the file `libwwxd.so` in `/usr/lib/vapoursynth/` and change ownership to root (`sudo chown root:root libwwxd.so`)

## Launch the `generate_keyframes.py` script

1. Save https://raw.githubusercontent.com/LightArrowsEXE/fansub-utils/master/generate_keyframes.py in a folder to the name `generate_keyframes.py`
1. `python3 generate_keyframes.py --f 'Your_file.mp4'`
1. Import them in aegisub using *Videos* > *Open Keyframes*
