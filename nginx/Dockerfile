FROM nginx:latest
MAINTAINER Michal Buczko "michal@buczko.pl"

ADD ./nginx.conf /etc/nginx/nginx.conf

RUN echo "gitlab-www:x:998:998::/var/opt/gitlab/nginx:/bin/false" >> /etc/passwd
RUN echo "gitlab-www:x:998:" >> /etc/group
RUN echo Europe/Warsaw > /etc/timezone && dpkg-reconfigure --frontend noninteractive tzdata

