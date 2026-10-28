# Piwigo with nginx, mariadb and cloudflare tunell

1. ### If you create new database, go to folder and delete piwigo database.inc.php Location = piwigo-data -> piwigo -> local -> config -> database.inc.php

2. ### Create .env file.

piwigo_port=
db_user_password=
timezone=
PIWIGO_UID=1000
PIWIGO_GID=1000
#### If use cloudflare tunnel
CF_TUNNEL_TOKEN=

3. #### Nginx config file nginx.conf is for cloudflare tunnel.
edit conf file "server_name photo.piwigo.lv" and hostname -> http://nginx:80 add to Cloudflare Zero Trust panel.

4. ### Without cloudflare tunnel, local build.
docker compose up -d --build nginx

5. ### Open piwigo
http://localhost:8080

6. ### Manual type database form:
localhost database change to piwigo-db

### Logs:
docker compose logs -f piwigo-db

### Create backup:
docker compose exec -T piwigo-db sh -c 'mariadb-dump -upiwigo_user -ppiwiStrong!2026!@!! --single-transaction piwigo_database' > piwigo-backup.sql

### Restore database:
docker compose up -d piwigo-db
docker compose exec -T piwigo-db sh -c 'mariadb -upiwigo_user -ppiwiStrong!2026!@!! piwigo_database'

### Delete all files and volumes:
docker compose down -v

### Up docker compose with cloudflare tunnel:
docker copmopse up -d

#### If migrate server - Create folder "initdb". Copy your piwigo-backup.sql and use "docker compose down -v" and "docker compose up -d"