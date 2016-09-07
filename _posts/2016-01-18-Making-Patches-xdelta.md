---
layout: post
title: Making Patches with xdelta
excerpt: <!--more-->
---
{{post.excerpt}}

## Creating a patch

* You need ```xdelta3``` and the V1 file and the V2 file
* Open a terminal, go to the folder where the files are (with ```cd``` command)
* Execute ```xdelta3 -s v1filename v2filename v2patch.xdelta``` (change ```v1filename``` and ```v2filename``` by the correct filename, and ```v2patch``` by the name of the patch)

> You can change the ```.xdelta``` of ```v2patch.xdelta``` by ```vcdiff```
> You can add two more args, ```-e``` to compress the file and a number between 0 and 9 for the compression level (for example ```-9```)

## Applying a patch

* Open a terminal
* If V1 and ```.vcdiff```/```.xdelta``` (```v2patch.xdelta``` for example) are on the same folder.
 * ```xdelta3 -d "v2patch.xdelta"```
* Else ```xdelta3 -d -s old_mkv.mkv v2patch.xdelta new_mkv_name.mkv```

## Release a patch
For Windows user, the minimum is :

 * the patch + a xdelta executer ([download the 32b ZIP here for windows](https://github.com/jmacd/xdelta-gpl/releases/download/v3.0.10/xdelta3-i686-3.0.10.exe.zip))
 * + a .bat file (change ```v2patch.xdelta``` by what you want)

```
@echo off
echo Patching...
xdelta3 -d v2patch.xdelta
echo Patching complete!
@pause
```
OR
```
xdelta3 -d v2patch.xdelta
@echo off
mkdir Non-Batch
move "old_mkv.mkv" "Non-Batch" > NUL 2>&1
```
OR

```
@echo off
setlocal ENABLEDELAYEDEXPANSION

if %PROCESSOR_ARCHITECTURE%==x86 (
  set xdelta3=xdelta3_32b.exe
) else (
  set xdelta3=xdelta3_64b.exe
)

set DIFF=v2patch.xdelta 
set OLD=old_mkv.mkv
set NEW=new_mkv_name.mkv

@echo Patching in progress...

%xdelta3% -d -s "%OLD%" "%DIFF%" "%NEW%"
if %ERRORLEVEL% EQU 0 (
  if EXIST "%NEW%" (
     @echo Patching succesfull, if the new video plays correctly you can delete the old one
  ) else (
  @echo Unknown error  )
) else (
  @echo Patching failed or file exists
)

pause:exit
endlocal
```
