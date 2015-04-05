FROM mbuczko/java8:latest
MAINTAINER Michal Buczko "michal@buczko.pl"

RUN apt-get update && apt-get install -y python2.7

# Download and extract Cassandra
RUN mkdir /opt/cassandra; \
    wget -O - http://www.us.apache.org/dist/cassandra/2.1.2/apache-cassandra-2.1.2-bin.tar.gz | tar xzf - --strip-components=1 -C "/opt/cassandra";

# Download and extract DataStax OpsCenter Agent
RUN mkdir /opt/agent; \
    wget -O - http://downloads.datastax.com/community/datastax-agent-5.0.1.tar.gz | tar xzf - --strip-components=1 -C "/opt/agent";

ENV CASSANDRA_CONFIG /opt/cassandra/conf/
RUN ln -s /opt/cassandra/bin/cqlsh /usr/bin

# Run base config script
ADD config-cassandra-base.sh /usr/local/bin/config-cassandra-base
RUN /usr/local/bin/config-cassandra-base

# Necessary since cassandra is trying to override the system limitations
# See https://groups.google.com/forum/#!msg/docker-dev/8TM_jLGpRKU/dewIQhcs7oAJ
RUN rm -f /etc/security/limits.d/cassandra.conf

EXPOSE 7199 7000 7001 9160 9042 8012 61621

USER root

# Place single-node startup-config script
ADD cassandra-singlenode.sh /usr/local/bin/cassandra-singlenode

# Start Cassandra
ENTRYPOINT ["cassandra-singlenode"]
