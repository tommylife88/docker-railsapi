ARG MYSQL_VERSION
FROM mysql:${MYSQL_VERSION}

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && \
    apt-get install -y --no-install-recommends locales && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* && \
    locale-gen ja_JP.UTF-8

RUN sed -i -E 's/# (ja_JP.UTF-8)/\1/' /etc/locale.gen && locale-gen

ENV LC_ALL ja_JP.UTF-8
ENV TZ Asia/Tokyo

COPY my.cnf /etc/mysql/conf.d/my.cnf
RUN chmod 0444 /etc/mysql/conf.d/my.cnf

EXPOSE 3306
CMD ["mysqld"]