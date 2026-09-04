FROM debian:bookworm-slim

ARG DEBIAN_FRONTEND=noninteractive
ENV RD_PORT=9222

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        chromium-headless-shell=151.0.7922.173-1~deb12u1 \
        dumb-init \
        socat \
        wget \
        fontconfig \
        fonts-liberation \
        procps \
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN groupadd -r chromium && useradd --create-home -rm -g chromium -G audio,video chromium

WORKDIR /home/chromium

COPY --chown=chromium:chromium entrypoint.sh /home/chromium/

USER chromium
ENTRYPOINT ["dumb-init", "--", "/bin/sh", "/home/chromium/entrypoint.sh"]
