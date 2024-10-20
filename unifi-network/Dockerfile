FROM ubuntu:24.04

ARG DEBIAN_FRONTEND=noninteractive
ENV APP_NAME=unifi
ENV APP_VERSION=8.5.6
ENV APP_ROOT=/app

USER root

RUN apt-get update && apt-get -y upgrade

RUN mkdir -p ${APP_ROOT}

RUN apt-get install -y \
  binutils \
  curl \
  gnupg \
  gosu \
  jsvc \
  libcap2 \
  liblog4j2-java \
  logrotate \
  openjdk-17-jre-headless \
  tzdata

# unifi requires mongo v7 but mongo's noble repo only has v8
RUN curl -fsSL https://www.mongodb.org/static/pgp/server-7.0.asc | \
  gpg -o /usr/share/keyrings/mongodb-server-7.0.gpg --dearmor && \
  echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-7.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/7.0 multiverse" | tee /etc/apt/sources.list.d/mongodb-org-7.0.list && \
  apt-get update && \
  apt-get install -y mongodb-org

RUN curl -o /tmp/unifi.deb "https://dl.ui.com/unifi/${APP_VERSION}/unifi_sysvinit_all.deb"

RUN dpkg -i /tmp/unifi.deb; \
  ln -s /var/lib/unifi ${APP_ROOT}/var; \
  ln -s /var/log/unifi ${APP_ROOT}/log; \
  mkdir -p ${APP_ROOT}/var/sites/default;

COPY ./rootfs /
RUN chmod +x -R /usr/local/bin

VOLUME ["${APP_ROOT}/var"]

HEALTHCHECK CMD /usr/local/bin/healthcheck.sh || exit 1

ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
