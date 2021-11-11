ARG RUBY_VERSION
FROM ruby:${RUBY_VERSION}

ENV LANG C.UTF-8
ENV TZ Asia/Tokyo

ENV API_ROOT /myapi

RUN apt-get update -qq && \
    apt-get install -y --no-install-recommends \
    nodejs \
    default-mysql-client && \
    apt-get clean && \
    rm --recursive --force /var/lib/apt/lists/*

RUN mkdir -p ${API_ROOT}
WORKDIR ${API_ROOT}

COPY ./src/Gemfile ${API_ROOT}/Gemfile
COPY ./src/Gemfile.lock ${API_ROOT}/Gemfile.lock
RUN bundle install
COPY . ${API_ROOT}

COPY ./src/entrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]
EXPOSE 3000

CMD ["rails", "server", "-p", "3000", "-b", "0.0.0.0"]