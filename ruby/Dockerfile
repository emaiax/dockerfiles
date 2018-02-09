FROM ruby:2.3.3-alpine
LABEL maintainer "emaiax <eduvimaia@gmail.com>"

RUN apk add --no-cache --update \
      build-base bash git curl tzdata \
      libxml2-dev libxslt-dev less

RUN echo "install: --no-document" > $HOME/.gemrc && echo "update: --no-document" >> $HOME/.gemrc
RUN gem install bundler && bundle config build.nokogiri --use-system-libraries

WORKDIR /app

CMD ["/bin/bash"]
