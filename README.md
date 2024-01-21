# steam

## install steamcmd on debian 12

```bash
# add user
useradd -m -s /bin/bash steam
passwd steam
usermod -aG sudo steam

# add repo
tee /etc/apt/sources.list <<EOF_SOURCES
deb http://deb.debian.org/debian/ bookworm main non-free
deb-src http://deb.debian.org/debian/ bookworm main non-free
EOF_SOURCES

# increase limits
tee /etc/sysctl.conf <<EOF_SYSCTL
fs.file-max=100000
EOF_SYSCTL

sysctl --system

tee /etc/security/limits.conf <<EOF_LIMITS
* soft nofile 100000
* hard nofile 100000
EOF_LIMITS

tee /etc/pam.d/common-session <<EOF_SESSION
session required pam_limits.so
EOF_SESSION

# install packages
dpkg --add-architecture i386
apt update
apt install steamcmd
```

## install ark server

```bash
/usr/games/steamcmd +force_install_dir /home/steam/ark/ +login anonymous +app_update 376030 validate +quit
```

## start ark server

```bash
export SERVERNAME=myark
export ADMINPASSWORD=topsecret
/home/steam/ark/ShooterGame/Binaries/Linux/ShooterGameServer TheIsland?listen?SessionName=$SERVERNAME?ServerAdminPassword=$ADMINPASSWORT -server -log
```
