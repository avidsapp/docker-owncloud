# Dockerized Owncloud

## Setup
1. `git clone https://github.com/avidsapp/docker-owncloud.git owncloud`
1. `cd owncloud`
1. `sudo cp .env.example .env && sudo nano .env`
1. `sudo cp backup.env.example backup.env && sudo nano backup.env`
1. `docker-compose up -d`

## Backups

[Upstream Repo](https://github.com/offen/docker-volume-backup#manually-triggering-a-backup)

### External USB Drives
To grant read/write access to all USB devices:
1. `sudo nano /etc/udev/rules.d/99-perm.rules`:
    ```
    SUBSYSTEM=="usb", OWNER="<NON_ROOT_USER>"
    ```
1. Reboot - `sudo reboot`
1. [More granular device control](https://ramonh.dev/2020/09/22/usb-device-linux-startup/)
1. Symlink the backups for ease of access - `ln -s /media/usb2/backups/ ~/backups`

### Manually run a backup
```
docker exec backup_media backup
docker exec backup_mariadb backup
docker exec backup_redis backup
```
