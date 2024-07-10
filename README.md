# docker-laravel
docker laravel

## command 

```sh
docker-compose ps

docker-compose up -d

docker-compose down
```

## port 

```sh
www port 8082

phpmyadmin port 8083
```

## url 

```sh
http://localhost:8082/

http://localhost:8083/
```

## nginx config

```
server {
   charset utf-8;
   client_max_body_size 128M;
   server_name _;
   listen 80;
   root /var/www/html;
   index index.html index.htm index.php;
   server_tokens off;
   #   add_header X-Frame-Options DENY;
   add_header 'Access-Control-Allow-Origin' '*';
   location ~* \.(ico|css|js|gif|jpe?g|png)(\?[0-9]+)?$ {
      expires max;
      log_not_found off;
   }
   location / {
      try_files $uri $uri/ /index.php;
   }
   location ~ \.php$ {
      include fastcgi_params;
      fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
      fastcgi_pass php1:9000;
   }
}
```

