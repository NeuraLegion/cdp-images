FROM debian:bookworm-slim

ARG DEBIAN_FRONTEND=noninteractive
ENV RD_PORT=9222

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        chromium=150.0.7871.124-1~deb12u1 \
        dumb-init \
        socat \
        fontconfig \
        fonts-liberation \
        procps \
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN groupadd -r chrome && useradd --create-home -rm -g chrome -G audio,video chrome

WORKDIR /home/chrome

COPY --chown=chrome:chrome entrypoint.sh /home/chrome/

USER chrome
ENTRYPOINT ["dumb-init", "--", "/bin/sh", "/home/chrome/entrypoint.sh"]
