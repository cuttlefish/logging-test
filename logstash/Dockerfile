FROM docker.elastic.co/logstash/logstash:5.4.0
MAINTAINER Tyler Battle <tbattle@boundlessgeo.com>

COPY logstash.conf /usr/share/logstash/pipeline/logstash.conf

CMD ["-f", "/usr/share/logstash/pipeline/logstash.conf"]
