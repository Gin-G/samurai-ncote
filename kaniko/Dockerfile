FROM gcr.io/kaniko-project/executor:debug AS kaniko
FROM alpine:3

RUN rm /var/spool/mail && \
    mv /var/mail /var/spool/mail && \
    ln -s spool/mail /var/mail

RUN apk update && \
    apk upgrade && \
    apk add --no-cache \
    bash \
    curl \
    cmake \
    gcc \
    g++ \
    make 

COPY --from=kaniko /kaniko /kaniko

ENV HOME=/root
ENV USER=root
ENV PATH=/kaniko:$PATH
ENV DOCKER_CONFIG='/kaniko/.docker'
ENV SSL_CERT_DIR=/kaniko/ssl/certs

WORKDIR /workspace

ENTRYPOINT ["/kaniko/executor"]