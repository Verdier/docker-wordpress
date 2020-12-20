A ready to use docker-compose project for multiple wordpress.

# How to start?

## Setup environment variables

Copy `.env.example` to `.env`, edit *at least* `MYSQL_ROOT_PASSWORD`, `SERVER_NAME_*` and `MYSQL_PASSWORD_*` variables.

## Generate an SSL certificate

Start generation with `docker-copose up`, when certificates are generated, stop with `Ctrl+C`

## Make some changes

Edit `nginx-conf/default.conf.template`, uncomment ssl lines and comment 8080 lines.

Be careful, keep ${SERVER_NAME_1} as ssl path, even for site 2. If you want separate certificates, modify the `docker-compose`
file certbot command and rerun certbot.

TODO: mount a certbot script to generate both certificates automatically.

## Update `options-ssl-nginx.conf`

```
curl -sSLo nginx-ìncludes/options-ssl-nginx.conf https://raw.githubusercontent.com/certbot/certbot/master/certbot-nginx/certbot_nginx/_internal/tls_configs/options-ssl-nginx.conf
```

## Start the server

Now, start the server expect certbot.

```shell
docker-compose up -d --scale certbot=0
```

Well done, your multiple wordpress SSL sites are successfully running!

# How to renew SSL certificates?

```shell
docker-compose run certbot renew && docker-compose restart webserver
```


