# proxy-vpn-wg
![GitHub Actions Workflow Status](https://img.shields.io/github/actions/workflow/status/rooty/proxy-vpn-wg/docker-image.yml)

## Features

- Supports CONNECT method and forwarding of HTTPS connections
- Supports TLS operation mode (HTTP(S) proxy over TLS)
- Supports client authentication with client TLS certificates
- Supports HTTP/2

## Usage
For run WireGuard prepare  file
- wg.conf file


### Example  wg.conf file
```
[Interface]
PrivateKey = AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA=
Address = 10.0.0.231/32
DNS = 10.0.0.1

[Peer]
PublicKey = BBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBBB=
PresharedKey = CCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCC=
AllowedIPs = 0.0.0.0/0
Endpoint = 111.222.3333.4444:15288
PersistentKeepalive = 25
```

### Exmaple compose.yaml file
```yaml
services:
  proxy:
    image: ghcr.io/rooty/proxy-vpn-wg:latest
    restart: always
    privileged: true
    dns:
      - 8.8.8.8
    volumes:
        - /path/to/wg.conf:/etc/wireguard/wg0.conf:ro
    ports:
       - 127.0.0.1:8888:8888
    networks:
         - vpn-net
```


