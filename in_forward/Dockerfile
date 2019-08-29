FROM ruby:2.5

RUN gem update bundler

RUN mkdir -p /app
WORKDIR /app
COPY Gemfile /app/
RUN bundle install -j4 --path /app/vendor/bundle

COPY . /app

CMD ["bundle", "exec", "fluentd", "-c", "receiver.conf"]
