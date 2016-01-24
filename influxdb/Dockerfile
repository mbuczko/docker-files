FROM debian:jessie
MAINTAINER Michal Buczko "michal@buczko.pl"

RUN apt-get update && apt-get install -y wget supervisor
RUN wget https://s3.amazonaws.com/influxdb/influxdb_0.9.4.2_amd64.deb && dpkg -i influxdb_0.9.4.2_amd64.deb
RUN wget https://s3.amazonaws.com/get.influxdb.org/chronograf/chronograf_0.4.0_amd64.deb && dpkg -i chronograf_0.4.0_amd64.deb && rm *.deb

RUN apt-get -y clean all

RUN echo Europe/Warsaw > /etc/timezone && dpkg-reconfigure --frontend noninteractive tzdata

ADD influx.conf /etc/influxdb/influx.conf
ADD chronograf.conf /etc/influxdb/chronograf.conf
ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf

# Admin server
EXPOSE 8083

# HTTP API
EXPOSE 8086

# HTTPS API
#EXPOSE 8084

# chronograf
EXPOSE 10000

ENTRYPOINT ["/usr/bin/supervisord", "-n"]
