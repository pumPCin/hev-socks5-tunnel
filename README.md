# HevSocks5Tunnel

[![status](https://gitlab.com/hev/hev-socks5-tunnel/badges/master/pipeline.svg)](https://gitlab.com/hev/hev-socks5-tunnel/commits/master)

A tunnel over Socks5 proxy (tun2socks) for Unix.

## Features

* IPv4/IPv6. (dual stack)
* Redirect TCP connections.
* Redirect UDP packets. (Fullcone NAT, UDP in UDP/TCP)
* Linux/Android/FreeBSD/macOS/iOS.

## Benchmarks

See [here](https://github.com/heiher/hev-socks5-tunnel/wiki/Benchmarks) for more details.

### Speed

![](https://github.com/heiher/hev-socks5-tunnel/wiki/res/upload-speed.png)
![](https://github.com/heiher/hev-socks5-tunnel/wiki/res/download-speed.png)

### CPU usage

![](https://github.com/heiher/hev-socks5-tunnel/wiki/res/upload-cpu.png)
![](https://github.com/heiher/hev-socks5-tunnel/wiki/res/download-cpu.png)

### Memory usage

![](https://github.com/heiher/hev-socks5-tunnel/wiki/res/upload-mem.png)
![](https://github.com/heiher/hev-socks5-tunnel/wiki/res/download-mem.png)

## How to Build

### Unix

```bash
git clone --recursive https://github.com/heiher/hev-socks5-tunnel
cd hev-socks5-tunnel
make
```

### Android

```bash
mkdir hev-socks5-tunnel
cd hev-socks5-tunnel
git clone --recursive https://github.com/heiher/hev-socks5-tunnel jni
ndk-build
```

## How to Use

### Config

```yaml
tunnel:
  # Interface name
  name: tun0
  # Interface MTU
  mtu: 9000
  # IPv4 address
  ipv4: 198.18.0.1
  # IPv6 address
  ipv6: 'fc00::1'

socks5:
  # Socks5 server port
  port: 1080
  # Socks5 server address (ipv4/ipv6)
  address: 127.0.0.1
  # Socks5 UDP relay mode (tcp|udp)
  udp: 'tcp'
  # Socks5 server username
# username: 'username'
  # Socks5 server password
# password: 'password'

#misc:
   # task stack size (bytes)
#  task-stack-size: 20480
   # connect timeout (ms)
#  connect-timeout: 5000
   # read-write timeout (ms)
#  read-write-timeout: 60000
   # stdout, stderr or file-path
#  log-file: stderr
   # debug, info, warn or error
#  log-level: warn
   # If present, run as a daemon with this pid file
#  pid-file: /run/hev-socks5-tunnel.pid
   # If present, set rlimit nofile; else use default value
#  limit-nofile: 65535
```

### Run

```bash
bin/hev-socks5-tunnel conf/main.yml

# Bypass upstream socks5 server
sudo ip route add SOCKS5_SERVER dev DEFAULT_IFACE metric 10
sudo ip -6 route add SOCKS5_SERVER dev DEFAULT_IFACE metric 10

# Route others
sudo ip route add default dev tun0 metric 20
sudo ip -6 route add default dev tun0 metric 20
```

### Android VPN

* [SocksTun](https://github.com/heiher/sockstun)

## Contributors

* **daemooon** - https://github.com/daemooon
* **hev** - https://hev.cc

## License

MIT
