# NGINX

Template 1 (wdds.ml) technologies : `https` `upstream proxy` `basic-auth` 

```nginx
location ^~ /log {
     alias /srv/logs/;
}
location ^~ /fig {
    alias /srv/shiny-server/fig/;
}
location / {
    proxy_pass http://127.0.0.1:3838;
    auth_basic           "Restricted Access";
    auth_basic_user_file /etc/apache2/.htpasswd;
}
    listen [::]:443 ssl ipv6only=on; # managed by Certbot
    listen 443 ssl; # managed by Certbot
    ssl_certificate /etc/letsencrypt/live/wdds.ml/fullchain.pem; # managed by Certbot
    ssl_certificate_key /etc/letsencrypt/live/wdds.ml/privkey.pem; # managed by Certbot
    include /etc/letsencrypt/options-ssl-nginx.conf; # managed by Certbot
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; # managed by Certbot
}
server {
    if ($host = www.wdds.ml) {
        return 301 https://$host$request_uri;
    } # managed by Certbot
    if ($host = wdds.ml) {
        return 301 https://$host$request_uri;
    } # managed by Certbot
        listen 80 default_server;
        listen [::]:80 default_server;
        server_name wdds.ml www.wdds.ml;
    return 404; # managed by Certbot
}
```

