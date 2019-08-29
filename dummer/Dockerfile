FROM ruby:2.5

RUN gem update bundler

RUN mkdir -p /app
COPY Gemfile Gemfile.lock /tmp/
RUN cd /tmp && bundle install -j4 --deployment --without 'development test' --path /app/vendor/bundle

COPY . /app
WORKDIR /app

CMD bundle exec dummer -c dummer_client.conf -r ${RATE:-1000}
