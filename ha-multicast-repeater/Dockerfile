ARG BUILD_FROM
FROM ${BUILD_FROM}

SHELL ["/bin/ash", "-o", "pipefail", "-c"]

ARG MDNS_REPEATER_VERSION
RUN \
    apk add --no-cache --virtual .build-deps \
        build-base \
        git \
    \
    && git clone -b ${MDNS_REPEATER_VERSION} --depth 1 \
        https://github.com/gamorris/mdns-repeater /usr/src/mdns \
    && cd /usr/src/mdns \
    && gcc -O3 -o /usr/bin/mdns-repeater \
        mdns-repeater.c -DVERSION="\"${MDNS_REPEATER_VERSION}\"" \
    \
    && apk del .build-deps \
    && rm -rf \
        /usr/src/mdns

COPY rootfs /
RUN chmod 755 /etc/services.d/ha_mdns_repeater/*
