# As simple an example of a laravel app as I have come up with.

Steps to get working:

# Simple

1. Clone the repo:
```bash
Git clone git@github.com:raydennis/docker-example-laravel.git
```

2. Build the container:
```bash
docker build -t laravel-app .
```

3. Run the container on port 80:
```bash
docker run -dit -p 80:80 laravel-app
```

# Simple w/ reverse proxy (ngingx)

1. Clone the repo:
```bash
Git clone git@github.com:raydennis/docker-example-laravel.git
```

2. Run the reverse proxy on port 80:
```bash
docker run -d -p 80:80 -v /var/run/docker.sock:/tmp/docker.sock:ro jwilder/nginx-proxy
```

3. Build the container:
```bash
docker build -t laravel-app .
```

4. Run the container without a port.  The reverse proxy will handle the routing:
```bash
docker run -dit -e VIRTUAL_HOST=example.com laravel-app
```

# Troubleshooting
If you're having issues with composer, you can try the following to do a reset and start over

```bash
cd /var/www/html/$Directory; \
rm -rf composer.lock; \
/usr/local/bin/composer install; \
mkdir /var/www/html/coa-requests.unm.edu/storage/framework/cache/data; \
php artisan key:generate; \
php artisan clear-compiled; \
php artisan cache:clear; \
php artisan route:clear; \
php artisan view:clear; \
php artisan config:clear; \
php artisan config:cache"
```
