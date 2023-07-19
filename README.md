# Lotusboard
### Restore Backup
```
tar xf lotusboard-backup.tar.gz
cd lotusboard-docker
docker compose up -d
```
# What has been modified

Hysteria
 - Multiple bugs fixed

Vmess
 - TLS fingerprint, firefox by default
 - Websocket ed4096(0rtt enabled for xray)
 - Subscription info was translated into English
 - Auto zero encryption when TLS enabled

Subscription:
```
version: '3'
services:
  www:
    image: ghcr.io/lotusproxy/sakuraneko
    # build: https://github.com/lotusproxy/sakuraneko.git <- if you're ARM user please replace image line with this
    volumes:
      - './www:/www'
      - './wwwlogs:/wwwlogs'
      - './caddy.conf:/run/caddy/caddy.conf'
      - './supervisord.conf:/run/supervisor/supervisord.conf'
      - './crontabs.conf:/etc/crontabs/root'
      - './.caddy:/root/.caddy'
    ports:
      - '12500:80' <--- Modify if you want to reverse proxy, Eg (443tls -> caddy -> 8080), format is host:container
    restart: always
    links:
      - mysql
  mysql:
    image: mysql:5.7.29
    # image: arm64v8/mysql:latest  <- if you're ARM user please replace image line with this
    volumes:
      - './mysql:/var/lib/mysql'
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: 'lahiru1998'
      MYSQL_DATABASE: lahiru1998

```
 - Simplified the default clash config

# Install with docker

[Read Docs](https://github.com/lotusproxy/lotusboard-docker/wiki)
