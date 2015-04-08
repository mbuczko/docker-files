FROM mbuczko/java8:latest 
MAINTAINER Michal Buczko "michal@buczko.pl"

ENV RUBY_VERSION 2.2.1

## To install add-apt-repository
RUN apt-get -y update

## ruby 2.2.0 installation
RUN apt-get install -y --force-yes git-core curl wget zlib1g-dev build-essential libssl-dev libreadline-dev libyaml-dev libsqlite3-dev sqlite3 libxml2-dev libxslt1-dev libcurl4-openssl-dev python-software-properties libffi-dev patch libz-dev make

## Cleanup
RUN apt-get clean all
RUN curl -o /ruby-$RUBY_VERSION/src.tar.bz2 --create-dirs http://cache.ruby-lang.org/pub/ruby/ruby-$RUBY_VERSION.tar.bz2 && \
    cd /ruby-$RUBY_VERSION && tar xjf src.tar.bz2 --strip-components=1 && \
    ./configure --prefix=/usr --sysconfdir=/etc --disable-install-doc --without-tk --without-win32 --without-win32ole --without-X11 && \
    make && make install && cd / && \
    rm -fr /ruby-$RUBY_VERSION && \

    apt-get remove -y libssl-doc libtinfo-dev $RUBY_BUILD_DEPENDENCIES && \
    apt-get clean && \
    cd /var/lib/apt/lists && rm -fr *Release* *Sources* *Packages* && \
    truncate -s 0 /var/log/*log

# Don't install rdoc and ri files for any gem
RUN echo 'gem: --no-document' > /etc/gemrc

RUN gem install bundler -v 1.8.2
RUN gem update --system
