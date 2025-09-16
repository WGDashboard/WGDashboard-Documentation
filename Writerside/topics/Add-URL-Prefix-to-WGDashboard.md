# Add URL Prefix to WGDashboard

> Required version: v4.3+

Let's say if you wish to use WGDashboard not in a subdomain, but a prefix, you can do the following. In this example, we want WGDashboard to be hosted under https://wgdashboard.dev/wgdashboard

```nginx
server {
    server_name wgdashboard.dev;

    location /wgdashboard {
        rewrite ^/wgdashboard/(.*)$ /$1 break;
        proxy_pass http://0.0.0.0:10086;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }

    location /static/dist/WGDashboardAdmin/ {
        return 301 /wgdashboard$request_uri;
    }
    location /static/dist/WGDashboardClient/ {
        return 301 /wgdashboard$request_uri;
    }

    location /wgdashboard/static/dist/WGDashboardAdmin/ {
         rewrite ^/wgdashboard(.*)$ $1 break;
         proxy_pass http://0.0.0.0:10086;
    }

    location /wgdashboard/static/dist/WGDashboardClient/ {
         rewrite ^/wgdashboard(.*)$ $1 break;
         proxy_pass http://0.0.0.0:10086;
    }

}
```

Some users might say this is _hack_, I agree, but in order to not use a hack like this, it would require them to re-compile the frontend app whenever that want to change the prefix.

But if you have a better idea, please let me know!