# handy docker receipts

## nginx for gitlab

    docker run -d --name gitlab_data --volume /var/opt/gitlab --volume /var/log/gitlab --volume /etc/gitlab ubuntu:14.04.2 /bin/true
    docker run -d --name gitlab --publish 8080:80 --publish 2222:22 --volume /opt/gitlab/embedded/service/gitlab-rails/public --volumes-from gitlab_data mbuczko/gitlab:latest
    docker run -d --name nginx --volumes-from gitlab -v /home/core/www-data:/usr/share/nginx/html:ro -p 80:80 -p 443:443 nginx
