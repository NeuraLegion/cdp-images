FROM ubuntu:latest

ARG VERSION
ARG DEBIAN_FRONTEND=noninteractive
ENV DBUS_SESSION_BUS_ADDRESS disabled:
ENV RD_PORT=9222

RUN apt-get update -y
RUN apt-get install wget unzip socat apt-utils -y --no-install-recommends
RUN wget -q --no-check-certificate https://storage.googleapis.com/chrome-for-testing-public/${VERSION}/linux64/chrome-headless-shell-linux64.zip
RUN unzip chrome-headless-shell-linux64.zip
RUN rm chrome-headless-shell-linux64.zip

RUN cat chrome-headless-shell-linux64/deb.deps | while read pkg ; do apt-get satisfy -y --no-install-recommends "${pkg}"; done
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN mv chrome-headless-shell-linux64 /headless-shell
RUN chmod +x /headless-shell/chrome-headless-shell
RUN groupadd -r chrome && useradd --create-home -rm -g chrome -G audio,video chrome

WORKDIR /home/chrome

COPY --chown=chrome:chrome entrypoint.sh /home/chrome/

USER chrome
ENV PATH /headless-shell:$PATH
ENTRYPOINT ["/bin/sh", "/home/chrome/entrypoint.sh"]
