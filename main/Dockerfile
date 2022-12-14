FROM node:18.12.1-alpine AS prebuilder

WORKDIR /app

RUN set -eux; \
    apk add python3 make build-base krb5-dev git; \
    git clone https://github.com/mongodb-js/kerberos.git; \
    cd kerberos; \
    npm install -g node-gyp; \
    npm i; \
    npm run prebuild


FROM node:18.12.1-alpine AS node-kerberos

WORKDIR /app

# Install python/pip
ENV PYTHONUNBUFFERED=1
RUN apk add --update --no-cache python3 && ln -sf python3 /usr/bin/python
RUN python3 -m ensurepip
RUN pip3 install --no-cache --upgrade pip setuptools


COPY --from=prebuilder /app/kerberos/prebuilds/*.tar.gz /root/.npm/_prebuilds/

RUN set -eux; \
    apk add krb5 krb5-libs vim curl; \
    npm install -g node-gyp; \
    npm config set kerberos_local_prebuilds=/root/.npm/_prebuilds
    

RUN apk update && apk add bash

CMD [ "node" ]