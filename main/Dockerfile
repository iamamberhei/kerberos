FROM node:16.17.1-alpine

WORKDIR /app

COPY kerberos-v1.1.5-node-v83-linuxmusl-x64.tar.gz /root/.npm/_prebuilds/f76494-kerberos-v1.1.5-node-v83-linuxmusl-x64.tar.gz

RUN set -eux; \
    apk add krb5 krb5-libs vim curl; \
    mkdir -p /root/.npm/_cacache/_prebuilds; \
    ln -s /root/.npm/_prebuilds/f76494-kerberos-v1.1.5-node-v83-linuxmusl-x64.tar.gz /root/.npm/_cacache/_prebuilds/f76494-kerberos-v1.1.5-node-v83-linuxmusl-x64.tar.gz

RUN apk update && apk add bash

CMD [ "node" ]