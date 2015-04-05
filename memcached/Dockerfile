FROM ubuntu:14.04
MAINTAINER Michal Buczko "michal@buczko.pl"

RUN apt-get update && apt-get install -y memcached

EXPOSE 11211
CMD ["/usr/bin/memcached", "-u", "memcache", "-v"]
