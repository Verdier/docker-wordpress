A ready to use docker-compose project for multiple wordpress sites over SSL.

# How to start?

## 1. Setup environment variables

Copy `.env.example` to `.env`, edit **at least** `MYSQL_ROOT_PASSWORD`, `SERVER_NAME_*` and `MYSQL_PASSWORD_*` variables.

## 2. Generate an SSL certificate

Start certificates generation with `docker-copose up`. 
When certificates are generated, stop with `Ctrl+C`

## 3. Enable sites

Enable sites by copying `sites.conf.templates` into templates:

```shell
cp -f nginx/available/sites.conf.template nginx/templates/
```

## 4. Start the server

Start all services expect certbot.

```shell
docker-compose up -d --scale certbot=0
```

Well done, your multiple wordpress SSL sites are successfully running!

# How to renew SSL certificates?

```shell
docker-compose run certbot renew && docker-compose restart webserver
```


