FROM joshfng/broadway-base:latest

RUN apt-get update && \
  apt-get dist-upgrade -y

RUN apt-get install -y --no-install-recommends \
  virt-manager \
  dbus-x11 \
  libglib2.0-bin \
  gir1.2-spiceclientgtk-3.0 \
  ssh \
  at-spi2-core

  RUN apt-get autoclean && \
    apt-get autoremove && \
    rm -rf /var/lib/apt/lists/*

RUN mkdir -p /root/.ssh

RUN echo "Host *\n\tStrictHostKeyChecking no\n" >> /root/.ssh/config

COPY startapp.sh /usr/local/bin/startapp

CMD ["/usr/local/bin/startapp"]
