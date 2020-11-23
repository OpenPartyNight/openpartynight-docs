# How to Map USB Devices to Consistent Names

## Overview

This process allows for consistent input from USB devices by mapping the device ID to a human-readable friendly name.


## Example: Microphone

This example maps a Logitech USB Microphone to friendly name "MicPlayer1".

- Plug USB device into pi

- Identify the USB device

    <pre>
    $ lsusb
    Bus 003 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
    Bus 002 Device 001: ID 1d6b:0003 Linux Foundation 3.0 root hub
    Bus 001 Device 003: ID 89e5:1001
    Bus 001 Device 004: ID 0e6a:02c0 Megawin Technology Co., Ltd
    <b>Bus 001 Device 005: ID 046d:0a03 Logitech, Inc. Logitech USB Microphone</b>
    Bus 001 Device 002: ID 2109:3431 VIA Labs, Inc. Hub
    Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
    </pre>

- Locate further device information

    ```
    lsusb -d 046d:0a03 -v
    ```

- Add a udev rule to /etc/udev.d/

    ```

    ```

