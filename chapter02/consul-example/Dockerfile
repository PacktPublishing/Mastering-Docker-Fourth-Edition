FROM alpine:latest
LABEL maintainer="Russ McKendrick <russ@mckendrick.io>"
LABEL description="An image with the latest version on Consul."

ENV CONSUL_VERSION 1.7.1
ENV CONSUL_SHA256 09f3583c6cd7b1f748c0c012ce9b3d96de95a6c0d2334327b74f7d72b1fa5054

RUN  apk add --update ca-certificates wget && \
     wget -O consul.zip https://releases.hashicorp.com/consul/${CONSUL_VERSION}/consul_${CONSUL_VERSION}_linux_amd64.zip && \
     echo "$CONSUL_SHA256 *consul.zip" | sha256sum -c - && \
     unzip consul.zip && \
     mv consul /bin/ && \
     rm -rf consul.zip && \
     rm -rf /tmp/* /var/cache/apk/*

EXPOSE 8300 8301 8301/udp 8302 8302/udp 8400 8500 8600 8600/udp

VOLUME [ "/data" ]

ENTRYPOINT [ "/bin/consul" ]
CMD [ "agent", "-data-dir", "/data", "-server", "-bootstrap-expect", "1", "-client=0.0.0.0"]