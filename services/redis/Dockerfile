ARG REDIS_VERSION=alpine

FROM redis:${REDIS_VERSION}

COPY redis.conf /usr/local/etc/redis/redis.conf

RUN mkdir /var/log/redis && \
    chown -R 999:1000 /var/log/redis

CMD ["redis-server", "/usr/local/etc/redis/redis.conf"]
