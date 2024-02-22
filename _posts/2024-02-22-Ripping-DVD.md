---
layout: post
title: Ripping DVD
excerpt: <!--more-->
---
{{post.excerpt}}

In true you can rip DVD / BD / UHD BD with this tutorial

* Download MAKEMKV: https://www.makemkv.com/

On makemkv:
 * put your dvd/bd
 * open makemkv
 * Choose file > save

In the case of DVD, the operation ends here.  

For BDs, it is necessary to carry out additional operations:
 * When saving, check the Video decryption file" box
 * once the backup is complete, delete the "MAKEMKV" folder in the created folder, "BDMV" and "CERTIFICATE" should remain

On windows only, then use imgburn to rebuild an iso; you will find the software here: https://www.imgburn.com/
 * open imgburn
 * select "create image file from files/folders"
 * select the folder created above (which therefore contains the 2 folders "BDMV" and "CERTIFICATE") and the path to the ISO destination
 * (question not often asked) "the BD uses USD and not ISO9660 + UDF", choose yes
 * choose a label for the UDF (I keep the default one) and choose yes
 * then wait :)
 * and... done
