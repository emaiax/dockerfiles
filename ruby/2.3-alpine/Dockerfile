FROM ruby:2.3-alpine
LABEL maintainer "emaiax <eduvimaia@gmail.com>"

RUN apk add --no-cache --update \
      bash \
      build-base \
      curl \
      git \
      less \
      libxml2-dev \
      libxslt-dev \
      tzdata

RUN echo "install: --no-document" > $HOME/.gemrc && echo "update: --no-document" >> $HOME/.gemrc
RUN gem install bundler && bundle config build.nokogiri --use-system-libraries

WORKDIR /app

CMD ["/bin/bash"]
