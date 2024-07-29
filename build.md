# Build

## Alpine 3.19 LXC install

```
wget https://github.com/fliberd/amneziawg-go-lxc/raw/master/images/alpine-3.19-amd64.tar.xz -O /var/lib/vz/template/cache/alpine-3.19-amd64.tar.xz
```
## Create LXC

 CPU | RAM | Storage
--- | --- | ---
  1 core| 2 GB | 5 GB

## Edit config

```
nano /etc/pve/lxc/<LXD-ID>.conf
```
```
lxc.cgroup.devices.allow: c 10:200 rwm
lxc.mount.entry: /dev/net dev/net none bind,create=dir
```

## Build Go lang
```
apk add --no-cache make musl-dev gcc-go alpine-sdk bash
```
```
wget -c https://go.dev/dl/go1.20.4.src.tar.gz && tar xzvf go1.20.4.src.tar.gz
```
```
cd go/src && ./make.bash
```
```
cd ~ && cp -r go /opt
```
```Please wait...
ln -s /opt/go/bin/gofmt /usr/local/bin/gofmt && ln -s /opt/go/bin/go /usr/local/bin/go
```
```
apk del gcc-go
```

## Build amneziawg-go

```
cd ~ && git clone https://github.com/fliberd/amneziawg-go -b v0.2.4
```
```
cd amneziawg-go && go env && go env -w GOMODCACHE=$HOME/golang/pkg/mod
```
```
make && make install
```

## Create TUN device

```
mkdir /dev/net && mknod /dev/net/tun c 10 200
```
## Build amneziawg-tools
```
wget https://github.com/fliberd/amneziawg-tools/archive/refs/tags/v1.0.20240213.tar.gz
```
```
tar xzvf v1.0.20240213.tar.gz
```
```
cd amneziawg-tools-1.0.20240213/src/
```
```
make && make install
```

