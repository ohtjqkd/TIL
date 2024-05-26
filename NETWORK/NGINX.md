# NGINX

nginx 웹서버를 설치 및 설정하는 방법

## Installation

```bash
sudo apt-get update
sudo apt-get install nginx
```

## Configuration

configuration 파일은 `/etc/nginx/nginx.conf`에 위치한다.

server block은 `/etc/nginx/sites-available/`에 위치한다.
server block 작성 예시 (proxy_pass with certbot)
  
```conf
server {
  access_log /var/log/nginx/access.log test;
	error_log /var/log/nginx/error.log;

  client_max_body_size 50M;
  client_body_buffer_size 50k;

	listen [::]:443 ssl ipv6only=on; # managed by Certbot
	listen 443 ssl; # managed by Certbot
	ssl_certificate /etc/letsencrypt/live/domain.com/fullchain.pem; # managed by Certbot
	ssl_certificate_key /etc/letsencrypt/live/domain.com/privkey.pem; # managed by Certbot
	include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
	ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot
    server_name example.com;
    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
		    proxy_set_header X-NginX-Proxy true;
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
        include /etc/nginx/proxy_params;
        proxy_redirect off;
		    charset utf-8;
    }
}
```

available site를 enable하려면 다음과 같이 실행한다.

```bash
sudo ln -s /etc/nginx/sites-available/server.conf /etc/nginx/sites-enabled/
```