FROM ubuntu:16.04

MAINTAINER Saverio Proto <zioproto@gmail.com>

RUN apt-get update && \
    apt-get install -y \
      redis-server \
      redis-tools \
      redis-sentinel && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 6379
EXPOSE 26379
COPY redis-master.conf /redis-master/redis.conf
COPY redis-slave.conf /redis-slave/redis.conf
COPY ./entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
ENTRYPOINT ["bash","-c"]
CMD ["/entrypoint.sh"]
