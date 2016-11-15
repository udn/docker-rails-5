FROM ruby:2.2.3

MAINTAINER Burhanudin Hakim "udnpico@gmail.com"

ENV PHANTOMJS_VERSION 2.1.1
ENV APP_HOME /rails-app


RUN apt-get update && apt-get install -y \
  build-essential \
  git \
  mysql-client \
  libmysqlclient-dev \
  nodejs \
  wget libfreetype6 libfontconfig bzip2 && \
  mkdir -p /srv/var  && \
  wget -q --no-check-certificate -O /tmp/phantomjs-$PHANTOMJS_VERSION-linux-x86_64.tar.bz2 https://github.com/Medium/phantomjs/releases/download/v$PHANTOMJS_VERSION/phantomjs-$PHANTOMJS_VERSION-linux-x86_64.tar.bz2 && \
  tar -xjf /tmp/phantomjs-$PHANTOMJS_VERSION-linux-x86_64.tar.bz2 -C /tmp && \
  rm -f /tmp/phantomjs-$PHANTOMJS_VERSION-linux-x86_64.tar.bz2 && \
  mv /tmp/phantomjs-$PHANTOMJS_VERSION-linux-x86_64/ /srv/var/phantomjs && \
  ln -s /srv/var/phantomjs/bin/phantomjs /usr/bin/phantomjs && \ 
  git clone https://github.com/n1k0/casperjs.git /srv/var/casperjs && \
  ln -s /srv/var/casperjs/bin/casperjs /usr/bin/casperjs  && \
  apt-get autoremove -y && \
  apt-get clean all

RUN mkdir -p $APP_HOME
WORKDIR $APP_HOME

ADD Gemfile  $APP_HOME/Gemfile
ADD Gemfile.lock $APP_HOME/Gemfile.lock
RUN gem install bundler && bundle config build.nokogiri --use-system-libraries && bundle install --jobs 20 --retry 5

