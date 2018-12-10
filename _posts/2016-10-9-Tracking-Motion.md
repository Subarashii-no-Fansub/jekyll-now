---
layout: post
title: Tracking Motion using Blender
excerpt: <!--more-->
---
{{post.excerpt}}
A lot of people who does TypeSetting use Mocha to do that!<br>But because I'm on Linux, this solution is not the best for me.
<br>Here a tutorial to do that on Blender, a free and open-source software. You can use it on Windows too!

## Install Aegisub Motion plugin

* Go on [github.com/TypesettingTools/Aegisub-Motion/releases](https://github.com/TypesettingTools/Aegisub-Motion/releases) and download the latest release
* Extract the content (the folders `autoload`, `include`) in `~/.aegisub/automation` (you may create this folder) for Linux.
  * For others OS, see [this page](https://github.com/TypesettingTools/Aegisub-Motion/wiki/Installation#installation-instructions)
* Install `Blender`, and `x264`

## Do a tracking

### In Aegisub

You should have open a video and a subtitle file.

1. The first thing to do is to do you edit on the first frame when the edit appears on the video. And the end of the time must correspond to the last frame of the edit showing in this video.
  * to check that, time it, and with the **directional arrow** push right or left to see if in the previous/next frame, the edit is showing.
  * if yes, change the time in aegisub by the [time by frame](https://cloud.githubusercontent.com/assets/6844060/19222330/3124e70a-8e56-11e6-9891-be692aada1a2.png)
  * and report the frame number to the good input (start/end) (EG: [here](https://cloud.githubusercontent.com/assets/6844060/19222348/86f1b7b2-8e56-11e6-8d8d-ebff8cb392c3.png) the edit finish at `4752` but the last frame is `4753` - see under the video)
 2. After the 1. done, we'll trim the video using Aegisub Motion. But before, you need to configure it once:
  * select the edit line (good timed) and select **Automation** > **Aegisub-Motion** > **Trim Setting**
  * here let's **video** to `?video`, change **encoding preset** to `x264` and click on **Encoder..** button.
  * Select the x264 binary (in Linux, it's `/sbin/x264` or `/usr/bin/x264`)
  * Save
  * select **Automation** > **Aegisub-Motion** > **Trim**
 3. Now in Blender
  * open the 'movie clip editor' view, in the bottom left
  * at the right of this, click on Open, open your video (it's in the same folder than the video you open in aegisub, but with at the end `[start_frame-end_frame]`)
  * At the mid-left, in tracking settings, change settings: pattern size at 15; search size at 61
  * change the *motio* to
     - Loc, for locality's changing
     - LocRot, for locality+rotation's changing
     - LocScale, for locality+size's changing
     - LocRotScale, for locality+size+rotation's changing
  * change the *match* to > previous frame
  * add a marker (Marker > Add at the left)
  * in the right, check *search* in the *marker display* section
  * You can track it (using at the left *Trackt* section > Track > right directionnal arrow or left directionnal arrow)
4. After that, we need to add the plugin to export the data to aegisub-motion. You need to do that once!
  * save [aae-export.py](https://raw.githubusercontent.com/Subarashii-no-Fansub/AAE-Export/master/aae-export.py)
  * in blender: file > user preferences > add-ons > install from file (search the file `aae-export.py` you've just downloaded!)
  * Do not forget to activate it! (by checking the box). The name in blender of this add-ons is `Import-Export: Export: Adobe After Effects 6.0 Keyframe Data`
5. We can now do: file > export > dobe After Effects 6.0 Keyframe Data
  * save it on a file.
  * Open the file, copy the content
6. And paste it into **aegisub** > **Automation** > **Aegisub-Motion** > **Apply**
