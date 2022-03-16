# Overview

Software Version: 
Device: Raspberry Pi 4 (4G)
OS: Raspbian 11

# How To

Note: libgtk3-dev renamed to libgtk-3-dev in raspbian 11

```
git clone https://github.com/stepmania/stepmania
cd stepmania

git checkout 5_1-rpi
git submodule update --init

sudo apt-get install mesa-common-dev libglu1-mesa-dev libglew1.5-dev libxtst-dev libxrandr-dev libpng-dev libjpeg-dev libjpeg62 zlib1g-dev libbz2-dev libogg-dev libvorbis-dev libc6-dev yasm libasound-dev libpulse-dev libjack-dev binutils-dev libgtk-3-dev libmad0-dev libjack0 libudev-dev libva-dev

sudo apt-get install build-essential cmake mesa-common-dev libglu1-mesa-dev libglew1.5-dev libxtst-dev libxrandr-dev libpng-dev libjpeg-dev zlib1g-dev libbz2-dev libogg-dev libvorbis-dev libc6-dev yasm libasound-dev libpulse-dev binutils-dev libgtk-3-dev libmad0-dev libudev-dev libva-dev nasm

cd Build
cmake -G 'Unix Makefiles' -DCMAKE_BUILD_TYPE=Release .. && cmake ..

make -j4
```

# SpottyMatt Build - Working?

```
sudo apt-get install mesa-common-dev libglu1-mesa-dev libglew1.5-dev libxtst-dev libxrandr-dev libpng-dev libjpeg-dev libjpeg62 zlib1g-dev libbz2-dev libogg-dev libvorbis-dev libc6-dev yasm libasound-dev libpulse-dev libjack-dev binutils-dev libgtk-3-dev libmad0-dev libjack0 libudev-dev libva-dev

sudo apt-get install build-essential cmake mesa-common-dev libglu1-mesa-dev libglew1.5-dev libxtst-dev libxrandr-dev libpng-dev libjpeg-dev zlib1g-dev libbz2-dev libogg-dev libvorbis-dev libc6-dev yasm libasound-dev libpulse-dev binutils-dev libgtk-3-dev libmad0-dev libudev-dev libva-dev nasm

git clone https://github.com/SpottyMatt/raspbian-stepmania-build
cd raspbian-stepmania-build

cp stepmania-build/deps/buster.list stepmania-build/deps/bullseye.list
sed -i 's,-DARM_FPU=$(ARM_FPU),-DARM_FPU=$(ARM_FPU) -DCMAKE_INSTALL_PREFIX=/opt/openpartynight/games,g' Makefile

# Manually initialise submodules
git submodule init
git submodule update
cd stepmania 
git submodule init
git submodule update
cd ..

# Remove all the module inits and git reset from Makefile 

cd stepmania
git checkout 5_1-rpi
cd ..

make

cd /opt/openpartynight/games/stepmania-5.1
touch Portable.ini
```

- Updates to `/opt/openpartynight/games/stepmania-5.1/Saves/Preferences.ini` (not present until first launch)
  - Add `/opt/openpartynight/content/dance/` as AdditionalFolders
  - AllowExtraStage=1
  - DefaultModifiers=FailAtEnd, Overhead
  - DelayedTextureDelete=1
  - DisplayHeight=720
  - DisplayWidth=1280
  - FullscreenIsBorderlessWindow=0
  - MaxHighScoresPerListForMachine=20
  - MaxHighScoresPerListForPlayer=20
  - MaxRegenComboAfterMiss=10
  - PercentageScoring=1
  - ShowInstructions=0
  - ShowMouseCursor=1
  - ShowNativeLanguage=0
  - Theme=Simply Love (only if installed)
  - Windowed=0
  - DefaultModifiers=FailAtEnd, Overhead
  - Theme=Simply Love



# SpottyMatt build

```
sudo apt-get install mesa-common-dev libglu1-mesa-dev libglew1.5-dev libxtst-dev libxrandr-dev libpng-dev libjpeg-dev libjpeg62 zlib1g-dev libbz2-dev libogg-dev libvorbis-dev libc6-dev yasm libasound-dev libpulse-dev libjack-dev binutils-dev libgtk-3-dev libmad0-dev libjack0 libudev-dev libva-dev

sudo apt-get install build-essential cmake mesa-common-dev libglu1-mesa-dev libglew1.5-dev libxtst-dev libxrandr-dev libpng-dev libjpeg-dev zlib1g-dev libbz2-dev libogg-dev libvorbis-dev libc6-dev yasm libasound-dev libpulse-dev binutils-dev libgtk-3-dev libmad0-dev libudev-dev libva-dev nasm

git clone https://github.com/SpottyMatt/raspbian-stepmania-build
cd raspbian-stepmania-build

cp stepmania-build/deps/buster.list stepmania-build/deps/bullseye.list
sed -i 's,-DARM_FPU=$(ARM_FPU),-DARM_FPU=$(ARM_FPU) -DCMAKE_INSTALL_PREFIX=/opt/openpartynight/games,g' Makefile

make
```

It made it passed it after I did the following
- Remove the git reset from Spotty Makefile
- Comment out the `sys/io.h` line in the LightsDriver_LinuxParallel.cpp.o file
- Run `make` again
- It fails cos io stuff missing
- Change to stepmania directory, hard reset and checkout `5_1-rpi`
    - This still does the submodule sync to a commit, is it perhaps grabbing it from rpi branch where it's fixed?
- Reset Spotty Makefile
- Run make again
- NOPE - It was the 67% thing


### Test to try to replicate successful build / making it past lights driver

```
sudo apt-get install mesa-common-dev libglu1-mesa-dev libglew1.5-dev libxtst-dev libxrandr-dev libpng-dev libjpeg-dev libjpeg62 zlib1g-dev libbz2-dev libogg-dev libvorbis-dev libc6-dev yasm libasound-dev libpulse-dev libjack-dev binutils-dev libgtk-3-dev libmad0-dev libjack0 libudev-dev libva-dev

sudo apt-get install build-essential cmake mesa-common-dev libglu1-mesa-dev libglew1.5-dev libxtst-dev libxrandr-dev libpng-dev libjpeg-dev zlib1g-dev libbz2-dev libogg-dev libvorbis-dev libc6-dev yasm libasound-dev libpulse-dev binutils-dev libgtk-3-dev libmad0-dev libudev-dev libva-dev nasm

git clone https://github.com/SpottyMatt/raspbian-stepmania-build
cd raspbian-stepmania-build

cp stepmania-build/deps/buster.list stepmania-build/deps/bullseye.list
sed -i 's,-DARM_FPU=$(ARM_FPU),-DARM_FPU=$(ARM_FPU) -DCMAKE_INSTALL_PREFIX=/opt/openpartynight/games,g' Makefile

cd stepmania
git checkout 5_1-rpi
cd ..

make
```


