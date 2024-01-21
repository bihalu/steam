# steam

## install steamcmd on debian 12

```bash
# add user
useradd -m steam
passwd steam
usermod -aG sudo steam

# add repo
tee /etc/apt/sources.list <<EOF
deb http://deb.debian.org/debian/ bookworm main non-free
deb-src http://deb.debian.org/debian/ bookworm main non-free
EOF

# install packages
dpkg --add-architecture i386
apt update
apt-get install steamcmd

# switch user and create link for steamcmd
su - steam
ln -s /usr/games/steamcmd steamcmd

./steamcmd
```