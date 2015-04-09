FROM mbuczko/ruby:2.2
MAINTAINER Michal Buczko "michal@buczko.pl"

RUN apt-get update && apt-get install -y supervisor
RUN wget http://aphyr.com/riemann/riemann_0.2.9_all.deb && dpkg -i riemann_0.2.9_all.deb
RUN wget http://s3.amazonaws.com/influxdb/influxdb_latest_amd64.deb && dpkg -i influxdb_latest_amd64.deb && rm *.deb
RUN apt-get -y clean all
RUN mkdir /var/log/influx
RUN echo Europe/Warsaw > /etc/timezone && dpkg-reconfigure --frontend noninteractive tzdata

# Expose the ports for inbound events and websockets
EXPOSE 5555
EXPOSE 5555/udp
EXPOSE 5556

ADD ./riemann.config /etc/riemann/riemann.config

# Influx config
ADD influx.conf /etc/influxdb/influx.conf
ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf

# Admin server
EXPOSE 8083

# HTTP API
EXPOSE 8086

# HTTPS API
#EXPOSE 8084

VOLUME ["/data"]

ENTRYPOINT ["/usr/bin/supervisord", "-n"]
