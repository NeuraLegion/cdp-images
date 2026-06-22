FROM chromedp/headless-shell:139.0.7258.155

ENV RD_PORT=9222

# Install socat (required for port forwarding)
USER root
RUN apt-get update -y && \
    apt-get install -y --no-install-recommends socat && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN groupadd -r chrome 2>/dev/null || true && \
    useradd --create-home -rm -g chrome -G audio,video chrome 2>/dev/null || true

WORKDIR /home/chrome

COPY --chown=chrome:chrome entrypoint.sh /home/chrome/

USER chrome
ENTRYPOINT ["/bin/sh", "/home/chrome/entrypoint.sh"]
