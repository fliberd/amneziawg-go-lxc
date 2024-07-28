# amneziawg-go-lxc 
Amnezia WG Go in LXC container for Proxmox

## Quick setup 

```bash
wget -qO- https://raw.githubusercontent.com/fliberd/amneziawg-go-lxc/main/setup.sh | bash
``` 

## Build

### Alpine 3.19 LXC install

```
wget https://github.com/fliberd/amneziawg-go-lxc/raw/master/images/alpine-3.19-amd64.tar.xz -O /var/lib/vz/template/cache/alpine-3.19-amd64.tar.xz
```
### Setting up

### Build Go lang
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
cp -r go /opt
```
```
ln -s /opt/go/bin/gofmt /usr/local/bin/gofmt && ln -s /opt/go/bin/go /usr/local/bin/go
```
```
apk del gcc-go
```


*Made by Fliberd,
forked from [Amnezia-vpn](https://github.com/amnezia-vpn)*
