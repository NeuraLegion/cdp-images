# chromedp/headless-shell v139.0.7258.155
# TODO: Fork upstream repo or mirror to internal registry before production use (security review required)
FROM chromedp/headless-shell@sha256:ab3598f600417861066c8e1002ef355423b97b3365e3b8f5cf36c12ebc9f3637

ENV RD_PORT=9222

# Install socat (required for port forwarding)
USER root
RUN apt-get update -y && \
    apt-get install -y --no-install-recommends socat curl && \
    apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN groupadd -r chrome 2>/dev/null || true && \
    useradd --create-home -rm -g chrome -G audio,video chrome 2>/dev/null || true

WORKDIR /home/chrome

COPY --chown=chrome:chrome entrypoint.sh /home/chrome/

USER chrome
ENTRYPOINT ["/bin/sh", "/home/chrome/entrypoint.sh"]
