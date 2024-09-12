# TODO
[ ] Setup shared folder via Ansible
[ ] Add Plex to the ansible stuff

# Guides

* [Rip BluRays](https://www.plexopedia.com/plex-media-server/general/how-rip-bluray-discs-stream-plex/)
* [Ripping Instructions](https://www.winxdvd.com/video-transcoder/best-handbrake-settings-for-plex.htm)
* [Plex Docker Compose](https://www.gravee.dev/en/configs/docker-compose/plex/)

# Usage Instructions

## Run Media Server


* Update .env configuration file in root of webnerdbot-deploy

```
claim_code= #get your claim code from here - https://www.plex.tv/claim/
host_tv=D:\medialibrary\tv
host_movies=D:\medialibrary\movies
host_music=D:\medialibrary\music
```

* Run Via Docker Compose
```
docker compose down
docker compose pull
docker compose up -d
docker logs -f plex
```

* Access [Plex](localhost:32400/web)

## Shutdown Media Server

```
docker compose down
```

# Setup Instructions

## Connect to Media Folder

* TBD

## Setup Shared Folder

```bash
Symlink /shared/media to ~/media
sudo apt install samba samba-common-bin

sudo chmod -R 1777 /shared/media/library

sudo vim /etc/samba/smb.conf
[MediaLibrary]
path = /shared/media/library
writeable = yes
browseable = yes
create mask = 0777
directory mask = 0777
public = no
```

* Set Password, add user to password file (psw medialibrary)

```
sudo smbpasswd -a gille
```

* restart samba

```bash
sudo systemctl restart smbd
```