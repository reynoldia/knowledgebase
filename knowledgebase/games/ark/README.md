# ARK: Survival Evolved

## Installation

https://ark.fandom.com/wiki/Dedicated_server_setup

`steamcmd +login anonymous +force_install_dir <install_dir> +app_update 376030 +quit`

Create a file named /etc/systemd/system/ark-dedicated.service with the following contents:
```ini
[Unit]
Description=ARK: Survival Evolved dedicated server
Wants=network-online.target
After=syslog.target network.target nss-lookup.target network-online.target

[Service]
ExecStartPre=/home/steam/steamcmd +login anonymous +force_install_dir /home/steam/servers/ark +app_update 376030 +quit
ExecStart=/home/steam/servers/ark/ShooterGame/Binaries/Linux/ShooterGameServer TheIsland?listen?SessionName=<session_name> -server -log
WorkingDirectory=/home/steam/servers/ark/ShooterGame/Binaries/Linux
LimitNOFILE=100000
ExecReload=/bin/kill -s HUP $MAINPID
ExecStop=/bin/kill -s INT $MAINPID
User=steam
Group=steam

[Install]
WantedBy=multi-user.target
```
