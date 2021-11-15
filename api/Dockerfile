ARG RUBY_VERSION
FROM ruby:${RUBY_VERSION}

# Set env
ENV LANG C.UTF-8
ENV TZ Asia/Tokyo
ENV API_ROOT /myapi

# Install dependency
RUN apt-get update -qq \
    && apt-get install -y --no-install-recommends \
        nodejs \
        default-mysql-client \
    && apt-get clean \
    && rm --recursive --force /var/lib/apt/lists/*

# Set working directory
RUN mkdir -p $API_ROOT
WORKDIR $API_ROOT

# Install gems
COPY ./src/Gemfile ${API_ROOT}/Gemfile
COPY ./src/Gemfile.lock ${API_ROOT}/Gemfile.lock
RUN bundle install
COPY ./src $API_ROOT

COPY ./entrypoint.sh /usr/bin/
RUN chmod +x /usr/bin/entrypoint.sh
ENTRYPOINT ["entrypoint.sh"]

# Create the user
ARG USERNAME=api
RUN useradd --create-home api --shell /bin/bash
RUN chown -R api $API_ROOT
USER api

EXPOSE 3000
CMD ["rails", "server", "-p", "3000", "-b", "0.0.0.0"]