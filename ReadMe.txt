php artisan serve --port=8001
php artisan websocket:serve



sudo apt install supervisor -y
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
