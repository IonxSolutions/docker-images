# Docker image for PostgreSQL with the plv8 extension installed
# https://www.ionxsolutions.com

FROM postgres:10.2

LABEL description="PostgreSQL with the plv8 extension installed" maintainer="support@ionxsolutions.com"

ENV PLV8_VERSION 2.1.0
ENV PLV8_SHASUM="207d712e919ab666936f42b29ff3eae413736b70745f5bfeb2d0910f0c017a5c ${PLV8_VERSION}.tar.gz"

RUN buildDeps="curl build-essential ca-certificates git python postgresql-server-dev-$PG_MAJOR" \
    && apt-get update \
    && apt-get install -y --no-install-recommends ${buildDeps} \
    && mkdir -p /tmp/build \
    && curl -o /tmp/build/${PLV8_VERSION}.tar.gz -SL "https://github.com/plv8/plv8/archive/v${PLV8_VERSION}.tar.gz" \
    && cd /tmp/build \
    && echo ${PLV8_SHASUM} | sha256sum -c \
    && tar -xzf /tmp/build/${PLV8_VERSION}.tar.gz -C /tmp/build/ \
    && cd /tmp/build/plv8-${PLV8_VERSION} \
    && make static \
    && make install \
    && strip /usr/lib/postgresql/${PG_MAJOR}/lib/plv8.so \
    && cd / \
    && rm -rf /tmp/build \
    && apt-get remove -y --purge ${buildDependencies} \
    && apt-get autoremove -y --purge \
    && rm -rf /var/lib/apt/lists/*

FROM postgres:10.2
ENV PLV8_VERSION 2.1.0
COPY --from=0 /usr/lib/postgresql/${PG_MAJOR}/lib/plv8.so /usr/lib/postgresql/${PG_MAJOR}/lib/plv8.so
COPY --from=0 /usr/share/postgresql/${PG_MAJOR}/extension/plv8.control /usr/share/postgresql/${PG_MAJOR}/extension/plv8.control
COPY --from=0 /usr/share/postgresql/${PG_MAJOR}/extension/plv8--${PLV8_VERSION}.sql /usr/share/postgresql/${PG_MAJOR}/extension/plv8--${PLV8_VERSION}.sql
RUN chmod 0755 /usr/lib/postgresql/${PG_MAJOR}/lib/plv8.so \
    && chmod 0644 /usr/share/postgresql/${PG_MAJOR}/extension/plv8.control \
    && chmod 0644 /usr/share/postgresql/${PG_MAJOR}/extension/plv8--${PLV8_VERSION}.sql \
    && echo 'CREATE EXTENSION plv8;' > /docker-entrypoint-initdb.d/plv8.sql
