FROM docker.io/bitnami/minideb:buster
LABEL maintainer "Bitnami <containers@bitnami.com>"

ENV HOME="/" \
    OS_ARCH="amd64" \
    OS_FLAVOUR="debian-10" \
    OS_NAME="linux"

COPY prebuildfs /
# Install required system packages and dependencies
RUN install_packages ca-certificates curl gzip procps tar wget
RUN wget -nc -P /tmp/bitnami/pkg/cache/ https://downloads.bitnami.com/files/stacksmith/elasticsearch-exporter-1.3.0-7-linux-amd64-debian-10.tar.gz && \
    echo "1ec5044e1de9e412620f4b72d7feb8b8dadabca9e7a744e6c615d5b8d72d5ef1  /tmp/bitnami/pkg/cache/elasticsearch-exporter-1.3.0-7-linux-amd64-debian-10.tar.gz" | sha256sum -c - && \
    tar -zxf /tmp/bitnami/pkg/cache/elasticsearch-exporter-1.3.0-7-linux-amd64-debian-10.tar.gz -P --transform 's|^[^/]*/files|/opt/bitnami|' --wildcards '*/files' && \
    rm -rf /tmp/bitnami/pkg/cache/elasticsearch-exporter-1.3.0-7-linux-amd64-debian-10.tar.gz
RUN apt-get update && apt-get upgrade -y && \
    rm -r /var/lib/apt/lists /var/cache/apt/archives
RUN chmod g+rwX /opt/bitnami

ENV APP_VERSION="1.3.0" \
    BITNAMI_APP_NAME="elasticsearch-exporter" \
    PATH="/opt/bitnami/elasticsearch-exporter/bin:$PATH"

EXPOSE 9114

WORKDIR /opt/bitnami/elasticsearch-exporter
USER 1001
ENTRYPOINT [ "/opt/bitnami/elasticsearch-exporter/bin/elasticsearch_exporter" ]
