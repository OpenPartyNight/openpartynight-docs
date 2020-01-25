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
    cat << EOF > Makefile.patch
    --- Makefile	2020-01-25 17:32:26.475149635 +0000
    +++ Makefile.orig	2020-01-25 17:31:34.103204886 +0000
    @@ -70,8 +70,7 @@
                -DWITH_FULL_RELEASE=1 \
            -DCMAKE_BUILD_TYPE=Release \
                -DARM_CPU=$(ARM_CPU) \
    -		-DARM_FPU=$(ARM_FPU) \
    -		-DCMAKE_INSTALL_PREFIX=/opt/openpartynight/games/stepmania
    +		-DARM_FPU=$(ARM_FPU)
        cmake $(PARALLELISM) .
        git reset --hard HEAD^
    EOF
    git apply Makefile.patch 
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
