docker run --name nginx -v /home/core/sites-enabled:/etc/nginx/sites-enabled:ro -v /home/core/www-data:/usr/share/nginx/html:ro -p 80:80 -p 443:443 --volumes-from gitlab --add-host=localbox:172.17.42.1 -d mbuczko/riemann:latest