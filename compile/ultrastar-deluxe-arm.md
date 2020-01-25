# Compiling UltraStar Deluxe on arm

## Overview

Software Version: master@f1e9f7e954a254c7cd9eafec302234b1cc7dbef8 
Device: Raspberry Pi 4 (4G)
OS: Raspbian 10 (Buster)

## How To

Perform these actions as a regular user with sudo privileges.

- Install make dependencies

    ```
    sudo apt-get update && sudo apt-get install git automake make gcc fpc libsdl2-image-dev libavformat-dev libswscale-dev libsqlite3-dev libfreetype6-dev portaudio19-dev libportmidi-dev liblua5.3-dev libopencv-videoio-dev
    sudo apt-get update && sudo apt-get install git fpc libsdl2-dev libsdl2-image-dev libsdl2-image-2.0-0 libsdl2-2.0-0 libsdl2-mixer-2.0-0 libsdl2-mixer-dev libsdl2-net-2.0-0 libsdl2-net-dev libsdl2-ttf-2.0-0 libsdl2-ttf-dev libsdl2-gfx-1.0-0 libsdl2-gfx-dev ffmpeg libavdevice-dev libsqlite3-0 libsqlite3-dev libpcre3 libpcre3-dev ttf-dejavu fonts-freefont-ttf portaudio19-dev lua5.1-dev libpng16-16 libopencv-highgui-dev libprojectm-dev
    ```

- Create project compilation directory

    ```
    mkdir ~/COMPILE/
    cd ~/COMPILE
    git clone https://github.com/UltraStar-Deluxe/USDX
    ```

- Checkout the target software version branch

    ```
    cd USDX
    git checkout f1e9f7e954a254c7cd9eafec302234b1cc7dbef8
    ```

- Compile steps

    ```
    ./autogen.sh
    ./configure
    make
    ```

- Test running game

    ```
    ./game/ultrastardx
    ```

## To Do

- Install to `/opt/openflight/ultrastar/`

- Verify symlinking songs works

- 


