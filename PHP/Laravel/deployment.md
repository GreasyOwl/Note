# Laravel 8 部署到正式環境

## Server Requirements

```
PHP >= 7.3

extension:
    bcmath
    ctype
    curl
    fileinfo
    gd2
    json
    mbstring
    openssl
    PDO
    pdo_mysql
    tokenizer
    xml
```

## Server Configuration

```
// Nginx

server {
    listen 80;
    listen [::]:80;
    server_name example.com;
    root /srv/example.com/public;

    add_header X-Frame-Options "SAMEORIGIN";
    add_header X-Content-Type-Options "nosniff";

    index index.php;

    charset utf-8;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location = /favicon.ico { access_log off; log_not_found off; }
    location = /robots.txt  { access_log off; log_not_found off; }

    error_page 404 /index.php;

    location ~ \.php$ {
        fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
        include fastcgi_params;
    }

    location ~ /\.(?!well-known).* {
        deny all;
    }
}
```

## Optimization

```shell
> composer install --optimize-autoloader --no-dev
> php artisan config:cache
> php artisan route:cache
> php artisan view:cache
```

## Environment

```javascript
APP_ENV = production;
APP_DEBUG = false;
```
