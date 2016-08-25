FROM node:6.4.0-slim

MAINTAINER Renuo Developers <dev@renuo.ch>

RUN apt-get update && \
        DEBIAN_FRONTEND="noninteractive" \
        apt-get install -y --no-install-recommends \
        xvfb \
        chromium=52.0.2743.116-1~deb8u1 \
        bzip2

ENV DISPLAY :99
ENV CHROME_BIN /usr/bin/chromium

ADD entrypoint.sh /entrypoint.sh
RUN chmod a+x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
