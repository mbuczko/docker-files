FROM java:8-jre
MAINTAINER Michal Buczko "michal@buczko.pl"

#RUN gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
#RUN curl -sSL https://get.rvm.io | bash -s stable --ruby
#RUN rvm install 2.0.0 && rvm use 2.0.0 && rvm rubygems latest

RUN apt-get update && \
    apt-get -y install wget build-essential zlib1g-dev libssl-dev \
    libreadline6-dev libyaml-dev && cd /tmp && \
    wget -q http://cache.ruby-lang.org/pub/ruby/2.2/ruby-2.2.2.tar.gz && \
    tar xzf ruby-2.2.2.tar.gz && \
    cd ruby-2.2.2 && ./configure --enable-shared --prefix=/usr && \
    make && make install && cd .. && rm -rf ruby-2.2.2*

RUN apt-get update && apt-get install -y supervisor
RUN wget http://aphyr.com/riemann/riemann_0.2.10_all.deb && dpkg -i riemann_0.2.10_all.deb
RUN apt-get -y clean all
RUN gem install riemann-tools

RUN echo Europe/Warsaw > /etc/timezone && dpkg-reconfigure --frontend noninteractive tzdata

# Expose the ports for inbound events and websockets
EXPOSE 5555
EXPOSE 5555/udp
EXPOSE 5556

ADD supervisord.conf /etc/supervisor/conf.d/supervisord.conf

ENTRYPOINT ["/usr/bin/supervisord", "-n"]
