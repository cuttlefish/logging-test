FROM debian:jessie
MAINTAINER Tyler Battle <tbattle@boundlessgeo.com>

# Install curl
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        ca-certificates \
        curl \
    && rm -rf /var/lib/apt/lists/*

# Fetch logz.io cert
RUN set -ex \
    && mkdir -p /etc/pki/tls/certs \
    && curl -o /etc/pki/tls/certs/COMODORSADomainValidationSecureServerCA.crt https://raw.githubusercontent.com/logzio/public-certificates/master/COMODORSADomainValidationSecureServerCA.crt

# Install filebeat
RUN set -ex \
    && export DEBIAN_FRONTEND=noninteractive \
    && curl --insecure -L -O https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-5.4.0-amd64.deb \
    && dpkg -i filebeat-5.4.0-amd64.deb \
    && rm filebeat-5.4.0-amd64.deb

# Copy in config files
COPY filebeat.yml /etc/filebeat/

RUN mkdir -p /var/log/filebeat && mkdir -p /usr/share/filebeat

#CMD ["/usr/share/filebeat/bin/filebeat", "-c /etc/filebeat/filebeat.yml", "-path.home /usr/share/filebeat", "-path.config /etc/filebeat", "-path.data /var/lib/filebeat", "-path.logs /var/log/filebeat"]
CMD ["/usr/share/filebeat/bin/filebeat", "-e", "-path.config", "/etc/filebeat"]
