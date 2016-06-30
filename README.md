# Create a borgbackup container for the Raspberry Pi

Raspbian:jessie does not have borgbackup packages. So I've just built an Ubuntu container.

Download the image:

```
docker pull teemow/rpi-borgbackup
```

Create your own image

```
docker build -t rpi-borgbackup .
```

# Run

```
/usr/bin/docker run --rm --name=borgbackup --net=host \
    -v /root/.ssh:/root/.ssh \
    -v /var/lib/:/backup/var/lib/ \
    -v /home/:/backup/home/ \
    -v /etc/:/backup/etc/ \
    -v /usr/local/:/backup/usr/local/ \
    --entrypoint=/bin/bash \
    teemow/rpi-borgbackup -c "/usr/bin/borg create \
    --compression zlib,6 \
    my-repository-server::my-tag-$(date +%%Y-%%m-%%d) \
    /backup/var/lib/ \
    /backup/home/ \
    /backup/etc/ \
    /backup/usr/local/ \
    --exclude '/backup/home/*/.cache'"
```

Also see: https://github.com/teemow/docker-rpi-ubuntu
