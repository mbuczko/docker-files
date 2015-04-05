# handy docker receipts

## nginx

    docker run -d --name gitlab_data --volume /opt/gitlab/embedded/service/gitlab-rails/public --volume /var/opt/gitlab --volume /var/log/gitlab --volume /etc/gitlab ubuntu:14.04.2 /bin/true
    docker run -d --name nginx --volumes-from gitlab_data -v /home/core/www-data:/usr/share/nginx/html:ro -p 80:80 -p 443:443 nginx
