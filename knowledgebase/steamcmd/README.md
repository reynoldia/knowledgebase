# SteamCMD

## Installation

https://developer.valvesoftware.com/wiki/SteamCMD

Create a user for SteamCMD
```bash
sudo useradd -m steam
sudo passwd steam 
sudo -u steam -s
cd /home/steam
```

Add dependencies and install steamcmd and dependencies
```bash
sudo add-apt-repository multiverse
sudo dpkg --add-architecture i386
sudo apt update

sudo apt install lib32gcc-s1 steamcmd 

sudo ln -s /usr/games/steamcmd /home/steam/steamcmd
```
