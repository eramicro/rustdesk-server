FROM busybox:stable

ARG S6_OVERLAY_VERSION=3.1.1.2
ARG S6_ARCH=x86_64
ADD https://github.com/just-containers/s6-overlay/releases/download/v${S6_OVERLAY_VERSION}/s6-overlay-noarch.tar.xz /tmp
ADD https://github.com/just-containers/s6-overlay/releases/download/v${S6_OVERLAY_VERSION}/s6-overlay-${S6_ARCH}.tar.xz /tmp
RUN \
  tar -C / -Jxpf /tmp/s6-overlay-noarch.tar.xz && \
  tar -C / -Jxpf /tmp/s6-overlay-${S6_ARCH}.tar.xz && \
  rm /tmp/s6-overlay*.tar.xz && \
  ln -s /run /var/run

COPY rootfs /

ENV RELAY relay.example.com
ENV ENCRYPTED_ONLY 0

EXPOSE 11115 11116 11116/udp 11117 11118 11119

HEALTHCHECK --interval=10s --timeout=5s CMD /usr/bin/healthcheck.sh

WORKDIR /data

VOLUME /data

ENTRYPOINT ["/init"]
