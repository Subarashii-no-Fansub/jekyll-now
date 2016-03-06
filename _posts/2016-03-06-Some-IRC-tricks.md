---
layout: post
title: Some tricks for IRC
---
I use ```hexchat``` software to speak and to download through XDCC.

## Download on IRC

You can follow this guide wich is written to download on the #horriblesubs channel on IRC: [http://horriblesubs.info/images/hexchatguide.png](http://horriblesubs.info/images/hexchatguide.png).

## Seed the files you've downloading on IRC

If you want to seed on torrent all the files you download, sometimes you must change all the underscore (```_```) into spaces (``` ```).
<br>To do that, just use this command: ```$ rename 's/_/ /g' *```.

## Change Access to an user on IRC

You can see all the people which have privilege by using: ```/msg ChanServ ACCESS #channel LIST```

The default value is:

  * 10/SOP/&: Chanserv give OP status automatically. User can use ```AKICK``` command.
  * 5/OP/@: Chanserv give OP status automatically. (/op <username> || /deop <username>)
  * 4/HalfOp/%: sometimes not available. (/hop <username> || /dehop <username>)
  * 3/Voice/+: User is voiced. (/voice <username> || /devoice <username>)
  * 0 : No privilege. By default.

To add an user: ```/msg ChanServ ACCESS #channel ADD <username> level```.
