ARG GRAFANA_VERSION="latest"
FROM grafana/grafana:${GRAFANA_VERSION}

ENV SERVER_PROTOCOL="http" \
    HTTP_PORT="80" \
    DOMAIN_NAME="localhost" \
    ENFORCE_DOMAIN="false"

EXPOSE 80/tcp
EXPOSE 443/tcp

VOLUME [ "/etc/grafana", "/var/lib/grafana" ]

# grafana image uses already at this point grafana user. apk needs root permissions
USER root

COPY conf/grafana.ini /etc/grafana/grafana.ini

RUN chown grafana:grafana /etc/grafana/grafana.ini \
    && apk add --update libcap \ 
    && rm -rf /var/cache/apk \
    && setcap 'cap_net_bind_service=+ep' /usr/share/grafana/bin/grafana-server

USER grafana
