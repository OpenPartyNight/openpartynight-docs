# Compiling StepMania on arm

# Future Improvements

- According to [mikemintz](https://github.com/SpottyMatt/raspbian-stepmania-build/issues/4#issuecomment-735295508) - HDMI audio works with SoundWriteAhead=2048 in the Stepmania config file
    - This works although sound can occasionally crackle and sound laggy
    - Tweaked to 1024 (as it defaults to 0)
    - Same
    - Upped to 4096 (as recommended by [Project Moondance](https://projectmoon.dance/index.php/releases/5.3-a4.9.5) for older systems)
    - Still feels a bit off but slightly better
    - Set SoundPreferredSampleRate to 44100 (44.1Khz)
    - Not really much of a difference initially but after leaving on a song preivew for a while it seemed perfectly smooth
    - Yep, this seems to work, it may just be that patience is needed initially on the song wheel to catch up
    - 2021-10-20 - There is a slight audio delay, this can likely be addressed by increasing the "Visual Delay", increasing to +1 doesn't seem to get alignment quite right, might need to play with decimal points in the prefs file, +2 seems closer but still feels "off"

# Attempt 6

Bought sound card and it just works, wtf.

Settings:
- 1280x720 fullscreen
- To make the save file stay in the install dir, `touch /opt/openpartynight/games/stepmania-5.1/Portable.ini`
- Set extra data directory (so parent dir for themes, songs, characters, etc to `/opt/openpartynight/content/dance/`)

# Attempt 5 (Continue - 2020-11-10)

Running the build dependencies thing from the wiki wants to install jack stuff... maybe I do it?
```
sudo apt-get install mesa-common-dev libglu1-mesa-dev libglew1.5-dev libxtst-dev libxrandr-dev libpng-dev libjpeg-dev zlib1g-dev libbz2-dev libogg-dev libvorbis-dev libc6-dev yasm libasound-dev libpulse-dev libjack-dev binutils-dev libgtk3-dev libmad0-dev libjack0 libudev-dev libva-dev
```

- No sound with SoundDevice=plughw:0,0 (same for 1,0, 2,0 [cos this one doesn't exist])
- Perhaps it's an overflow thing as [described here](wiki.rivendellaudio.org/index.php/Garbled_audio,_alsa_error_32:_Broken_pipe,_Xrun_errors)
    - Can't really find a way to change this, tried setting `ALSA_BUFFER_SIZE_MAX` on CLI but didn't seem to make a difference
- Made the /boot/config.txt changes
    - No difference
- Set to HDMI1 display mode instead of X screen (no diff, even on restart)
- Biffed ~/.stepmania-5.1
    - No diff
- Tried increasing buffer with `echo 256 > /proc/asound/card0/pcm0p/sub0/prealloc`
    - It doesn't make a FUCKING DIFFERENCE, the value is immediately back to 128
- Installed pulseaudio (`sudo apt install pulseaudio`)
- Recompile...


# Attempt 5 (2020-11-07)

- Looked for any additional sound dev files that may be missing
```
sudo apt install libalsaplayer-dev libghc-alsa-core-dev
```

- Recompile SpottyMatt's...



Other Notes:
- Tested soundcore2 as speaker, this didn't seem to respond to the left/right audio-test command (but HDMI did - note: Analog did not)
```
speaker-test -c2 -twav -l7
```
- I seem to have 2 of the same soundcard (the [ref article](https://www.tinkerboy.xyz/raspberry-pi-test-sound-output/) shows otherwise?)
```
pi@openpartynight:~/COMPILE/raspbian-stepmania-build $ cat /proc/asound/modules
 0 snd_bcm2835
 1 snd_bcm2835
```
- Note: Analog does work with sound, it's headphone aux port



Things to try:
- Explicitly setting audio device in Preferences.ini (SoundDevice=plughw:0,0 to ~/.stepmania-X.X/Save/Preferences.ini)
- Completely biffing ~/.stepmania-5.1
- Forcing HDMI with hdmi_drive=2 in /boot/config.txt - https://raspberrypi.stackexchange.com/a/60639
- Forcing VGA mode for HDMI with hdmi_group=1 in /boot/config.txt (as per SpottyMatt's suggestion)
- Pulseaudio? (3 libpulse packages present, no base packages, perhaps causing issue? - Indications that pulse may be better for StepMania on Linux sometimes described at https://github.com/stepmania/stepmania/issues/1848)



# Attempt 4 (2020-10-30)

## Checking Clock Speeds

- View kernel requested speed with
  ```
  cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_cur_freq
  ```
- Returns 600000Khz (600Mhz)
- View actual ARM CPU frequency with
  ```
  vcgencmd measure_clock arm
  ```
- Returns `frequency(48)=700154304` (700Mhz)

It's running at a slower speed but that's due to it not doing anything. I'd expect the output of the above to be around 1750Mhz when trying to run stepmania.


## Updating/Package Checks

Ran an update to see if anything good comes from it
```
sudo apt update
sudo apt upgrade
```
A bunch of packages got updated, some compiley, some io related ones, perhaps some improvement in there!

Note: Checked clock speed during install and it did spike up to 1750412160 (1750MHz) for most of it, overclocking is working!

- Rebooted

## Recompiling

While SpottyMatt's build hasn't changed, the Stepmania source tree may have (*takes a look...*)

According to [this GitHub issue](https://github.com/stepmania/stepmania/issues/2031) there is a branch of Stepmania for arm64... Will give that a go too!

### SpottyMatt Precompiled Binary

If all else fails, I guess this will be the final solution.

- Install the binary with
  ```
  cd /tmp
  wget https://github.com/SpottyMatt/raspbian-stepmania-deb/releases/download/v5.1.0-b2/stepmania-4b_5.1.0-b2_buster.deb
  sudo dpkg -i stepmania-4b_5.1.0-b2_buster.deb
  ```

- Launch it
  ```
  /usr/games/stepmania-5.1/stepmania
  ```

Still no sound :(

### RPi StepMania Branch Compile

```
sudo apt-get install build-essential cmake mesa-common-dev libglu1-mesa-dev libglew1.5-dev libxtst-dev libxrandr-dev libpng-dev libjpeg-dev zlib1g-dev libbz2-dev libogg-dev libvorbis-dev libc6-dev yasm libasound-dev libpulse-dev binutils-dev libgtk-3-dev libmad0-dev libudev-dev libva-dev nasm
```

```
cd ~/COMPILE

# Low depth to reduce disk space usage
git clone -b 5_1-rpi --depth 1 --single-branch https://github.com/stepmania/stepmania

cd stepmania
git submodule update --init

cd Build
cmake -G 'Unix Makefiles' -DCMAKE_BUILD_TYPE=Release ..
cmake ..
```

Unrecognised processor type... SHRUG

### SpottyMatt Compile

Sound issues aren't just a me problem - https://github.com/SpottyMatt/raspbian-stepmania-build/issues/4

Went through process again but trying with:
- Latest 5-1_new branch commit (6a645b4710dd6a89a5f22a2d849e86a98af5c9a3)
    - FFS it backdated (can't just git checkout)
    - Instead of just doing `make` do `make stepmania-build`
    - This at least fixes most deprecation issues from the built-in commit
    - Still no sound :( 
    - Added make option `-DWITH_FFMPEG=0` to Spotty Makefile
- 5_1-rpi branch latest commit

### ProjectMoon Attempt

This project boasts RPi support!?

```
cd ~/COMPILE

wget https://github.com/TeamRizu/OutFox/releases/download/OF4.9.0HF/Stepmania-Outfox-Alpha-4.9-arm32v7-date-20201006.tar.gz

```

Note: initially tried 64bit build but apparently 64-bit OSes are uncommon for the pi :(


# Attempt 3 

**Installed heatsink & case with fan. This brought the Pi's resting temp from ~75C down to ~35C.**

Used the previously compiled Stepmania from Attempt 1.

Overclocking
```
git clone https://github.com/SpottyMatt/raspbian-stepmania-arcade /opt/openpartynight/lib/SpottyMattEnhancements

cd /opt/openpartynight/lib/SpottyMattEnhancements

make overclock-apply
make no-turbo # cos we'll be playing other games and things
```

The previously compiled version still has no sound and can stutter during gameplay.

Attempted to recompile using SpottyMatt's builder. Noted that, despite alsa errors when running binary, that libasound2-dev is installed so would expect alsa to work for at least menu music.

Questionable lines from outcome
- Still using usr/local for install dir in some parts
```
sudo mkdir -p /usr/local/stepmania-5.1
sudo chmod a+rw /usr/local/stepmania-5.1
```
- A few packages were installed/upgraded, some of which look audio related
- Didn't seem to work :( - CHECK CLOCK SPEEDS AND THINGS



# Attempt 2

The raspbian source has not been updated for a while. Perhaps a newer Stepmania could do it. It looks like the overclocking/turbo of the Pi is needed to get good performance.


# Original Attempt

This mostly worked but the sound issue is not possible to work around.

## Overview

Software Version: master@7b72be79759dc9a31570897b7a48caedced67fcc (https://github.com/SpottyMatt/raspbian-stepmania-build - StepMania 5.1-new)
Device: Raspberry Pi 4 (4G)
OS: Raspbian 10 (buster)

## How To

Perform these actions as a regular user with sudo privileges

- Clone source code

    ```
    mkdir ~/COMPILE
    cd ~/COMPILE
    git clone https://github.com/SpottyMatt/raspbian-stepmania-build
    ```

- Update prefixes in make file

    ```
    cd raspbian-stepmania-build
    sed -i 's,-DARM_FPU=$(ARM_FPU),-DARM_FPU=$(ARM_FPU) -DCMAKE_INSTALL_PREFIX=/opt/openpartynight/games,g' Makefile
    ```

- Run make (this will install stepmania too)

    ```
    make
    ```

## Tidy

- Delete the build directory

    ```
    rm -rf ~/COMPILE/raspbian-stepmania-build
    ```


## To Do

- Fix sound output of compiled version (no audio!! ultrastar build still works so definitely something to do with stepmania compilation)
- Ensure consistency of key mappings between game starts (https://github.com/SpottyMatt/raspbian-stepmania-arcade#instructions)
- Provide in-place configuration to start the game full screen and with various other optimised settings
