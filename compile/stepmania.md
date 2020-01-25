# Compiling StepMania on arm

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
    sed -i 's,-DARM_FPU=$(ARM_FPU),-DARM_FPU=$(ARM_FPU) -DCMAKE_INSTALL_PREFIX=/opt/openpartynight/games/stepmania,g' Makefile
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

- Ensure consistency of key mappings between game starts (https://github.com/SpottyMatt/raspbian-stepmania-arcade#instructions)
- Provide in-place configuration to start the game full screen and with various other optimised settings
- 
