# Note: I can't use Ruby 3.2 yet because Jekyll uses Liquid 4, and Liquid 4
# throws an exception if you use it with Ruby 3.2:
#
#     Liquid Exception: undefined method `tainted?' for { ... post ...}
#
# The fix is available in Liquid 5, but that isn't supported by Jekyll yet.
#
# There are various bugs tracking this on the Jekyll repository, e.g. see
# https://github.com/jekyll/jekyll/issues/9233
# https://github.com/jekyll/jekyll/issues/8535
#
# If/when Jekyll allows a Liquid upgrade, then I can bump this to Ruby 3.2.
FROM ruby:3.1-slim

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
ADD plugins /usr/local/lib/ruby/3.1.0/alexwlchan

ENTRYPOINT ["bundle", "exec", "jekyll"]
