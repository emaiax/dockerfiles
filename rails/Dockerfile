FROM emaiax/ruby:latest
LABEL maintainer "emaiax <eduvimaia@gmail.com>"

RUN apk add --no-cache --update \
      build-base bash git curl tzdata fontconfig \
      libxml2-dev libxslt-dev postgresql-dev

# Yarn
RUN echo -e 'http://dl-cdn.alpinelinux.org/alpine/edge/main\nhttp://dl-cdn.alpinelinux.org/alpine/edge/community\nhttp://dl-cdn.alpinelinux.org/alpine/edge/testing' > /etc/apk/repositories
RUN apk add --no-cache --update yarn

# Phantomjs 2.0.0
RUN curl -Ls https://github.com/fgrehm/docker-phantomjs2/releases/download/v2.0.0-20150722/dockerized-phantomjs.tar.gz | tar xz -C /

CMD ["rails s"]
