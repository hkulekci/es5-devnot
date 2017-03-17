FROM ubuntu

ENV FILEBEAT_VERSION 5.2.2

RUN apt-get update -qq \
 && apt-get install -qqy curl \
 && apt-get clean

RUN curl -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-${FILEBEAT_VERSION}-amd64.deb \
 && dpkg -i filebeat-${FILEBEAT_VERSION}-amd64.deb \
 && rm filebeat-${FILEBEAT_VERSION}-amd64.deb
RUN ln -s /usr/share/filebeat/bin/filebeat /usr/bin/filebeat

COPY filebeat.yml /etc/filebeat/filebeat.yml

CMD ["/usr/share/filebeat/bin/filebeat", "-path.home", "/usr/share/filebeat", "-path.config", "/etc/filebeat", "-path.data", "/var/lib/filebeat", "-path.logs", "/var/log/filebeat", "-e", "-v"]
