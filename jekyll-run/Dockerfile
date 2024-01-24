FROM ruby:3.2-slim

LABEL maintainer "Alex Chan <alex@alexwlchan.net>"
LABEL description "Build image for alexwlchan.net"
LABEL org.opencontainers.image.source https://github.com/alexwlchan/jekyll-docker-image

COPY Gemfile .
COPY Gemfile.lock .

COPY ./scripts/install_jekyll.sh .
RUN ./install_jekyll.sh

# Install my custom plugins, so they can be loaded in other Jekyll sites.
#
# This is a bit of a hack, because I'm injecting them directly
# alongside the Ruby standard library rather than packaging them
# as proper gems -- it'll do for now.
#
# TODO: Look at packaging some of these as proper gems.
ADD plugins /usr/local/lib/ruby/3.2.0/alexwlchan

ENTRYPOINT ["bundle", "exec", "jekyll"]
