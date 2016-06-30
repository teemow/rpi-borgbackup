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

Also see: https://github.com/teemow/docker-rpi-ubuntu
