FROM ubuntu:latest
MAINTAINER Michal Buczko "michal@buczko.pl"

RUN apt-get install -y nginx 

ADD ./nginx.conf /etc/nginx/nginx.conf

RUN echo "gitlab-www:x:998:998::/var/opt/gitlab/nginx:/bin/false" >> /etc/passwd
RUN echo "gitlab-www:x:998:" >> /etc/group

# Set working directory.
WORKDIR /etc/nginx

# Expose riemann dash port
EXPOSE 80

# Define default command.
ENTRYPOINT ["nginx"]

