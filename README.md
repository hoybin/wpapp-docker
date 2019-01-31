# WPAPP DOCKER

Rapidly deploy LNMP services for WordPress.

## Get

Make sure you have the docker package installed on your machine before you start, then continue to:

```bash
git clone https://github.com/hoybin/wpapp-docker.git docker
cd docker
```

## Configure

1. Create **.env** file for docker-compose

```bash
cp .env-dist .env
```

    Modify it to set values of parameters, and use a [personal token](https://github.com/settings/tokens) you generate on github.com as value of **GITHUB_API_TOKEN** in the file.

2. Preset the database initialization script files

    *.sql files in **./mysql/initdb.d/** will be executed when mysql first start, please ensure the database info in these files are consistent with the settings in the .env file above.

3. Configure nginx virtual hosts

    Nginx virtual host configuration files is in **./nginx/conf.d/**, you can refer to [official recommended configuration](https://github.com/yiisoft/yii2/blob/master/docs/guide/start-installation.md#user-content-recommended-nginx-configuration-) for modifications.

## Startup

Okay, the trouble is over, just one line missing, let's get started:

```bash
docker-composer up -d
```

For the first time, it takes a little time, instead of having a cup of coffee and waiting for it to be finished.

## Deploy

Place the code in the `~/www/wpapp/` directory specified by variable `DOCUMENT_ROOT_PATH` in .env file, then open the browser and visit the following addresses:

- app: http://wpapp.com:8030
- phpmyadmin: http://localhost:8031

Ports 8030 and 8031 are already set in the .env file, and you should remember.

## Control

A few commands to know:

```bash
# stop services
docker-compose stop

# start services
docker-compose start

# restart services
docker-compose restart
```

More on docker-compose: https://docs.docker.com/compose

## Proxy

Maybe you need to access applications in containers through reverse proxy of nginx on host:

```bash
sudo cp nginx-proxy.conf /etc/nginx/conf.d/wpapp.conf
sudo nginx -ts reload
```

then access the following addresses in the browser:

- app: http://wpapp.com
- phpmyadmin: http://pma.wpapp.com

---

Congratulations! Your code is running ...
