## LNMP Docker 集成环境

### Nginx
* `conf/nginx` 下为 nginx 配置文件
* 如果使用 php 解析 则查看 `conf/nginx/php_default.conf`
```shell
location ~ \.php$ {
      # 为 php 容器内运行目录
      root           /app;
      # php 容器 php-fpm 监听端口
      fastcgi_pass   php:9000;
      fastcgi_index  index.php;
      fastcgi_param  PATH_INFO $fastcgi_path_info;
      fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
      include        fastcgi_params;
    }
```

### Php
* `bitnami php` 镜像 内含 `composer`
* 在环境变量里添加
  ```shell
  alias php="docker run --rm -v ${PWD}:/app bitnami/php-fpm:8.1 php"
  ```
  即可使用 `php-cli`
* 在环境变量里添加
  ```shell
  alias composer="docker run --rm -v ${PWD}:/app bitnami/php-fpm:8.1 composer"
  ```
  即可使用 `composer`

### Mysql

### Redis