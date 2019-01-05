---
layout: page
title: nginx 常用配置
permalink: /linux/2018_3_14
---

### nginx 常用配置

#### rewrite url跳转
```
$ rewrite ^(.*)$  https://$host$1 permanent;
```

#### rewrite 路由覆盖
```
location ~ ^/huobi/.*$ {
        rewrite /huobi/(.+)$ /$1 break;
        proxy_pass https://api.huobi.pro;
}
```

#### 单页面重定向
```
location / {
    try_files $uri $uri/ /index.html;
}
```

#### api代理
```
location ~ ^/(api|public)/.*$ {
    #proxy_set_header       Host $host;
    #proxy_set_header       X-Real-IP $remote_addr;
    proxy_set_header       X-Forwarded-For $proxy_add_x_forwarded_for;

    #proxy_pass             http://127.0.0.1:8088;
    proxy_pass             http://api.example.com;
}
```

#### 端口代理
```
location / {
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection "upgrade";
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-Proto http;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header Host $host;

    proxy_http_version 1.1;

    # 端口代理转发
    proxy_pass http://127.0.0.1:8989;
    proxy_buffering            off;
    chunked_transfer_encoding  off;
}
```

#### 静态文件缓存
```
location ~ .*\.(js|css|gif|jpg|jpeg|png|svg|woff|ttf|eot|map|ico)$ {
    expires 3d;
    root /data/portal/qtin-front-portal-x/dist;
}
```

#### 文件后缀拦截
```
location ~ .*\.(txt|doc)$ {  
    root   /data/portal/qtin-front-portal-x/dist;  
    deny all;  
} 
```

#### error_page
```
error_page 403 404 500 502 /error.html;	
```

#### 允许跨域
```
add_header     Access-Control-Allow-Origin *;
```

#### upstream
```
upstream api-sexyvc {
    ip_hash;
    server 127.0.0.1:8088 max_fails=3 fail_timeout=10s;
    keepalive 512;
} 
```

#### 相关参数配置
```
#nginx 区分终端类型
if ($http_user_agent ~* (.*Android.*)|(.*iPhone.*)) {
    rewrite (.*) http://m.sexyvc.com;
}

if (!-f $request_filename){
    rewrite (.*) /index.php last;
}

#定义变量 $path_info ，用于存放pathinfo信息
set $path_info "";

#定义变量 $real_script_name，用于存放真实地址
set $real_script_name $fastcgi_script_name;

#如果地址与引号内的正则表达式匹配
if ($fastcgi_script_name ~ "^(.+?\.php)(/.+)$") {
    #将文件地址赋值给变量 $real_script_name
    set $real_script_name $1;

    #将文件地址后的参数赋值给变量 $path_info
    set $path_info $2;
}

#配置fastcgi的一些参数
fastcgi_param SCRIPT_FILENAME $document_root$real_script_name;
fastcgi_param SCRIPT_NAME $real_script_name;
fastcgi_param PATH_INFO $path_info;
```

#### location 重命名
```
location @jenkins {
    sendfile off;
    proxy_pass         http://127.0.0.1:8080;
    proxy_redirect     default;
    
    proxy_set_header   Host             $host;
    proxy_set_header   X-Real-IP        $remote_addr;
    proxy_set_header   X-Forwarded-For  $proxy_add_x_forwarded_for;
    proxy_max_temp_file_size 0;
    
    #this is the maximum upload size
    client_max_body_size       10m;
    client_body_buffer_size    128k;
    
    proxy_connect_timeout      90;
    proxy_send_timeout         90;
    proxy_read_timeout         90;
    
    proxy_buffer_size          4k;
    proxy_buffers              4 32k;
    proxy_busy_buffers_size    64k;
    proxy_temp_file_write_size 64k;
}

location / {
    # Optional configuration to detect and redirect iPhones
    if ($http_user_agent ~* '(iPhone|iPod)') {
      rewrite ^/$ /view/iphone/ redirect;
    }

    try_files $uri @jenkins;
}
```

#### body size 上传body限制
```
client_max_body_size 100m;
```

#### 配置模块化引入
```
include /etc/nginx/conf.d/*.conf;
```

#### gzip 配置
```
gzip  on;
gzip_min_length 1000;
gzip_proxied    expired no-cache no-store private auth;
gzip_types      application/javascript text/css text/javascript text/plain application/xml;
```

#### https
```
listen       443 ssl;
server_name  www.example.com;

root /data/front/noise;
index index.html; 

ssl_certificate     /opt/ssl/noise/full_chain.pem;
ssl_certificate_key /opt/ssl/noise/private.key;
```