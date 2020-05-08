---
layout: post
title: Fix Separated & Linked MKV Files.
excerpt: <!--more-->
---
{{post.excerpt}}

## How can I know it's separated?

Some groups think it’s fancy to remove the OP and ED from the episode and store them as separate files in order to save space on their releases by avoiding repetition for each episode.
For doing that, they use MKVs chapter segment linking feature to make them play correctly.

For eg, Coalgirls was a group that done this a lot:
```
    [Coalgirls]_Kannagi_01_(1280x720_Blu-ray_FLAC)_[4DF6A563].mkv (323.1 MiB)
    [Coalgirls]_Kannagi_02_(1280x720_Blu-ray_FLAC)_[D75E7F2C].mkv (343.5 MiB)
    [Coalgirls]_Kannagi_03_(1280x720_Blu-ray_FLAC)_[CEDE4A97].mkv (382.2 MiB)
    [Coalgirls]_Kannagi_04_(1280x720_Blu-ray_FLAC)_[96C229C4].mkv (323.5 MiB)
    [Coalgirls]_Kannagi_05_(1280x720_Blu-ray_FLAC)_[562DBE63].mkv (335.9 MiB)
    [Coalgirls]_Kannagi_06_(1280x720_Blu-ray_FLAC)_[F7D1764D].mkv (304.1 MiB)
    [Coalgirls]_Kannagi_07_(1280x720_Blu-ray_FLAC)_[CA3704AE].mkv (309.7 MiB)
    [Coalgirls]_Kannagi_08_(1280x720_Blu-ray_FLAC)_[F7B0B604].mkv (380.1 MiB)
    [Coalgirls]_Kannagi_09_(1280x720_Blu-ray_FLAC)_[1E9E0B46].mkv (342.2 MiB)
    [Coalgirls]_Kannagi_10_(1280x720_Blu-ray_FLAC)_[01102516].mkv (306.8 MiB)
    [Coalgirls]_Kannagi_11_(1280x720_Blu-ray_FLAC)_[F0D97739].mkv (368.3 MiB)
    [Coalgirls]_Kannagi_12_(1280x720_Blu-ray_FLAC)_[2B54B98F].mkv (308.9 MiB)
    [Coalgirls]_Kannagi_13_(1280x720_Blu-ray_FLAC)_[54703869].mkv (348.6 MiB)
    [Coalgirls]_Kannagi_14_(1280x720_Blu-ray_FLAC)_[308B4631].mkv (409.4 MiB)
    [Coalgirls]_Kannagi_ED01_(1280x720_Blu-ray_FLAC)_[E44A4B14].mkv (43.2 MiB)
    [Coalgirls]_Kannagi_ED02_(1280x720_Blu-ray_FLAC)_[1F5609E5].mkv (44.0 MiB)
    [Coalgirls]_Kannagi_ED03_(1280x720_Blu-ray_FLAC)_[0A6B762B].mkv (44.6 MiB)
    [Coalgirls]_Kannagi_ED04_(1280x720_Blu-ray_FLAC)_[FCA61CCF].mkv (41.2 MiB)
    [Coalgirls]_Kannagi_ED05_(1280x720_Blu-ray_FLAC)_[1A9CABA3].mkv (42.3 MiB)
    [Coalgirls]_Kannagi_ED06_(1280x720_Blu-ray_FLAC)_[1F3AA3A7].mkv (44.2 MiB)
    [Coalgirls]_Kannagi_ED08_(1280x720_Blu-ray_FLAC)_[BEDA52D8].mkv (43.8 MiB)
    [Coalgirls]_Kannagi_ED09_(1280x720_Blu-ray_FLAC)_[67A7AF8A].mkv (43.7 MiB)
    [Coalgirls]_Kannagi_ED10_(1280x720_Blu-ray_FLAC)_[2D6203AB].mkv (45.5 MiB)
    [Coalgirls]_Kannagi_ED11_(1280x720_Blu-ray_FLAC)_[7FD78B3A].mkv (43.1 MiB)
    [Coalgirls]_Kannagi_ED12_(1280x720_Blu-ray_FLAC)_[268C0CA6].mkv (44.8 MiB)
    [Coalgirls]_Kannagi_ED14_(1280x720_Blu-ray_FLAC)_[43CE2840].mkv (42.2 MiB)
    [Coalgirls]_Kannagi_OP_(1280x720_Blu-ray_FLAC)_[47A347D1].mkv (60.7 MiB)
    [Coalgirls]_Kannagi_Play_All_(1280x720_Blu-ray_FLAC)_[AF6D56F9].mkv (4.2 MiB)
    [Coalgirls]_Kannagi_Play_All_No_OPED_(1280x720_Blu-ray_FLAC)_[D94FC256].mkv (4.2 MiB)
    [Coalgirls]_Kannagi_Play_All_No_Previews_(1280x720_Blu-ray_FLAC)_[00F25371].mkv (4.2 MiB)
```

If you only download `[Coalgirls]_Kannagi_01_(1280x720_Blu-ray_FLAC)_[4DF6A563].mkv (323.1 MiB)`, you'll have an episode without preview, opening and ending; if you download all and put all files in a same folder, you'll have ep 1 with opening, ending and preview in your player = it's a separated & linked mkv files.

## Fix it

### Automatically

By using the project [UnlinkMKV](https://github.com/gnoling/UnlinkMKV), it's simple: you download all the file, and run the `unlinkmkv` command (after having installed the dependencies - MKVToolnix, and some perl dependencies - of course).<br>
If an audio is FLAC, the software will convert it to ALAC format. You can also read my post on [Encode audio from FLAC to AAC using fdkaac on Linux](../Encode-audio-flac-aac-linux/)

### Manually

(TODO)
