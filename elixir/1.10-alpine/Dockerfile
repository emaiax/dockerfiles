FROM elixir:1.10-alpine

RUN apk add --update --no-cache \
      bash \
      build-base \
      git \
      inotify-tools

RUN mix local.hex --force && mix local.rebar --force
