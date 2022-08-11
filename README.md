# Introduction
Docker with 
- Elasticsearch 6.8
- Laravel 9.11
- MySql 8
- Nginx
- PHP 8.1
- ReactJs Apps with Node 14
- Redis

## Install

### Docker: 
[Installation Guide](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04-pt)

### Docker-compose:
[Installation Guide](https://phoenixnap.com/kb/install-docker-compose-on-ubuntu-20-04)

### Add-on command to docker installation 
```bash
sudo chown $USER /var/run/docker.sock
```
---

### Cloning projects:
- Docker directory
```bash
git clone git@github.com:guigald/docker-boilerplate.git docker
```
- Enter the docker folder
```bash
cd docker
```
- Api `PHP`
```bash
git clone git@github.com:guigald/api-boilerplate.git api
```
---

## Projects

### Docker

#### Copy .env file
```bash
cp api/.env.local api/.env
```
---

#### Build Docker containers
```bash
docker-compose build
```
---

#### Elasticsearch
Set max map count to elasticsearch work:
```bash
sudo sysctl -w vm.max_map_count=262144
```
References [here ***`(elastic.co)`***](https://www.elastic.co/guide/en/elasticsearch/reference/current/vm-max-map-count.html) and [here for definitive configuration ***`(stackoverflow.com)`***](https://stackoverflow.com/questions/42889241/how-to-increase-vm-max-map-count)

---

#### Start containers
```bash
docker-compose up -d
```

##### Configuring Api
Get into the api container:
```bash
docker exec -it api bash
```
---

Inside the api container, run composer and artisan commands to initialize the api and exit:
```bash
composer install # install dependencies
composer dump-autoload # reveal the untracked classes
php artisan key:generate # generate an application key
php artisan migrate # initialize database structure and initial data
php artisan jwt:secret # generate a jwt secret to api authentication
php artisan storage:link # enable public storage for local temporary files 
exit
```
---

## Access
### WEB
- Web: http://localhost:3101
- Backoffice: http://localhost:3102
- API: http://localhost:8000/v1

### Mysql
- MySql: Get the host by running the command below. Username, port and password have already been defined in .env file 
```bash
docker inspect db | grep IPAddress
```

### Elasticsearch
- API:  http://localhost:9222
---

## Before committing your changes

### API
Run the command below to adjust the code according to PSR-1 and PSR-12
```bash
docker exec -it api bash ./contrib/csfix.sh # Api
```
