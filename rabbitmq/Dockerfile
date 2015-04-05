FROM ubuntu:14.04
MAINTAINER Michal Buczko "michal@buczko.pl"

# Reduce output from debconf
ENV DEBIAN_FRONTEND noninteractive
ENV PATH /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

RUN apt-get -y update
RUN echo "deb http://www.rabbitmq.com/debian/ testing main" >> /etc/apt/sources.list
RUN apt-get install -y wget
RUN wget http://www.rabbitmq.com/rabbitmq-signing-key-public.asc -O /tmp/rabbitmq-signing-key-public.asc
RUN apt-key add /tmp/rabbitmq-signing-key-public.asc
RUN apt-get -y update

RUN apt-get install -y rabbitmq-server
RUN rabbitmq-plugins enable rabbitmq_management
RUN echo "[{rabbit, [{loopback_users, []}]}]." > /etc/rabbitmq/rabbitmq.config

# For RabbitMQ and RabbitMQ Adminm
EXPOSE 5672 15672

ENTRYPOINT ["/usr/sbin/rabbitmq-server"]