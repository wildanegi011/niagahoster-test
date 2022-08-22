# BoxBilling Docker

This is step by step for install boxbilling with docker

## Requirements

- Docker [instructions](https://www.docker.com/get-started)
- Docker Compose [here](https://docs.docker.com/compose/)
- Boxbilling [here](https://www.boxbilling.org/)

## Installation

1. Download [BoxBilling latest release](https://www.boxbilling.org/)
2. Make a folder named whatever is up to you, i make folder name `niagahoster-test`
3. make folder public and extract downloaded BoxBilling into public folder inside
4. Copy `bb-config-sample.php` to `bb-config.php`
5. Make `config` folder on the project root, and add `nginx`, and `mysql` folders inside
6. Make file default.conf in nginx folder

```
server {
    listen       80;
    server_name  localhost;

    index index.php index.html;
    error_log  /var/log/nginx/error.log;
    access_log /var/log/nginx/access.log;
    root /var/www/public;

    location ~ \.php$ {
        try_files $uri =404;
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass app:9000;
        fastcgi_index index.php;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_param PATH_INFO $fastcgi_path_info;
    }
    location / {
        try_files $uri $uri/ /index.php?$query_string;
        gzip_static on;
    }
}

```

7. Make file `structure.sql`, this file used for table and seeder initialization when docker run
8. Make file `Dockerfile` for PHP image
9. Make file `docker-compose.yml`
10. Now run `docker-compose-up -d --build` and let docker build images and containers.
11. Installation are done and we should remove `/var/www/public/install` folder, change `/var/www/public/bb-config.php` to readonly (CHMOD 644), and setup cron job `*/5 * * * * php /var/www/public/bb-cron.php` on our webserver docker entrypoint.
12. To check on installation go to `http://localhost:8004/bb-admin/staff/login` for administrator login
    this is credentials for login

```
    Email : admin@gmail.com
    Password : rahasia
```

# Landing Page on Docker

1. cd `landing-page`
2. Make file `Dockerfile`
3. Make file `docker-composer.yml`
4. In terminal `docker-compose up -d`
5. After docker up, landing page can be access in `http://localhost:8009/`

# Mockend

This is mock api you can see documentation in [mockend](https://mockend.com/)
for example api price [get price api](https://mockend.com/wildanegi011/niagahoster-test/prices)

# Netlify

you can see documentation in [netlify](https://www.netlify.com)
you olso can access this [landing page](https://dainty-gnome-46ba36.netlify.app)/
