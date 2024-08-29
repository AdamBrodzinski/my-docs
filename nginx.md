# Nginx Configs

Note, this is not an exhaustive list of instructions, rather bits that I tend to forget that can be used to piece together the start of a setup.

## Setup

Install the package, Debian will register this with systemctl and start it automatically
`apt install nginx`

Remove the default config from available/enabled and placeholder html

```
trash /etc/nginx/sites-available/default
trash /etc/nginx/sites-enabled/default
trash /var/www/hmtl
```

## Static site config

Add a config for the domain foo.com:

```
server {
    listen 80;
    server_name foo.com www.foo.com;

    root /var/www/foo.com;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

Copy site files to var:

```
sudo mkdir -p /var/www/foo.com
sudo cp build/* /var/www/foo.com/
```

## Test

Test the new config and then restart nginx:

```
sudo nginx -t
systemctl reload nginx
```
