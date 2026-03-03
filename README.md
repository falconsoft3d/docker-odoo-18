# docker-odoo-18
Cómo instalar odoo 18 con docker

## Actualizamos el sistema

```linux
apt-get update && apt-get upgrade -y
```


# Clonar el repo
```
git clone https://github.com/falconsoft3d/docker-odoo-18.git
cd docker-odoo-18
```

# Levantar el docker
```
apt install docker-compose
apt-get update && apt-get upgrade -y
docker-compose up -d
```

# Levantar el docker
```
cd /root
docker-compose down
docker-compose up -d
```

# Si te da error filestore
```
mkdir -p filestore
sudo chown -R 101:101 filestore
sudo chmod -R 775 filestore
docker-compose down
docker-compose up -d
```

# Listar los dockers
```
docker ps
```

# error comun
```
docker-compose exec -u 0 odoo bash -lc "mkdir -p /var/lib/odoo/sessions && chown -R odoo:odoo /var/lib/odoo && chmod -R 700 /var/lib/odoo/sessions"
docker-compose restart odoo
```

# reiniciar el docker 
```
docker-compose restart odoo
docker-compose logs -f odoo
```

# ver los logs
```
docker-compose logs --tail=200 odoo
docker logs --tail=30 odoo18
docker-compose logs -f db
```

## Instalamos ngix para cambiar el puerto
```linux
sudo apt-get install nginx -y
cd /etc/nginx/sites-available
git clone https://github.com/falconsoft3d/ngix-para-odoo-erp/
cd ngix-para-odoo-erp/
sudo cp /etc/nginx/sites-available/ngix-para-odoo-erp/default.conf /etc/nginx/sites-available/default.conf
cd ..
mv default default-temp
mv default.conf default

cd /etc/nginx/sites-available
nano default
server_name j.wemakeyourdayeasy.com 11.64.123.12;
nginx -s reload
```


# Instalando el certificado digital ( https://certbot.eff.org/lets-encrypt/ubuntuxenial-nginx )
```
sudo apt-get update
sudo apt-get install software-properties-common
sudo add-apt-repository ppa:certbot/certbot
sudo apt-get update
sudo apt-get install python3-certbot-nginx
sudo certbot --nginx
-A
- 2
Dentro de Odoo configuras los parámetros.
Configuración > Parámetros > Parámetros del sistema

web.base.url
http -> https

web.base.url.freeze
True
```
