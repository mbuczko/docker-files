FROM ubuntu:14.04.2 
MAINTAINER Michal Buczko "michal@buczko.pl"

RUN apt-get update && apt-get install -y wget
RUN wget --no-check-certificate https://download-cdn.getsyncapp.com/stable/linux-x64/BitTorrent-Sync_x64.tar.gz -O /tmp/btsync.tar.gz
RUN gzip -d /tmp/btsync.tar.gz
RUN cd /usr/bin && tar -xvf /tmp/btsync.tar && rm /tmp/btsync.tar

RUN mkdir -p /btsync/.sync

WORKDIR /btsync/.sync

EXPOSE 8888 55555

ENTRYPOINT ["btsync"]
CMD ["--config", "/etc/btsync.conf", "--nodaemon"]

ADD btsync.conf /etc/btsync.conf

