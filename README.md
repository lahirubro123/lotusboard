# Lotusboard
### UserManual | 用戶手冊

[WIKI](https://github.com/lotusproxy/lotusboard-docker/wiki)

### Go latest-release branch for latest stable, main is for develop purpose | 转到latest-stable分支以获得最新稳定版本，main用于开发目的

# Modified v2board, probably enhancement | 修改后的 v2board，可能是增强版

I have no intention in breaking open source license, but i don't understand them, so if you have some suggestion on this please tell me in issue

我无意破坏开源许可证，但我不理解它们，所以如果您对此有任何建议，请在问题中告诉我

# What has been modified | 修改了什么

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
