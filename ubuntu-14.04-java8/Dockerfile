FROM ubuntu:14.04.2
MAINTAINER Michal Buczko "michal@buczko.pl"

## To install add-apt-repository
RUN apt-get -y update

## JAVA installation
RUN apt-get install -y --force-yes software-properties-common
RUN add-apt-repository ppa:webupd8team/java
RUN apt-get update

RUN echo "oracle-java8-installer shared/accepted-oracle-license-v1-1 select true" | debconf-set-selections
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y --force-yes --no-install-recommends oracle-java8-installer

## Cleanup
RUN apt-get clean all

## JAVA_HOME
ENV JAVA_HOME /usr/lib/jvm/java-8-oracle
