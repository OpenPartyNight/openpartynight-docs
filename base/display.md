

## 4k Resolution

Big screens are worth downscaling, raspbian seems to struggle to know what to do. 

Set the pixel doubling gives and easier to see resolution but may result in screen tearing.

Doing `xrandr -s 1920x1080` will set res to standard HD but won't persist between reboots (could rc.local this?)

- Literally just right-click in the screens view to set resolution smh

## Audio 

Set default out to HDMI:
- Right-click on the audio symbol and select it as the output 
- I LITERALLY HAVE NO IDEA HOW TO DO THIS FROM CLI ALSAMIXER AND AMIXER UTILS SUCKKKK
