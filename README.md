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
location / {
   proxy_pass http://10.104.3.29:8081;
   # proxy_set_header Host $host;
   proxy_set_header Host $http_host;
   proxy_set_header X-Forwarded-Proto $scheme;
   proxy_set_header X-Real-IP $remote_addr;
   proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
}
```

## V 2 dbadmin

```
location / {
    proxy_buffers 8 8k;
    proxy_buffer_size 8k;
    proxy_pass http://localhost:8009/;
    proxy_set_header Host $host;
    proxy_buffering on;
    proxy_cache_valid 200  1d;
    proxy_cache_use_stale  error timeout invalid_header updating http_500 http_502 http_503 http_504;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
}
```

## nginx

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

