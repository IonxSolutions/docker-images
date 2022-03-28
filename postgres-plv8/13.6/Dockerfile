# Docker image for PostgreSQL with the plv8 extension installed
# Note: building plv8 times out on Docker Hub, so instead we download pre-built binaries
# Provided by Ionx Solutions: https://www.ionxsolutions.com

# Begin by downloading binaries built on Debian stretch-slim
FROM debian:stretch-slim AS staging

ENV PLV8_VERSION 2.3.15
ENV PLV8_SHASUM="d5f057d0307422c066ce87f077a22f6be7e407151a2b882270fa2420b6123dd4 plv8-${PLV8_VERSION}.7z"

RUN apt-get update
RUN apt-get install -y --no-install-recommends curl ca-certificates p7zip
RUN mkdir -p /tmp/plv8
RUN curl -o /tmp/plv8/plv8-${PLV8_VERSION}.7z -SL "https://www.ionxsolutions.com/files/plv8/${PLV8_VERSION}"
RUN cd /tmp/plv8 \
    && echo ${PLV8_SHASUM} | sha256sum -c \
    && 7zr x plv8-${PLV8_VERSION}.7z

# Copy the plv8 build output into an image based on postgres
FROM postgres:13.6
LABEL description="PostgreSQL 13.6 with the plv8 extension installed" maintainer="support@ionxsolutions.com"
ENV PLV8_VERSION 2.3.15

COPY --from=staging /tmp/plv8/plv8-${PLV8_VERSION}.so /usr/lib/postgresql/${PG_MAJOR}/lib/plv8-${PLV8_VERSION}.so
COPY --from=staging /tmp/plv8/plv8.control /tmp/plv8/plv8--${PLV8_VERSION}.sql /usr/share/postgresql/${PG_MAJOR}/extension/

RUN apt-get update \
    && apt-get install -y --no-install-recommends libc++1 \
    && rm -rf /var/lib/apt/lists/* \
    && chmod 0755 /usr/lib/postgresql/${PG_MAJOR}/lib/plv8-${PLV8_VERSION}.so \
    && chmod 0644 /usr/share/postgresql/${PG_MAJOR}/extension/plv8.control \
    && chmod 0644 /usr/share/postgresql/${PG_MAJOR}/extension/plv8--${PLV8_VERSION}.sql \
    && echo 'CREATE EXTENSION plv8;' > /docker-entrypoint-initdb.d/plv8.sql
