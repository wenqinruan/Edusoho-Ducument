#Edusoho Ubuntu安装教程

**安装PHP以及一些必备的扩展:**

    sudo apt-get install php5 php5-cli php5-curl php5-fpm php5-intl php5-mcrypt php5-mysqlnd php5-gd

**安装nginx**

    sudo apt-get install nginx

**安装mysql**

    sudo apt-get install mysql-server

**创建数据库**

    mysql -u root -p root
    create dabase edusoho

**安装EduSoho源码**

    cd /var/www
    sudo git clone http://gitlab.howzhi.net/edusoho/edusoho.git
    sudo chown $USER:$USER edusoho/
    cd edusoho

**安装composer**

    curl -sS https://getcomposer.org/installer | php
    sudo mv composer.phar /usr/local/bin/composer

**初始化项目**

    composer install
    app/console doctrine:migrations:migrate
    app/console topxia:init

**配置nginx**

    cd /etc/nginx/sites-enabled/
    sudo vim edusoho.conf

添加以下配置
    
    server {
        listen 80;

        server_name esdev.com;

        root /var/www/edusoho/web;

        access_log /var/log/nginx/edusoho.access.log;
        error_log /var/log/nginx/edusoho.error.log;
        
        location / {
            index app_dev.php;
            try_files $uri @rewriteapp;
        }

        location @rewriteapp {
            rewrite ^(.*)$ /app_dev.php/$1 last;
        }

        location ~ ^/udisk {
            internal;
            root /var/www/edusoho/app/data/;
        }

        location ~ ^/(app|app_dev)\.php(/|$) {
            fastcgi_pass   unix:/var/run/php5-fpm.sock;
            fastcgi_split_path_info ^(.+\.php)(/.*)$;
            include fastcgi_params;
            fastcgi_param  SCRIPT_FILENAME    $document_root$fastcgi_script_name;
            fastcgi_param  HTTPS              off;
            fastcgi_param HTTP_X-Sendfile-Type X-Accel-Redirect;
            fastcgi_param HTTP_X-Accel-Mapping /udisk=/var/www/edusoho/web/app/data/udisk;
            fastcgi_buffer_size 128k;
            fastcgi_buffers 8 128k;
        }

        location ~* \.(jpg|jpeg|gif|png|ico|swf)$ {
            expires 3y;
            access_log off;
            gzip off;
        }
        location ~ ^/files/ {
         limit_rate 12k;
        }
        location ~* \.(css|js)$ {
            access_log off;
            expires 3y;
        }

        location ~ ^/files/.*\.(php|php5)$ {
            deny all;
        }

        location ~ \.php$ {
            fastcgi_pass   unix:/var/run/php5-fpm.sock;
            fastcgi_split_path_info ^(.+\.php)(/.*)$;
            include fastcgi_params;
            fastcgi_param  SCRIPT_FILENAME    $document_root$fastcgi_script_name;
            fastcgi_param  HTTPS              off;
        }
    }

**修改fpm运行用户**

    sudo vim /etc/php5/fpm/pool.d/

修改以下参数:

    user = 当前用户
    group = 当前用户
    listen.owner = 当前用户
    listen.group = 当前用户
    listen.mode = 0666


**配置本地host**
    
    sudo vim /etc/hosts

添加一行:`0.0.0.0    esdev.com`

**访问**

[http://esdev.com](http://esdev.com)