# ARK: Survival Evolved

## Installation

See here for more details: https://ark.fandom.com/wiki/Dedicated_server_setup

To initially download the game,
run `/home/steam/steamcmd +login anonymous +force_install_dir <install_dir> +app_update 376030 +quit`

One the game is installed, create a file named `/etc/systemd/system/ark-dedicated.service` with the following contents:

```ini
[Unit]
Description=ARK: Survival Evolved dedicated server
Wants=network-online.target
After=syslog.target network.target nss-lookup.target network-online.target

[Service]
ExecStartPre=/home/steam/steamcmd +login anonymous +force_install_dir <install_dir> +app_update 376030 +quit
ExecStart=<install_dir>/ShooterGame/Binaries/Linux/ShooterGameServer TheIsland?listen?SessionName=<session_name> -server -log
WorkingDirectory=<install_dir>/ShooterGame/Binaries/Linux
LimitNOFILE=100000
ExecReload=/bin/kill -s HUP $MAINPID
ExecStop=/bin/kill -s INT $MAINPID
User=steam
Group=steam

[Install]
WantedBy=multi-user.target
```

# Configuration

TODO: How to edit config?

# Modding

See here for more details: https://help.akliz.net/docs/install-ark-survival-evolved-mods-on-a-server

Subscribe to mods in the Steam Workshop. The mods will be downloaded
to `<steam_dir>\steamapps\common\ARK\ShooterGame\Content\Mods`.

Copy this entire folder to `<install_dir>/ShooterGame/Content/Mods`.

In `<install_dir>/ShooterGame/Saved/Config/LinuxServer/GameUserSettings.ini`, inside of `[ServerSettings]`, edit
the `ActiveMods` key to include a comma seperated list of the IDs of each of the mods. The IDs are the names of the
folders.
