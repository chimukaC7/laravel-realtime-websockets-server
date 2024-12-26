php artisan serve --port=8001
php artisan websocket:serve


# On Debian / Ubuntu
apt install supervisor

# On Red Hat / CentOS
yum install supervisor
systemctl enable supervisord


cd /etc/supervisor/conf.d/
sudo nano ws.supersecuredomain.com.conf

========================================================================================================================
[program:ws_supersecuredomain]
command=/usr/bin/php /var/www/ws.supersecuredomain.com/artisan websockets:serve
autostart=true
autorestart=true
========================================================================================================================

sudo supervisorctl update
sudo supervisorctl start ws_supersecuredomain
sudo supervisorctl status


========================================================================================================================
cd /etc/nginx/sites-available
sudo nano ws.supersecuredomain.com
sudo ln -s /etc/nginx/sites-available/ws.supersecuredomain.com /etc/nginx/sites-enabled/
ll ../sites-enabled/
sudo nginx -t
sudo systemctl reload nginx.service


sudo acme.sh --issue -d ws.supersecuredomain.com -w /var/www/ws.supersecuredomain.com/public/ --force

sudo mkdir /etc/nginx/certs/ws.supersecuredomain.com/
sudo acme.sh -d ws.supersecuredomain.com --install-cert --key-file /etc/nginx/certs/ws.supersecuredomain.com/key.pem
--fullchain-file/etc/nginx/certs/ws.supersecuredomain.com/fullchain.pem
--ca-file /etc/nginx/certs/ws.supersecuredomain.com/ca.pem --reloadcmd "systemctl force-reload nginx.service"
--force
