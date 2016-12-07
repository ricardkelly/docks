FROM alpine:latest
MAINTAINER Ricard Kelly <ricard@ricardkelly.com>
ENV REFRESHED_AT 2016-12-06
ENV PROD_NAME=vault \
    PROD_VERS=0.6.3 \
    PROD_HASH=8d28c4425e78a00c0f437393b7a87ff00bc3ce1aa0f10ef6538d1ba3181f1d08

RUN apk update && apk add openssl ca-certificates && rm -rf /var/cache/apk/*

WORKDIR /

ADD https://releases.hashicorp.com/${PROD_NAME}/${PROD_VERS}/${PROD_NAME}_${PROD_VERS}_linux_amd64.zip ${PROD_NAME}_${PROD_VERS}_linux_amd64.zip

RUN mkdir /app && mkdir /app/bin && mkdir /app/config && \
    echo "${PROD_HASH}  ${PROD_NAME}_${PROD_VERS}_linux_amd64.zip" | sha256sum -cw && \
    unzip -d /app/bin ${PROD_NAME}_${PROD_VERS}_linux_amd64.zip && \
    rm -r ${PROD_NAME}_${PROD_VERS}_linux_amd64.zip && \
    chmod 755 /app/bin/vault

ADD vault.hcl /app/config/vault.hcl

EXPOSE 8200

ENTRYPOINT ["/app/bin/vault"]
CMD ["server", "-config=/app/config/vault.hcl"]
