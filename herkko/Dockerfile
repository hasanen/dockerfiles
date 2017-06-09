FROM ruby:2.4.1-slim
LABEL maintainer Joni Hasanen "joni@pieceofcode.com"

ENV APP_USER herkko
ENV APP_HOME /app

RUN apt-get update \
    && apt-get -y --no-install-recommends install git build-essential curl \
    && curl -o heroku.tar.gz https://cli-assets.heroku.com/heroku-cli/channels/stable/heroku-cli-linux-x64.tar.gz \
    && tar -xzf heroku.tar.gz \
    && mkdir -p /usr/local/lib /usr/local/bin \
    && mv heroku-cli-* /usr/local/lib/heroku \
    && ln -s /usr/local/lib/heroku/bin/heroku /usr/local/bin/heroku

RUN gem install herkko
RUN gem install travis
RUN apt-get -y purge build-essential && apt-get clean  apt-get -y autoremove

RUN useradd  --create-home --shell /bin/bash $APP_USER

RUN mkdir -p $APP_HOME
RUN chown -R $APP_USER $APP_HOME

WORKDIR $APP_HOME

USER $APP_USER

ENTRYPOINT ["herkko"]
