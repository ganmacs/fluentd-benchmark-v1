FROM ruby:2.5

RUN gem update bundler

RUN mkdir -p /app && mkdir -p /var/log/flunetd_stats
WORKDIR /app
COPY Gemfile /app/
RUN bundle install -j4 --path /app/vendor/bundle

ARG ENTRYKIT_VERSION=0.4.0
RUN curl -sSfLO https://github.com/progrium/entrykit/releases/download/v${ENTRYKIT_VERSION}/entrykit_${ENTRYKIT_VERSION}_Linux_x86_64.tgz && \
  tar -xvzf entrykit_${ENTRYKIT_VERSION}_Linux_x86_64.tgz && \
  rm entrykit_${ENTRYKIT_VERSION}_Linux_x86_64.tgz && \
  mv entrykit /bin/entrykit && \
  chmod +x /bin/entrykit && \
  entrykit --symlink

COPY . /app

ENTRYPOINT ["render", "receiver.conf", "--"]
CMD ["bundle", "exec", "fluentd", "-c", "receiver.conf"]
