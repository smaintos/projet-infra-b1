# 1. Instalation de nginx
```
$sudo dnf install nginx
```
```
sudo systemctl enable nginx
sudo systemctl start nginx
```

### Modification des règles de firewall. 

```
sudo firewall-cmd --permanent --add-service=http
```

### Vérification de l'état du firewall.

```
sudo firewall-cmd --permanent --list-all
```

### Relancer le firewall pour confirmer les modifications.

```
sudo firewall-cmd --reload
```

### Vérifier le fonctionement de nginx.

```
systemctl status nginx
```

### Remplacer le `http://ww.exemple.com` par le lien voulus.

```
location /some/path/ {
    proxy_pass http://www.example.com/link/;
}
```

# 2. Installation de Certbot: 
```
sudo dnf install epel-release
```
```
sudo dnf install certbot python3-certbot-nginx
```

### Vérification du firewall.

```
sudo firewall-cmd --permanent --list-all
```

#### **Si le http est manquant :** 

```
sudo firewall-cmd --permanent --add-service=http
```

#### Pour acctiver le https. 

```
sudo firewall-cmd --permanent --add-service=https
```

#### Pour apliquer les changements. 

```
sudo firewall-cmd --reload
```

### Configuration :

```
sudo certbot --nginx -d your_domain -d www.your_domain
```
```
sudo certbot --nginx -d your_domain
```
```
sudo certbot --nginx
```
```
sudo certbot renew --dry-run
```
```
sudo crontab -e
```

# 3. Crontab
```
0 0,12 * * * python -c 'import random; import time; time.sleep(random.random() * 3600)' && certbot renew --quiet
```
```
sudo certbot certonly -d <url_mattermost> -m <ton_mail> --agree-tos --webroot -w /srv/www/letsencrypt
```

### Voici la template certbot pour Mattermost:

```
server {
    server_name <url_mattermost>; 
    
    listen 443 ssl;
    ssl_certificate /etc/letsencrypt/live/<generer_par_certbot>/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/<generer_par_certbot/privkey.pem;
    include /etc/letsencrypt/options-ssl-nginx.conf;
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem;

    location / {
        proxy_pass http://<l'adresse de votre bridge>/;
        proxy_set_header    Host $host;
        proxy_connect_timeout 30;
        proxy_send_timeout 30;
    }
}

server {
    listen 80;
    server_name <url_mattermost>;
    return 301 https://<url_mattermost>$request_uri;

    location ^~ /.well-known/acme-challenge {
        root /srv/www/letsencrypt;
        allow all;
   }
}
```

Merci d'avoir suivis ce guide jusqu'ici ! Retour au [Sommaire](https://github.com/smaintos/projet-infra-b1).
