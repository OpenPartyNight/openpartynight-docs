# How to Host a Samba Server on Pi

This will allow for easy addition of game content (songs, themes, etc).

## How To

- Install dependencies

    ```
    sudo apt-get install samba samba-common-bin
    ```

- Configure samba (run as root)

    ```
    cat << EOF > /etc/samba/smb.conf
    [global]
       workgroup = WORKGROUP
       log file = /var/log/samba/log.%m
       max log size = 1000
       logging = file
       panic action = /usr/share/samba/panic-action %d
       server role = standalone server
       obey pam restrictions = yes
       unix password sync = yes
       passwd program = /usr/bin/passwd %u
       passwd chat = *Enter\snew\s*\spassword:* %n\n *Retype\snew\s*\spassword:* %n\n *password\supdated\ssuccessfully* .
       pam password change = yes
       map to guest = bad user
       usershare allow guests = yes
    [CONTENT]
       comment = OpenPartyNight Game Content
       path = /opt/openpartynight/content
       create mask = 0775
       directory mask = 0775
       read only = no
       browseable = yes
       public = yes
       force user = pi
       only guest = no
    EOF
    ```

- Create share directory and ensure it has correct permissions

    ```
    sudo mkdir -p /opt/openpartynight/content/{sing,dance}/{songs,themes}
    sudo chown -R pi:pi /opt/openpartynight/
    ```

- Set samba password to "openpartynight" (going to use something easy as this is only shared over LAN)

    ```
    printf 'openpartynight\nopenpartynight\n' | sudo smbpasswd -a pi
    ```

- Ensure server is running

    ```
    systemctl restart smbd
    systemctl restart nmbd
    ```

The raspberry pi storage directory can now be mounted from Mac, Windows and Linux systems by mounting `smb://OPENPARTYNIGHT/CONTENT` (Linux/Mac) or `\\OPENPARTYNIGHT\CONTENT` (Windows). If prompted for user details, the username is `pi` and the password is `openpartynight`.

## To Do

- Examples of connecting to the samba share from other platforms
