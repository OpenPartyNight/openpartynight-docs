# Overview

There are a few options to adding pretty, accessible interfaces.

# General Thoughts/Notes

- Contribute the OpenPartyNight versions of the compiled software to the add-on libraries for supported/tested interfaces, this would allow the name to spread out as Stepmania & Ultrastar (attributed to _OpenPartyNight_) become available in the game libraries (obvs with correct contribution & links to contributors/original software repos).

# Applications/Interfaces

## [Kodi](https://kodi.tv)

Used to be the XBMC project, definitely going to have a lot of support behind it. Basically full media center so it'd allow the console to be even further expandible.

Pros:
- Full media center (including [game library](https://kodi.wiki/view/Games) support
- Control API (so web browsers, remote controls, etc can all be configured to work with it)
    - Additionally, built-in support for many remote controls
- Application, not OS, so can be [installed on current distribution](https://kodi.wiki/view/HOW-TO:Install_Kodi_on_Raspberry_Pi#Raspberry_Pi_OS)

Cons:
- Game library support is currently very primative (and seems focussed on emulation)

Add-ons:
- [Sports TV](https://zone3tech.com/how-to-install-sporthd-kodi-addon-watch-live-sports-game/)
- [Retro Game Streamed from Internet Archive](https://www.maketecheasier.com/turn-kodi-gane-arcade-center/)


Initially concerned that the game support was too primitive but that seems like for integrated support for emulators. It seems like it'd be fairly straightforward to add a third-party game.

## [LibreELEC](https://libreelec.tv)

A fork of Kodi, focussed on being stable and providing enough OS stuff for Kodi.

Pros:
- Same as Kodi
- [Custom boot splash screen](https://libreelec.wiki/how-to/change-bootscreen)

Cons:
- Poorly documented
- Requires full OS install

## [OSMC](https://osmc.tv)

Looks in a similar vein to the above, again it seems like third-party apps can just be added to these sorts of things so perhaps it'd be quite easy to hack games in?

# Installation/Setup

## Kodi

- Install Kodi
```
sudo apt update
sudo apt install kodi
```

- Kodi can now be launched from te CLI with
```
kodi
```

Note: The Kodi UI is not visible to VNC sessions so will confusingly display only a black screen.


- Launch on boot
```
```

- Enable webserver for configuration
  - Open Kodi
  - Go to Settings -> Services -> Webserver -> Allow Control of Kodi via HTTP
  - Leave port as 8080 and user as kodi 
  - Kodi can now be reached from a web browser on the same network at http://openpartynight:8080/
- Nginx config file
```

```

### Customisation

Via Normal GUI

- Add games to Games library
  - Click Games from the main menu (navigate so it is highlighted and then press Ok or Enter on your remote)
  - Select "Add games..."
  - Click "Browse" and navigate to `/opt/openpartynight/bin/`
  - Set the Name for this media source to "OPN Games"
  - NOPE


- Add games to Games Library
  - Download latest Advanced Launcher from https://github.com/SpiralCut/plugin.program.advanced.launcher/releases to `/opt/openpartynight/content/kodi/addons`
  - Select Add-Ons from Main Menu then click the settings gear and click "Install From Zip File"
  - Select the release zip
  - Go to Add-Ons menu and select Advanced Launcher
  - PLUGIN OUT OF DATE!

- Add games to Games Library
  - Above but with  https://github.com/Wintermute0110/plugin.program.AEL/releases
  - Launch plugin
  - Open the context menu (home/settings button on remote, c on keyboard)
  - Select Add New Launcher
  - Select Standalone Launcher
  - Select the game launch script (all file types are allowed/valid) 
  - Set emulator to Unknown
  - It launches but the window is nowhere to be seen, Kodi seems to do some weird stuff and take over the X session, even VNC has no idea where the window is

This is just generally unwieldy.



Via Web GUI

- Enable AirPlay
  - Settings -> Services -> Airplay
  - Enable AirPlay support
- Add games to Games library
- Change default theme




TODO: Determine CLI methodology for automation

Note: Unless otherwise stated, the config file to change the setting in is `~/.kodi/userdata/guisettings.xml`

- Enable AirPlay
- Add games to Games library
- Change default theme




## Pegasus

using release zip doesn't work, just fails with weird errors
```
failed to export dumb buffer: Permission denied
Failed to create scanout resource
[w] QEGLPlatformContext: eglSwapBuffers failed: 3003
[w] Could not lock GBM surface front buffer!
```

