FROM elixir:1.9-alpine
LABEL maintainer "emaiax <eduvimaia@gmail.com>"

RUN apk add --update --no-cache \
      bash \
      build-base \
      git \
      yarn \
      inotify-tools \

RUN mix local.hex --force \
  && mix local.rebar --force
