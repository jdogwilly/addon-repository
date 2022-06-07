ARG BUILD_FROM
FROM $BUILD_FROM

LABEL io.hass.version="1" io.hass.type="addon" io.hass.arch="armhf|aarch64|i386|amd64"

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        cups \
        avahi-daemon \
        libnss-mdns \
        dbus \
        colord \
        printer-driver-all \
        printer-driver-gutenprint \
        openprinting-ppds \
        hpijs-ppds \
        hp-ppd  \
        hplip \
        gnupg2 \
        lsb-release \
    && echo "deb http://nginx.org/packages/debian `lsb_release -cs` nginx" \
        | tee /etc/apt/sources.list.d/nginx.list \
    && curl -fsSL https://nginx.org/keys/nginx_signing.key | apt-key add - \
    && curl -o foo2zjs.zip https://github.com/mikerr/foo2zjs/archive/refs/heads/master.zip \
    && unzip foo2zjs.zip
    && cd foo2zjs.zip
    && make uninstall
    && make
    && make install
    && make cups
    && apt-get update \
    && apt-get install nginx nginx-module-njs \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*

COPY rootfs /

EXPOSE 631

CMD ["/run.sh"]
