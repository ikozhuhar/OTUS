#### Nginx & PHP-FPM

```ruby
server {
	listen 443 ssl;
	server_name disk2.mosinzhproekt.ru;
	root /var/www/html/nextcloud;
	index index.php index.html index.htm index.nginx-debian.html

	client_max_body_size 50M;

	error_log /home/deploy/apps/logs/example.error.log;
	access_log /home/deploy/apps/logs/example.access.log;

	ssl_protocols TLSv1.2 TLSv1.3;
	ssl_certificate /etc/nginx/ssl/mosinzhproekt_ru_2026_09_22.crt;
	ssl_certificate_key /etc/nginx/ssl/mosinzhproekt_ru_2026_09_22.key;

	location / {
		try_files $uri $uri/ /index.php$is_args$args;
	}

	location ~ \.php {
		try_files $uri =404;
		fastcgi_split_path_info ^(.+\.php)(/.+)$;
		fastcgi_index index.php;
		include fastcgi_params;
		fastcgi_pass unix:/run/php/php8.2-fpm.sock;
		fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
		fastcgi_param SCRIPT_NAME $fastcgi_script_name;
	}
}
```

```ruby
# https://www.php.net/manual/en/install.fpm.configuration.php
# https://www.php.net/manual/en/install.fpm.configuration.php
```
