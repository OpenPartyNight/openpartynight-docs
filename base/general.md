
## Enable VNC 

VNC is useful for remote configuration & debugging of a Pi, allowing for easy access and maintenance from your preferred system.

To enable VNC:
- Open the configuration tool
  ```
  sudo raspi-config
  ```
- Select "Interface Options"
- Select VNC and answer "Yes" to "Enable VNC server?" 

To configure non-system passwords (for MacOS screen share support):
- Set VNC password (default: `partytime`)
  ```
  sudo vncpasswd -service
  ```
- Enable password authentication
  ```
  echo "Authentication=VncAuth" >> /etc/vnc/config.d/common.custom
  ```
- Restart VNC service
  ```
  sudo systemctl restart vncserver-x11-serviced
  ```
