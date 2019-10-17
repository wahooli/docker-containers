ARG RADARR_VERSION="latest"
FROM linuxserver/radarr:${RADARR_VERSION}

ENV HTTP_PORT="80" \
    HTTPS_PORT="443" \
    ENABLE_SSL="False"

EXPOSE 80/tcp
EXPOSE 443/tcp

COPY config /config

# expecting arch linux to have setcap installed
RUN chown -R abc:abc /config \
    && sed -i "s/<Port>80\/Port>/<Port>$HTTP_PORT<\/Port>/g" /config/config.xml \
    && sed -i "s/<SslPort>443<\/Port>/<Port>$HTTPS_PORT<\/SslPort>/g" /config/config.xml \
    && sed -i "s/<EnableSsl>False<\/EnableSsl>/<EnableSsl>$ENABLE_SSL<\/EnableSsl>/g" /config/config.xml \
    && apt-get update \
    && apt-get install -y libcap2-bin \
    && rm -rf \
       /tmp/* \
       /var/lib/apt/lists/* \
       /var/tmp/* \
    && setcap 'cap_net_bind_service=+ep' $(realpath $(which mono))
