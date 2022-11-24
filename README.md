# docker-project

## clouddrive

```
docker run -d \
      --name clouddrive \
      --restart unless-stopped \
      -v /volume1/docker/CloudNAS:/CloudNAS:shared \
      -v /volume1/docker/CloudNAS/config:/Config \
      -v /volume1/docker/CloudNAS/share:/media:shared \
      --network host \
      --pid host \
     --privileged \
     --device /dev/fuse:/dev/fuse \
     cloudnas/clouddrive
```

* /volume1/docker/CloudNAS 为存放配置文件、挂载的实际目录



## speedtest

```
docker run -d -t --name speedtest -p 6688:80 ilemonrain/html5-speedtest:latest
```

* 6888 为web界面访问端口



## aria2+ariang

```
docker run -d \
  --name aria2-pro \
  --restart unless-stopped \
  --log-opt max-size=1m \
  -e PUID=$UID \
  -e PGID=$GID \
  -e UMASK_SET=022 \
  -e RPC_SECRET=aabbccdd \
  -e RPC_PORT=6800 \
  -p 6800:6800 \
  -e LISTEN_PORT=6888 \
  -p 6888:6888 \
  -p 6888:6888/udp \
  -v /volume2/DSM7/Downloads/aria2-config:/config \
  -v /volume2/DSM7/Downloads:/downloads \
  p3terx/aria2-pro:latest
```

* /volume2/DSM7/Downloads/aria2-config 为存放配置文件的实际目录
* /volume2/DSM7/Downloads 为下载的实际目录


```
docker run -d \
  --name ariang \
  --log-opt max-size=1m \
  --restart unless-stopped \
  -p 6880:6880 \
  p3terx/ariang:latest
```

* 6880 为web界面访问端口



## qbittorrent

```
docker run -d \
    --name qbittorrent \
    --restart unless-stopped \
    --network host \
    -e PUID=$UID \
    -e PGID=$GID \
    -e UMASK_SET=022 \
    -e TZ=Asia/Shanghai \
    -e WEBUI_PORT=8080 \
    -p 6881:6881 \
    -p 6881:6881/udp \
    -p 8080:8080 \
    -v /volume2/DSM7/Downloads/qbt-config:/config \
    -v /volume2/DSM7/Downloads:/downloads \
    linuxserver/qbittorrent:latest
```

* volume2/DSM7/Downloads/qbt-config 为存放配置文件的实际目录
* volume2/DSM7/Downloads 为下载的实际目录



## Emby


```
docker run -d --name emby \
  --restart unless-stopped \
  --env UID=0 \
  --env GID=0 \
  --env GIDLIST=0 \
  -p 8096:8096 \
  -v /volume2/SATA1/Emby/config:/config \
  -v /volume2/SATA1:/mnt/share1 \
  --device /dev/dri/renderD128:/dev/dri/renderD128 \
  --device /dev/dri/card0:/dev/dri/card0 \
  lovechen/embyserver:latest
```

* /volume2/SATA1/Emby/config 为存放配置文件的实际目录
* /volume2/SATA1 为多媒体文件所在的实际目录



## jellyfin

```
docker run -d --name jellyfin \
  --restart unless-stopped \
  --env UID=0 \
  --env GID=0 \
  --env GIDLIST=0 \
  -p 8096:8096 \
  -v /mnt/sdc1/jellyfin/config:/config \
  -v /mnt/sdc1:/media \
  --device /dev/dri/renderD128:/dev/dri/renderD128 \
  --device /dev/dri/card0:/dev/dri/card0 \
  jellyfin/jellyfin
```

* /mnt/sdc1/jellyfin/config 为存放配置文件的实际目录
* /mnt/sdc1 为多媒体文件所在的实际目录



