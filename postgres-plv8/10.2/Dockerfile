# Docker image for PostgreSQL with the plv8 extension installed
# Note: building plv8 times out on Docker Hub, so instead we download pre-built binaries
# Provided by Ionx Solutions: https://www.ionxsolutions.com

# Begin by downloading binaries built on Debian stretch
FROM debian:stretch AS staging

ENV PLV8_VERSION 2.1.0
ENV PLV8_SHASUM="0baa249e16b2d03076353d82b99cec03cbf8ecfed934b4bc7c543748fbab95c4 plv8-${PLV8_VERSION}.7z"

RUN apt-get update
RUN apt-get install -y --no-install-recommends curl ca-certificates p7zip
RUN mkdir -p /tmp/plv8
RUN curl -o /tmp/plv8/plv8-${PLV8_VERSION}.7z -SL "https://www.ionxsolutions.com/files/plv8/${PLV8_VERSION}"
RUN cd /tmp/plv8 \
    && echo ${PLV8_SHASUM} | sha256sum -c \
    && 7zr x plv8-${PLV8_VERSION}.7z

# Copy the plv8 build output into an image based on postgres
FROM postgres:10.2
LABEL description="PostgreSQL with the plv8 extension installed" maintainer="support@ionxsolutions.com"
ENV PLV8_VERSION 2.1.0

COPY --from=staging /tmp/plv8/plv8.so /usr/lib/postgresql/${PG_MAJOR}/lib/plv8.so
COPY --from=staging /tmp/plv8/plv8.control /tmp/plv8/plv8--${PLV8_VERSION}.sql /usr/share/postgresql/${PG_MAJOR}/extension/

RUN chmod 0755 /usr/lib/postgresql/${PG_MAJOR}/lib/plv8.so \
    && chmod 0644 /usr/share/postgresql/${PG_MAJOR}/extension/plv8.control \
    && chmod 0644 /usr/share/postgresql/${PG_MAJOR}/extension/plv8--${PLV8_VERSION}.sql \
    && echo 'CREATE EXTENSION plv8;' > /docker-entrypoint-initdb.d/plv8.sql
