# Potential Solutions

A collection of notes to document the various projects found to potentially test to provide a decent UI for OpenPartyNight boxes.

## Kodi / OSMC / OpenELEC

Not easy or intuitive to simply add an application launcher, makes extending to launch games a real struggle

I think the main issue here was not knowing whether compilations of apps actually worked, etc. Perhaps the launching with Advanced Emulator Launcher was the issue. Perhaps the [unofficial release](https://github.com/SpiralCut/plugin.program.advanced.launcher) ([Forum Thread](https://forum.kodi.tv/showthread.php?tid=85724&pid=2668762#pid2668762)) of Advanced Launcher will do the job?

## Plasma Bigscreen

https://plasma-bigscreen.org/get/

Looks like it just turns desktop launchers into buttons to click. It has a build for RPi4.
https://itsfoss.com/kde-plasma-bigscreen/

Looks like it's based on Ubuntu so compilation should work as expected! 

## ChimeraOS

https://chimeraos.org/

Boasts support for launching all different game clients.

FAQ makes it seem like arbitrary launching of programs isn't going to be supported
> While you can technically install Discord and other similar software, ChimeraOS does not support running more than one app or game at a time nor does it support the use of desktop applications. ChimeraOS is specifically designed and optimized for running games in a console-like environment. 

Oh, this is just a wrapper for Steam BPM.

Looks like the companion app could help with a lot of the functionality for remote control of the UI - https://github.com/ChimeraOS/chimera/blob/master/README.md

## Steam Big Picture Mode

This could be a bit of hacky workaround (I presume this requires a Steam login too) but would allow for launching of arbitrary games that are added to it
Refocusing on BPM after app close: https://www.reddit.com/r/linux_gaming/comments/faagju/comment/fixl4c9/?utm_source=share&utm_medium=web2x&context=3

Launch it in `~/.xinitrc`

## GoG Galaxy

https://www.gog.com/galaxy

Like Steam BPM?


## Lakka / Retroarch

Doesn't support much outside of libretro API as that's what it is designed around. 

## Lutris

Looks like it supports "local" games. 

## GameHub

https://github.com/tkashkin/GameHub

Seems to be a Steam/GoG/Humble Bundle/Itch.io instead of just a launcher UI.

## Flex Launcher

https://github.com/complexlogic/flex-launcher

Very new and promising, seems to be an arbitrary application launcher. 

## xlunch

http://xlunch.org/

Looks to be rather complex but potentially what I'm looking for, would require further investigation and testing into controller-support.

## Playnite

https://playnite.link/

**THIS IS A WINDOWS THING FFS**

This looks promising, sort of like BPM without the Steam stuff. If it's just a big picture app launcher then this could be the answer. - https://github.com/JosefNemec/Playnite/wiki/Adding-games-manually

Also looks like it supports themes for various console-like UIs, launching this full-screen should be a flexible solution.




