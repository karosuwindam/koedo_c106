FROM ubuntu:24.04

ENV FILEBEAT_VERSION 8.18.2
ENV FILEBEAT_BASE_URL https://artifacts.elastic.co/downloads/beats/filebeat/
# ENV ARCH x86_64
ENV ARCH arm64

RUN \
  apt-get update && apt-get upgrade -y && \
  apt-get -y install systemd && \
  apt-get -y install wget && \
  apt-get -y install bash && \
  wget -q ${FILEBEAT_BASE_URL}filebeat-${FILEBEAT_VERSION}-linux-${ARCH}.tar.gz && \
  wget -q ${FILEBEAT_BASE_URL}filebeat-${FILEBEAT_VERSION}-linux-${ARCH}.tar.gz.sha512 && \
  sha512sum -c filebeat-${FILEBEAT_VERSION}-linux-${ARCH}.tar.gz.sha512 && \
  tar xzf filebeat-${FILEBEAT_VERSION}-linux-${ARCH}.tar.gz && \
  mkdir -p /usr/share/filebeat && \
  mv filebeat-${FILEBEAT_VERSION}-linux-${ARCH}/filebeat /usr/share/filebeat && \
  mkdir -p /etc/filebeat/conf.d && \
  mkdir -p /etc/filebeat/modules.d && \
  mkdir -p /etc/filebeat/log && \
  rm -rf /filebeat* && \
  rm -rf /var/lib/apt/lists/*

WORKDIR /usr/share/filebeat

COPY filebeat.docker.yml filebeat.yml
RUN chmod go-w filebeat.yml


ENV PATH=/usr/share/filebeat:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

CMD ["filebeat","-e","-strict.perms=false"]