## Installing penpot
https://help.penpot.app/technical-guide/getting-started/docker/

## Penpot images

This is the docker compose file content

```yaml
## Common flags:

# demo-users

# email-verification

# log-emails

# log-invitation-tokens

# login-with-github

# login-with-gitlab

# login-with-google

# login-with-ldap

# login-with-oidc

# login-with-password

# prepl-server

# registration

# secure-session-cookies

# smtp

# smtp-debug

# telemetry

# webhooks

##

## You can read more about all available flags and other

## environment variables here:

## https://help.penpot.app/technical-guide/configuration/#penpot-configuration

#

# WARNING: if you're exposing Penpot to the internet, you should remove the flags

# 'disable-secure-session-cookies' and 'disable-email-verification'

x-flags: &penpot-flags

  PENPOT_FLAGS: disable-email-verification enable-smtp enable-prepl-server disable-secure-session-cookies enable-mcp enable-admin-console

  

x-uri: &penpot-public-uri

  PENPOT_PUBLIC_URI: http://localhost:9001

  

x-body-size: &penpot-http-body-size

  # Max body size

  PENPOT_HTTP_SERVER_MAX_BODY_SIZE: 367001600

  # Deprecation warning: this variable is deprecated. Use PENPOT_HTTP_SERVER_MAX_BODY (defaults to 367001600)

  PENPOT_HTTP_SERVER_MAX_MULTIPART_BODY_SIZE: 367001600

  

## Penpot SECRET KEY. It serves as a master key from which other keys for subsystems

## (eg http sessions, or invitations) are derived.

##

## We recommend to use a trully randomly generated

## 512 bits base64 encoded string here. You can generate one with:

##

## python3 -c "import secrets; print(secrets.token_urlsafe(64))"

x-secret-key: &penpot-secret-key

  PENPOT_SECRET_KEY: change-this-insecure-key

  

## Single database configuration block, shared by backend and admin-console.

## Don't touch them unless you are using custom postgresql connection parameters.

x-database: &penpot-database

  PENPOT_DATABASE_URI: postgresql://penpot-postgres/penpot

  PENPOT_DATABASE_USERNAME: penpot

  PENPOT_DATABASE_PASSWORD: penpot

  

networks:

  penpot:

  

volumes:

  penpot_postgres_v15:

  penpot_assets:

  # penpot_traefik:

  

services:

  ## Traefik service declaration example. Consider using it if you are going to expose

  ## penpot to the internet, or a different host than `localhost`.

  

  # traefik:

  #   image: traefik:v3.3

  #   networks:

  #     - penpot

  #   command:

  #     - "--api.insecure=true"

  #     - "--entryPoints.web.address=:80"

  #     - "--providers.docker=true"

  #     - "--providers.docker.exposedbydefault=false"

  #     - "--entryPoints.websecure.address=:443"

  #     - "--certificatesresolvers.letsencrypt.acme.tlschallenge=true"

  #     - "--certificatesresolvers.letsencrypt.acme.email=<EMAIL_ADDRESS>"

  #     - "--certificatesresolvers.letsencrypt.acme.storage=/traefik/acme.json"

  #   volumes:

  #     - "penpot_traefik:/traefik"

  #     - "/var/run/docker.sock:/var/run/docker.sock"

  #   ports:

  #     - "80:80"

  #     - "443:443"

  

  penpot-frontend:

    image: "penpotapp/frontend:${PENPOT_VERSION:-2.18}"

    restart: always

    ports:

      - 9001:8080

  

    volumes:

      - penpot_assets:/opt/data/assets

  

    depends_on:

      - penpot-backend

      - penpot-admin-console

      - penpot-mcp

      - penpot-exporter

  

    networks:

      - penpot

  

    # labels:

      # - "traefik.enable=true"

  

      # ## HTTPS: example of labels for the case where penpot will be exposed to the

      # ## internet with HTTPS using traefik.

  

      # - "traefik.http.routers.penpot-https.rule=Host(`<DOMAIN_NAME>`)"

      # - "traefik.http.routers.penpot-https.entrypoints=websecure"

      # - "traefik.http.routers.penpot-https.tls.certresolver=letsencrypt"

      # - "traefik.http.routers.penpot-https.tls=true"

  

    environment:

      << : [*penpot-flags, *penpot-http-body-size, *penpot-public-uri]

  

      # Don't touch it; this uses an internal docker network to

      # communicate with the admin-console.

      PENPOT_ADMIN_CONSOLE_URI: http://penpot-admin-console:3000

  

      # Set to "true" on hosts where IPv6 is disabled at kernel boot level.

      # PENPOT_DISABLE_IPV6_LISTEN: "true"

  

  penpot-backend:

    image: "penpotapp/backend:${PENPOT_VERSION:-2.18}"

    restart: always

  

    volumes:

      - penpot_assets:/opt/data/assets

  

    depends_on:

      penpot-postgres:

        condition: service_healthy

      penpot-valkey:

        condition: service_healthy

  

    networks:

      - penpot

  

    environment:

      << : [*penpot-flags, *penpot-public-uri, *penpot-http-body-size, *penpot-secret-key, *penpot-database]

  

      # Don't touch it; this uses an internal docker network to

      # communicate with the admin-console.

      PENPOT_ADMIN_CONSOLE_URI: http://penpot-admin-console:3000

  

      ## Valkey (or previously redis) is used for the websockets notifications. Don't touch

      ## unless the valkey container has different parameters or different name.

      PENPOT_REDIS_URI: redis://penpot-valkey/0

  

      ## Default configuration for assets storage: using filesystem based with all files

      ## stored in a docker volume.

      PENPOT_OBJECTS_STORAGE_BACKEND: fs

      PENPOT_OBJECTS_STORAGE_FS_DIRECTORY: /opt/data/assets

  

      ## Also can be configured to to use a S3 compatible storage.

      # AWS_ACCESS_KEY_ID: <KEY_ID>

      # AWS_SECRET_ACCESS_KEY: <ACCESS_KEY>

      # PENPOT_OBJECTS_STORAGE_BACKEND: s3

      # PENPOT_OBJECTS_STORAGE_S3_ENDPOINT: <ENDPOINT>

      # PENPOT_OBJECTS_STORAGE_S3_BUCKET: <BUKET_NAME>

  

      ## Telemetry. When enabled, a periodical process will send anonymous data about this

      ## instance. Telemetry data will enable us to learn how the application is used,

      ## based on real scenarios. If you want to help us, please leave it enabled. You can

      ## audit what data we send with the code available on github.

      PENPOT_TELEMETRY_ENABLED: "true"

      PENPOT_TELEMETRY_REFERER: compose

  

      ## Example SMTP/Email configuration. By default, emails are sent to the mailcatch

      ## service, but for production usage it is recommended to setup a real SMTP

      ## provider. Emails are used to confirm user registrations & invitations. Look below

      ## how the mailcatch service is configured.

      PENPOT_SMTP_DEFAULT_FROM: no-reply@example.com

      PENPOT_SMTP_DEFAULT_REPLY_TO: no-reply@example.com

      PENPOT_SMTP_HOST: penpot-mailcatch

      PENPOT_SMTP_PORT: 1025

      PENPOT_SMTP_USERNAME:

      PENPOT_SMTP_PASSWORD:

      PENPOT_SMTP_TLS: "false"

      PENPOT_SMTP_SSL: "false"

  

  penpot-admin-console:

    image: "penpotapp/admin-console:${PENPOT_VERSION:-2.18}"

    restart: always

  

    depends_on:

      penpot-postgres:

        condition: service_healthy

  

    networks:

      - penpot

  

    environment:

      << : [*penpot-public-uri, *penpot-secret-key, *penpot-database]

  

      # Don't touch it; this uses an internal docker network to

      # communicate with the frontend.

      PENPOT_INTERNAL_URI: http://penpot-frontend:8080

  

  penpot-mcp:

    image: "penpotapp/mcp:${PENPOT_VERSION:-2.18}"

    restart: always

    networks:

      - penpot

  

  penpot-exporter:

    image: "penpotapp/exporter:${PENPOT_VERSION:-2.18}"

    restart: always

  

    depends_on:

      penpot-valkey:

        condition: service_healthy

  

    networks:

      - penpot

  

    environment:

      << : [*penpot-flags, *penpot-secret-key, *penpot-public-uri]

  

      # Don't touch it; this uses an internal docker network to

      # communicate with the frontend.

      PENPOT_INTERNAL_URI: http://penpot-frontend:8080

  

      ## Valkey (or previously Redis) is used for the websockets notifications.

      PENPOT_REDIS_URI: redis://penpot-valkey/0

  

  penpot-postgres:

    image: "postgres:15"

    restart: always

    stop_signal: SIGINT

  

    healthcheck:

      test: ["CMD-SHELL", "pg_isready -U penpot"]

      interval: 2s

      timeout: 10s

      retries: 5

      start_period: 2s

  

    volumes:

      - penpot_postgres_v15:/var/lib/postgresql/data

  

    networks:

      - penpot

  

    environment:

      - POSTGRES_INITDB_ARGS=--data-checksums

      - POSTGRES_DB=penpot

      - POSTGRES_USER=penpot

      - POSTGRES_PASSWORD=penpot

  

  penpot-valkey:

    image: valkey/valkey:8.1

    restart: always

  

    healthcheck:

      test: ["CMD-SHELL", "valkey-cli ping | grep PONG"]

      interval: 1s

      timeout: 3s

      retries: 5

      start_period: 3s

  

    networks:

      - penpot

  

    environment:

      # You can increase the max memory size if you have sufficient resources,

      # although this should not be necessary.

      - VALKEY_EXTRA_FLAGS=--maxmemory 128mb --maxmemory-policy volatile-lfu

  

  ## A mailcatch service, used as temporal SMTP server. You can access via HTTP to the

  ## port 1080 for read all emails the penpot platform has sent. Should be only used as a

  ## temporal solution while no real SMTP provider is configured.

  

  penpot-mailcatch:

    image: sj26/mailcatcher:latest

    restart: always

    expose:

      - '1025'

    ports:

      - "1080:1080"

    networks:

      - penpot
```

 ✔ Image valkey/valkey:8.1                 Pulled                                                                  76.0s
 ✔ Image penpotapp/admin-console:2.18      Pulled                                                                  80.3s
 ✔ Image penpotapp/backend:2.18            Pulled                                                                 234.7s
 ✔ Image penpotapp/mcp:2.18                Pulled                                                                  92.4s
 ✔ Image sj26/mailcatcher:latest           Pulled                                                                 111.9s
 ✔ Image postgres:15                       Pulled                                                                 233.6s
 ✔ Image penpotapp/frontend:2.18           Pulled                                                                 254.8s
 ✔ Image penpotapp/exporter:2.18           Pulled                                                                 261.5s
 ✔ Volume penpot_penpot_assets             Created                                                                  0.0s
 ✔ Network penpot_penpot                   Created                                                                  0.1s
 ✔ Volume penpot_penpot_postgres_v15       Created                                                                  0.0s
 ✔ Container penpot-penpot-valkey-1        Healthy                                                                  5.4s
 ✔ Container penpot-penpot-mailcatch-1     Started                                                                  2.2s
 ✔ Container penpot-penpot-postgres-1      Healthy                                                                  4.6s
 ✔ Container penpot-penpot-mcp-1           Started                                                                  2.8s
 ✔ Container penpot-penpot-admin-console-1 Started                                                                  4.2s
 ✔ Container penpot-penpot-exporter-1      Started                                                                  5.0s
	 ✔ Container penpot-penpot-backend-1       Started                                                                  5.2s
 ✔ Container penpot-penpot-frontend-1      Started                                                                  4.7s

## Image valkey/valkey:8.1
The docker image is https://github.com/valkey-io/valkey-container/blob/mainline/8.1/debian/Dockerfile

```yaml
#
# NOTE: THIS DOCKERFILE IS GENERATED VIA "apply-templates.sh"
#
# PLEASE DO NOT EDIT IT DIRECTLY.
#

FROM debian:trixie-slim AS base

FROM base AS build

ENV VALKEY_DOWNLOAD_SHA c74e50cd83f6d398a3dc570e04ac2fe538249585d021f76ee2449bbf9ebd04ed

ADD "https://github.com/valkey-io/valkey/archive/refs/tags/8.1.10.tar.gz" /valkey.tar.gz

RUN set -eux; \
	\
	apt-get update; \
	apt-get install -y --no-install-recommends \
		dpkg-dev \
		gcc \
		libc6-dev \
		libssl-dev \
		libsystemd-dev \
		make \
	; \
	rm -rf /var/lib/apt/lists/*; \
	\
			echo "$VALKEY_DOWNLOAD_SHA *valkey.tar.gz" | sha256sum -c -; \
		\
	mkdir -p /usr/src/valkey; \
	tar -xzf valkey.tar.gz -C /usr/src/valkey --strip-components=1; \
	rm valkey.tar.gz; \
	\
# disable Valkey protected mode [1] as it is unnecessary in context of Docker
# (ports are not automatically exposed when running inside Docker, but rather explicitly by specifying -p / -P)
	grep -E '^ *createBoolConfig[(]"protected-mode",.*, *1 *,.*[)],$' /usr/src/valkey/src/config.c; \
	sed -ri 's!^( *createBoolConfig[(]"protected-mode",.*, *)1( *,.*[)],)$!\10\2!' /usr/src/valkey/src/config.c; \
	grep -E '^ *createBoolConfig[(]"protected-mode",.*, *0 *,.*[)],$' /usr/src/valkey/src/config.c; \
# for future reference, we modify this directly in the source instead of just supplying a default configuration flag because apparently "if you specify any argument to valkey-server, [it assumes] you are going to specify everything"
# (more exactly, this makes sure the default behavior of "save on SIGTERM" stays functional by default)
	\
# https://github.com/jemalloc/jemalloc/issues/467 -- we need to patch the "./configure" for the bundled jemalloc to match how Debian compiles, for compatibility
# (also, we do cross-builds, so we need to embed the appropriate "--build=xxx" values to that "./configure" invocation)
	gnuArch="$(dpkg-architecture --query DEB_BUILD_GNU_TYPE)"; \
	extraJemallocConfigureFlags="--build=$gnuArch"; \
# https://salsa.debian.org/debian/jemalloc/-/blob/c0a88c37a551be7d12e4863435365c9a6a51525f/debian/rules#L8-23
	dpkgArch="$(dpkg --print-architecture)"; \
	case "${dpkgArch##*-}" in \
		amd64 | i386 | x32) extraJemallocConfigureFlags="$extraJemallocConfigureFlags --with-lg-page=12" ;; \
		*) extraJemallocConfigureFlags="$extraJemallocConfigureFlags --with-lg-page=16" ;; \
	esac; \
	extraJemallocConfigureFlags="$extraJemallocConfigureFlags --with-lg-hugepage=21"; \
	grep -F 'cd jemalloc && ./configure ' /usr/src/valkey/deps/Makefile; \
	sed -ri 's!cd jemalloc && ./configure !&'"$extraJemallocConfigureFlags"' !' /usr/src/valkey/deps/Makefile; \
	grep -F "cd jemalloc && ./configure $extraJemallocConfigureFlags " /usr/src/valkey/deps/Makefile; \
	\
	echo "Version 8.1.10 is 8.1 or higher - enabling USE_FAST_FLOAT"; \
			apt-get update; \
		apt-get install -y --no-install-recommends g++; \
		rm -rf /var/lib/apt/lists/*; \
		export BUILD_TLS=yes USE_FAST_FLOAT=yes; \
	export USE_SYSTEMD=yes; \
	make -C /usr/src/valkey -j "$(nproc)" all; \
	make -C /usr/src/valkey install; \
	\
	serverMd5="$(md5sum /usr/local/bin/valkey-server | cut -d' ' -f1)"; export serverMd5; \
	find /usr/local/bin/valkey* -maxdepth 0 \
		-type f -not -name valkey-server \
		-exec sh -eux -c ' \
			md5="$(md5sum "$1" | cut -d" " -f1)"; \
			test "$md5" = "$serverMd5"; \
		' -- '{}' ';' \
		-exec ln -svfT 'valkey-server' '{}' ';' \
	; \
	\
	SPDX_CREATED="$(date -u +%Y-%m-%dT%H:%M:%SZ)"; \
	SPDX_UUID="$(cat /proc/sys/kernel/random/uuid)"; \
	echo '{"spdxVersion":"SPDX-2.3","dataLicense":"CC0-1.0","SPDXID":"SPDXRef-DOCUMENT","name":"valkey-server-sbom","documentNamespace":"https://valkey.io/spdxdocs/valkey-server-sbom-8.1.10-debian-trixie-@SPDX_UUID@","creationInfo":{"created":"@SPDX_CREATED@","creators":["Organization: The Valkey Project","Tool: valkey-container"]},"packages":[{"name":"valkey-server","versionInfo":"8.1.10","SPDXID":"SPDXRef-Package--valkey-server","supplier":"Organization: The Valkey Project","downloadLocation":"https://github.com/valkey-io/valkey/archive/refs/tags/8.1.10.tar.gz","filesAnalyzed":false,"externalRefs":[{"referenceCategory":"PACKAGE-MANAGER","referenceType":"purl","referenceLocator":"pkg:generic/valkey-server@8.1.10?os_name=debian&os_version=trixie"},{"referenceCategory":"SECURITY","referenceType":"cpe23Type","referenceLocator":"cpe:2.3:a:lfprojects:valkey:8.1.10:*:*:*:*:*:*:*"}],"licenseDeclared":"BSD-3-Clause"}],"relationships":[{"spdxElementId":"SPDXRef-DOCUMENT","relationshipType":"DESCRIBES","relatedSpdxElement":"SPDXRef-Package--valkey-server"}]}' \
		| sed -e "s|@SPDX_CREATED@|$SPDX_CREATED|g" -e "s|@SPDX_UUID@|$SPDX_UUID|g" > /usr/local/valkey.spdx.json

FROM base

ENV VALKEY_VERSION 8.1.10

LABEL org.opencontainers.image.source="https://github.com/valkey-io/valkey"

# add our user and group first to make sure their IDs get assigned consistently, regardless of whatever dependencies get added
RUN set -eux; \
	groupadd -r -g 999 valkey; \
	useradd -r -g valkey -u 999 valkey

# runtime dependencies
RUN set -eux; \
	apt-get update; \
	apt-get install -y --no-install-recommends \
# add tzdata explicitly for https://github.com/docker-library/redis/issues/138 (see also https://bugs.debian.org/837060 and related)
		tzdata \
		libssl3t64 \
		# add tini to act as PID 1 and reap orphaned/zombie processes
		tini \
	; \
	rm -rf /var/lib/apt/lists/*

# Install valkey built earlier
COPY --from=build /usr/local /usr/local
RUN mkdir /data && \
	chown valkey:valkey /data && \
	chmod 1777 /data && \
	mkdir -p /run/valkey && \
	chown valkey:valkey /run/valkey && \
	chmod 1777 /run/valkey && \
	valkey-cli --version && \
	valkey-server --version
WORKDIR /data

COPY docker-entrypoint.sh /usr/local/bin/
ENTRYPOINT ["tini", "--", "docker-entrypoint.sh"]

EXPOSE 6379
CMD ["valkey-server"]
```

## Image penpotapp/admin-console:2.18
Use command ` docker image inspect penpotapp/admin-console:2.18 | yq -P`


```yaml
Id: sha256:5935b5adbf33eb7abaabfab657fe8f5d465cac08e62e340f932ddb35ce0f311f
  RepoTags:
    - penpotapp/admin-console:2.18
  RepoDigests:
    - penpotapp/admin-console@sha256:5935b5adbf33eb7abaabfab657fe8f5d465cac08e62e340f932ddb35ce0f311f
  Comment: buildkit.dockerfile.v0
  Created: "2026-09-22T09:45:05.041886176Z"
  Config:
    User: 65532:65532
    ExposedPorts:
      3000/tcp: {}
    Env:
      - NODE_VERSION=24.20.0-0
      - PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
    Cmd:
      - node
      - docker-start-admin-console.mjs
    WorkingDir: /nitrate
    Labels:
      bundle_version: 2.18.0-RC4-1-gd8dd1b8
      com.docker.dhi.chain-id: sha256:3bfdf65cd0221ab05b6157d45438b4177dcd00cba79c185335289bd65d5b13bf
      com.docker.dhi.compliance: cis
      com.docker.dhi.created: "2026-08-28T09:08:28Z"
      com.docker.dhi.date.end-of-life: "2028-04-30"
      com.docker.dhi.date.release: "2025-05-06"
      com.docker.dhi.definition: image/node/debian-13/24
      com.docker.dhi.distro: debian-13
      com.docker.dhi.entitlement: public
      com.docker.dhi.flavor: ""
      com.docker.dhi.name: dhi/node
      com.docker.dhi.package-manager: ""
      com.docker.dhi.shell: ""
      com.docker.dhi.title: Node.js 24.x
      com.docker.dhi.url: https://dhi.io/catalog/node
      com.docker.dhi.variant: runtime
      com.docker.dhi.version: 24.20.0-0-debian13
      org.opencontainers.image.created: "2026-09-22T16:35:42.557Z"
      org.opencontainers.image.description: ""
      org.opencontainers.image.licenses: NOASSERTION
      org.opencontainers.image.revision: 9a009dfcfbed40c8d0ca2120f97d58fda3886461
      org.opencontainers.image.source: https://github.com/penpot/penpot-nitrate
      org.opencontainers.image.title: penpot-nitrate
      org.opencontainers.image.url: https://github.com/penpot/penpot-nitrate
      org.opencontainers.image.version: develop
    ArgsEscaped: true
  Architecture: amd64
  Os: linux
  Size: 568134830
  RootFS:
    Type: layers
    Layers:
      - sha256:f721c29b36d3419040dd50a6e355508db1a071ab90a389adaf1fed2b1e52d2c7
      - sha256:a369a71b77e052ef929e3b027dfb22f68a340c51fc0364bda764834e58e47b52
      - sha256:8a6e6b8e3dfc3a99f5707c026ce2cc1ea2bb450e29dd2286c296e7e918525216
      - sha256:310d783b3ceda4b86877422031e04625c593d18cf768086612b20a3579bf2c47
      - sha256:19d3e5a2fb0b741659de28bdf9321963c5eda4445050db4e15575b52935ed383
      - sha256:225c662a37974305bd9485e7fa36ce87c9716670d551e7f4209cdd2bbc441b44
      - sha256:5681ccc9dc67caa32c9b90f00320ac521f3e184547411048d542986e692664dc
      - sha256:0be8ea545348a8bd2a8c112c4c2e647ba61ff0622bc165e53ccce91fe3c2019a
      - sha256:373cb0bf0704d34453dc11abd8b9196a6c9ad7796787c267cb57286f83f3d2c2
      - sha256:34f64f125040dfa8542999290114939c7ce6e3e86034bbe666f808fa8c4611ef
      - sha256:9e49500b0b23bddefbe9009050efd3a76af10d6f1e9bbb411b628748b3febcc6
      - sha256:81cc19fab7897f62305ea86f85a3b79102bd026828eebdb6bbba1f4c64031b63
      - sha256:d08c7ca34fef0584a3b65dc49ae806730a3a3e88e263dce170d4701acd4287bd
      - sha256:0dd4b21ab17a256c6aaef48a9f61390433b803d735dbc53027dec20384c7875f
  Metadata:
    LastTagTime: "2026-10-21T06:36:33.374797216Z"
  Descriptor:
    mediaType: application/vnd.oci.image.index.v1+json
    digest: sha256:5935b5adbf33eb7abaabfab657fe8f5d465cac08e62e340f932ddb35ce0f311f
    size: 1375
  Identity:
    Pull:
      - Repository: docker.io/penpotapp/admin-console

```

## penpotapp/backend:2.18

`docker image inspect penpotapp/backend:2.18`

```json
[
    {
        "Id": "sha256:2df1b3440d2a82cc3571db211b4ffdfa2b89ccc910759e8d5e9387fb62971b5c",
        "RepoTags": [
            "penpotapp/backend:2.18"
        ],
        "RepoDigests": [
            "penpotapp/backend@sha256:2df1b3440d2a82cc3571db211b4ffdfa2b89ccc910759e8d5e9387fb62971b5c"
        ],
        "Comment": "buildkit.dockerfile.v0",
        "Created": "2026-10-06T12:35:01.521679048Z",
        "Config": {
            "User": "penpot:penpot",
            "Env": [
                "DEBIAN_FRONTEND=noninteractive",
                "PATH=/opt/jre/bin:/opt/imagick/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "LANG=C.UTF-8",
                "LC_ALL=C.UTF-8",
                "JAVA_HOME=/opt/jre",
                "TZ=Etc/UTC",
                "LD_LIBRARY_PATH=/opt/imagick/lib/deps"
            ],
            "Cmd": [
                "/bin/bash",
                "run.sh"
            ],
            "WorkingDir": "/opt/penpot/backend",
            "Labels": {
                "bundle_version": "2.18.3",
                "com.docker.dhi.chain-id": "sha256:67f5c1ee4db38b527b48d04ed3dbf27ff9bf8d7e4a74196ada45fdf3c1dd3511",
                "com.docker.dhi.compliance": "cis",
                "com.docker.dhi.created": "2026-09-01T21:37:30Z",
                "com.docker.dhi.date.end-of-life": "2028-08-09",
                "com.docker.dhi.date.release": "2025-08-09",
                "com.docker.dhi.definition": "image/debian-base/debian-13/13-dev",
                "com.docker.dhi.distro": "debian-13",
                "com.docker.dhi.entitlement": "public",
                "com.docker.dhi.flavor": "",
                "com.docker.dhi.name": "dhi/debian-base",
                "com.docker.dhi.package-manager": "apt",
                "com.docker.dhi.shell": "bash",
                "com.docker.dhi.title": "Debian 13 Base (dev)",
                "com.docker.dhi.url": "https://dhi.io/catalog/debian-base",
                "com.docker.dhi.variant": "dev",
                "com.docker.dhi.version": "trixie-debian13-dev",
                "maintainer": "Penpot <docker@penpot.app>",
                "org.opencontainers.image.created": "2026-10-06T12:34:03.436Z",
                "org.opencontainers.image.description": "Penpot: The open-source design platform for Product teams that need scalable collaboration.",
                "org.opencontainers.image.licenses": "MPL-2.0",
                "org.opencontainers.image.revision": "ff7a66f51938b2293260ea27a64e2c4e0833b5e3",
                "org.opencontainers.image.source": "https://github.com/penpot/penpot",
                "org.opencontainers.image.title": "penpot",
                "org.opencontainers.image.url": "https://github.com/penpot/penpot",
                "org.opencontainers.image.version": "2.18.3"
            },
            "ArgsEscaped": true
        },
        "Architecture": "amd64",
        "Os": "linux",
        "Size": 1203465713,
        "RootFS": {
            "Type": "layers",
            "Layers": [
                "sha256:6a88f393089c2ab65b9c702ee97a5d3f40a57d910f12bd2d1e405413942af10f",
                "sha256:c2a8870d390f4ca654a7ecf8a1d475b726a9b296be0e73c560480e1018c7ad31",
                "sha256:f36892eee1cba42147067916906723e2a590b585e8bdef271677d28f1821b8ba",
                "sha256:5f70bf18a086007016e948b04aed3b82103a36bea41755b6cddfaf10ace3c6ef",
                "sha256:4e83c71747b8c156f4538f8a06d502367bd8459ffd5ae7d67ead81ce41eedca0",
                "sha256:5f70bf18a086007016e948b04aed3b82103a36bea41755b6cddfaf10ace3c6ef",
                "sha256:e92f455a42a69d7ff1a5b1428548e4a641544fdd5c1bfcbfcf88ac6441e64ef0",
                "sha256:5f70bf18a086007016e948b04aed3b82103a36bea41755b6cddfaf10ace3c6ef",
                "sha256:1b2f919e7c0b48bf43b36911bd9fa945885b8f2ed64597af9b2f169906074eed",
                "sha256:5f70bf18a086007016e948b04aed3b82103a36bea41755b6cddfaf10ace3c6ef",
                "sha256:f3015762361c282bf1b560c4532583bc6a385ca513c90fb4dd9875dff31d07a5",
                "sha256:5f70bf18a086007016e948b04aed3b82103a36bea41755b6cddfaf10ace3c6ef",
                "sha256:78af550ce6c9bfa743037ab221e64355401c0b03c7686e67505f9ebb21c7b820",
                "sha256:ee1c63252eaa0128c83f9404a98a91a6432c27f45e21c9c5335c1dc100d65447",
                "sha256:544dc3676540f93040c6869a126287c7561ee26bc7c5e67ccccace4dd3165c1b",
                "sha256:bfedf8156c878bd8fe38a8d9fbfbfbe48e6d67e76a4aca7c0ecb2cea924c8a55",
                "sha256:acf8418d215508bcab6adbe34d7d5f78d1b73931d100e93508d1eacf9cda70c1",
                "sha256:82be09a1187cbe3d4d84c958f75035bc71789411771af2f3be10631c9f4cd4c7",
                "sha256:c2de87dfb93233dd3996500cbd176039065842bed3f193c504d3166638241134",
                "sha256:264ba9c51c32a2a37cb306dce5db6dda3323b098fd0a9483f5b326c6510d3bcc",
                "sha256:5f70bf18a086007016e948b04aed3b82103a36bea41755b6cddfaf10ace3c6ef"
            ]
        },
        "Metadata": {
            "LastTagTime": "2026-10-21T06:39:07.78112783Z"
        },
        "Descriptor": {
            "mediaType": "application/vnd.oci.image.index.v1+json",
            "digest": "sha256:2df1b3440d2a82cc3571db211b4ffdfa2b89ccc910759e8d5e9387fb62971b5c",
            "size": 1375
        },
        "Identity": {
            "Pull": [
                {
                    "Repository": "docker.io/penpotapp/backend"
                }
            ]
        }
    }
]

```

## penpotapp/mcp
`docker image inspect penpotapp/mcp:2.18`

```json
[
    {
        "Id": "sha256:5e811e6eeb179d80d8781fb0ffd2991560785d150b3676f1ac5e28d63ba9f7c2",
        "RepoTags": [
            "penpotapp/mcp:2.18"
        ],
        "RepoDigests": [
            "penpotapp/mcp@sha256:5e811e6eeb179d80d8781fb0ffd2991560785d150b3676f1ac5e28d63ba9f7c2"
        ],
        "Comment": "buildkit.dockerfile.v0",
        "Created": "2026-10-06T12:37:23.831980783Z",
        "Config": {
            "User": "node",
            "Env": [
                "NODE_VERSION=24.20.0-0",
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "LANG=en_US.UTF-8",
                "LC_ALL=en_US.UTF-8",
                "PENPOT_MCP_SERVER_HOST=0.0.0.0"
            ],
            "Cmd": [
                "node",
                "index.js",
                "--multi-user"
            ],
            "WorkingDir": "/opt/penpot/mcp",
            "Labels": {
                "bundle_version": "2.18.3",
                "com.docker.dhi.chain-id": "sha256:3bfdf65cd0221ab05b6157d45438b4177dcd00cba79c185335289bd65d5b13bf",
                "com.docker.dhi.compliance": "cis",
                "com.docker.dhi.created": "2026-08-28T09:08:28Z",
                "com.docker.dhi.date.end-of-life": "2028-04-30",
                "com.docker.dhi.date.release": "2025-05-06",
                "com.docker.dhi.definition": "image/node/debian-13/24",
                "com.docker.dhi.distro": "debian-13",
                "com.docker.dhi.entitlement": "public",
                "com.docker.dhi.flavor": "",
                "com.docker.dhi.name": "dhi/node",
                "com.docker.dhi.package-manager": "",
                "com.docker.dhi.shell": "",
                "com.docker.dhi.title": "Node.js 24.x",
                "com.docker.dhi.url": "https://dhi.io/catalog/node",
                "com.docker.dhi.variant": "runtime",
                "com.docker.dhi.version": "24.20.0-0-debian13",
                "maintainer": "Penpot <docker@penpot.app>",
                "org.opencontainers.image.created": "2026-10-06T12:37:06.632Z",
                "org.opencontainers.image.description": "Penpot: The open-source design platform for Product teams that need scalable collaboration.",
                "org.opencontainers.image.licenses": "MPL-2.0",
                "org.opencontainers.image.revision": "ff7a66f51938b2293260ea27a64e2c4e0833b5e3",
                "org.opencontainers.image.source": "https://github.com/penpot/penpot",
                "org.opencontainers.image.title": "penpot",
                "org.opencontainers.image.url": "https://github.com/penpot/penpot",
                "org.opencontainers.image.version": "2.18.3"
            },
            "ArgsEscaped": true
        },
        "Architecture": "amd64",
        "Os": "linux",
        "Size": 280064803,
        "RootFS": {
            "Type": "layers",
            "Layers": [
                "sha256:f721c29b36d3419040dd50a6e355508db1a071ab90a389adaf1fed2b1e52d2c7",
                "sha256:a369a71b77e052ef929e3b027dfb22f68a340c51fc0364bda764834e58e47b52",
                "sha256:8a6e6b8e3dfc3a99f5707c026ce2cc1ea2bb450e29dd2286c296e7e918525216",
                "sha256:310d783b3ceda4b86877422031e04625c593d18cf768086612b20a3579bf2c47",
                "sha256:19d3e5a2fb0b741659de28bdf9321963c5eda4445050db4e15575b52935ed383",
                "sha256:225c662a37974305bd9485e7fa36ce87c9716670d551e7f4209cdd2bbc441b44",
                "sha256:2dc1be3e85df022a46036640444c4f4f1f9441d9e335c1267ec7ccc148d1f777",
                "sha256:5f70bf18a086007016e948b04aed3b82103a36bea41755b6cddfaf10ace3c6ef"
            ]
        },
        "Metadata": {
            "LastTagTime": "2026-10-21T06:36:45.450454772Z"
        },
        "Descriptor": {
            "mediaType": "application/vnd.oci.image.index.v1+json",
            "digest": "sha256:5e811e6eeb179d80d8781fb0ffd2991560785d150b3676f1ac5e28d63ba9f7c2",
            "size": 1375
        },
        "Identity": {
            "Pull": [
                {
                    "Repository": "docker.io/penpotapp/mcp"
                }
            ]
        }
    }
]
```

## sj26/mailcatcher
` docker image inspect sj26/mailcatcher:latest`

```json
[
    {
        "Id": "sha256:572048324658d2198e0a96785cca4f0260f2c4cadb2cb057bd837b9ee0c60533",
        "RepoTags": [
            "sj26/mailcatcher:latest"
        ],
        "RepoDigests": [
            "sj26/mailcatcher@sha256:572048324658d2198e0a96785cca4f0260f2c4cadb2cb057bd837b9ee0c60533"
        ],
        "Comment": "buildkit.dockerfile.v0",
        "Created": "2026-09-03T00:59:08.182264754Z",
        "Author": "Samuel Cochran <sj26@sj26.com>",
        "Config": {
            "ExposedPorts": {
                "1025/tcp": {},
                "1080/tcp": {}
            },
            "Env": [
                "PATH=/usr/local/bundle/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "LANG=C.UTF-8",
                "RUBY_VERSION=3.4.10",
                "RUBY_DOWNLOAD_URL=https://cache.ruby-lang.org/pub/ruby/3.4/ruby-3.4.10.tar.xz",
                "RUBY_DOWNLOAD_SHA256=6f32ad662baafc228d12030dbcd284f83b034dd4337b300dc84ac74d11a1eb68",
                "GEM_HOME=/usr/local/bundle",
                "BUNDLE_SILENCE_ROOT_WARNING=1",
                "BUNDLE_APP_CONFIG=/usr/local/bundle"
            ],
            "Entrypoint": [
                "mailcatcher",
                "--foreground"
            ],
            "Cmd": [
                "--ip",
                "0.0.0.0"
            ],
            "WorkingDir": "/",
            "Labels": {
                "org.opencontainers.image.created": "2026-09-03T00:58:45.371Z",
                "org.opencontainers.image.description": "MailCatcher runs an SMTP server and displays caught email in a web interface.",
                "org.opencontainers.image.licenses": "MIT",
                "org.opencontainers.image.revision": "43e488e2a5692532c131a87d5bd16a973ee8db56",
                "org.opencontainers.image.source": "https://github.com/sj26/mailcatcher",
                "org.opencontainers.image.title": "mailcatcher",
                "org.opencontainers.image.url": "https://github.com/sj26/mailcatcher",
                "org.opencontainers.image.version": "v0.11.0"
            },
            "ArgsEscaped": true
        },
        "Architecture": "amd64",
        "Os": "linux",
        "Size": 165808239,
        "RootFS": {
            "Type": "layers",
            "Layers": [
                "sha256:34884abbe92863fce933ed7c39c0e045631af0ed86d5cc0dfbdf9fdca426ce3c",
                "sha256:ed61e5002960f021a8cf38f0f18e5e000f2d206b98af561dd93a48be5e2b1e40",
                "sha256:50026bb45cdb8bcf81b7786a0bf62a80bf13545d440b0ed8aa6112a525bcdeef",
                "sha256:278e235e76c84374b9615567dd052320e8238bf6c50ba53b0af90c322c3389d4",
                "sha256:80be1a8ae91d79ac16ec99d7e21e728921e43e4e47b3f298f3bb18dd712cedd7"
            ]
        },
        "Metadata": {
            "LastTagTime": "2026-10-21T06:37:04.910414599Z"
        },
        "Descriptor": {
            "mediaType": "application/vnd.oci.image.index.v1+json",
            "digest": "sha256:572048324658d2198e0a96785cca4f0260f2c4cadb2cb057bd837b9ee0c60533",
            "size": 1609
        },
        "Identity": {
            "Pull": [
                {
                    "Repository": "docker.io/sj26/mailcatcher"
                }
            ]
        }
    }
]
```

## postgres

```json
[
    {
        "Id": "sha256:77cb52de60c9c248e26267a6707db24f8433461ccd60b2c861900dcfe0c5a68e",
        "RepoTags": [
            "postgres:15"
        ],
        "RepoDigests": [
            "postgres@sha256:77cb52de60c9c248e26267a6707db24f8433461ccd60b2c861900dcfe0c5a68e"
        ],
        "Comment": "buildkit.dockerfile.v0",
        "Created": "2026-10-21T00:38:03.431359497Z",
        "Config": {
            "ExposedPorts": {
                "5432/tcp": {}
            },
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/lib/postgresql/15/bin",
                "GOSU_VERSION=1.19",
                "LANG=en_US.utf8",
                "PG_MAJOR=15",
                "PG_VERSION=15.19-1.pgdg13+2",
                "PGDATA=/var/lib/postgresql/data"
            ],
            "Entrypoint": [
                "docker-entrypoint.sh"
            ],
            "Cmd": [
                "postgres"
            ],
            "Volumes": {
                "/var/lib/postgresql/data": {}
            },
            "StopSignal": "SIGINT"
        },
        "Architecture": "amd64",
        "Os": "linux",
        "Size": 627586818,
        "RootFS": {
            "Type": "layers",
            "Layers": [
                "sha256:a70f6272827f64e1427d048ced77491aab5d64ab95725e56920802ff391197d7",
                "sha256:bad7ac542f8f71815a4e3eb1ae935f43cef7e5148ed932a34fcea165330d740f",
                "sha256:10daca7c4475cf31a0de1d572ba547d258dd44d869da1eb8536ea9e54f4fdd31",
                "sha256:0bed2a4a850052272fe3e0d07dd34963f93c492e7f547a129753200d795aca7b",
                "sha256:e1eb3edef25cf9e04a8bdb648e35f832f1d5936ce6e14b820371e1b6a166ab78",
                "sha256:86de9887e546727c325a740553db1143e2dc5aca24a891559189d601d9b81117",
                "sha256:8978834d28764c3ed7183dd9bc52391e44a12068cca0d2beaa637fce907e513f",
                "sha256:163c4897d031bb0ae3a311206c43894ee91ff3aead5c85db9c77044cca6751a9",
                "sha256:3fccdeca7c3cf1028fa60c8e24c59efdc11b5338d6503a113255b46cc12c8c9f",
                "sha256:efb0551e9426bc3d171819cfef776f62157f9dc1b219b21cef554345ec9b50c3",
                "sha256:6e8082627ede9ddc287d627956fb25ed25b16598beb317f33a9f627cfc2c3f88",
                "sha256:76f6bcb7dd4359f0c940314bb0ef4e4eba07403e143aa35f278d5f8b71be79e2",
                "sha256:8cd4531fc5ba33da3bcf5d6c66c386fc9db4a77263d02c369340f2885238c220",
                "sha256:ef9399aa3a28afb10e3a98ee39946f9e05ec0ba08f5215ca5f12282afdd53cea"
            ]
        },
        "Metadata": {
            "LastTagTime": "2026-10-21T06:39:06.703500078Z"
        },
        "Descriptor": {
            "mediaType": "application/vnd.oci.image.index.v1+json",
            "digest": "sha256:77cb52de60c9c248e26267a6707db24f8433461ccd60b2c861900dcfe0c5a68e",
            "size": 10237
        },
        "Identity": {
            "Pull": [
                {
                    "Repository": "docker.io/library/postgres"
                }
            ]
        }
    }
]
```

## penpotapp/frontend:2.18

```json
[
    {
        "Id": "sha256:bb8abe27d53de84c95597f2c02c0e702b2779971fb0703e543f9ecf183e999f6",
        "RepoTags": [
            "penpotapp/frontend:2.18"
        ],
        "RepoDigests": [
            "penpotapp/frontend@sha256:bb8abe27d53de84c95597f2c02c0e702b2779971fb0703e543f9ecf183e999f6"
        ],
        "Comment": "buildkit.dockerfile.v0",
        "Created": "2026-10-06T12:34:35.565566802Z",
        "Config": {
            "User": "penpot:penpot",
            "ExposedPorts": {
                "8080/tcp": {}
            },
            "Env": [
                "DEBIAN_FRONTEND=noninteractive",
                "NGINX_VERSION=1.31.1",
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "PKG_RELEASE=1~trixie"
            ],
            "Entrypoint": [
                "/bin/bash",
                "/entrypoint.sh"
            ],
            "Cmd": [
                "nginx",
                "-g",
                "daemon off;"
            ],
            "WorkingDir": "/",
            "Labels": {
                "bundle_version": "2.18.3",
                "com.docker.dhi.chain-id": "sha256:b04728864ff11f748c645d65cdf440e20dbccfaa42bb224c6da6f5130f368bf5",
                "com.docker.dhi.compliance": "cis",
                "com.docker.dhi.created": "2026-06-04T11:16:26Z",
                "com.docker.dhi.date.release": "2025-06-24",
                "com.docker.dhi.definition": "image/nginx/debian-13/mainline-dev",
                "com.docker.dhi.distro": "debian-13",
                "com.docker.dhi.entitlement": "public",
                "com.docker.dhi.flavor": "",
                "com.docker.dhi.name": "dhi/nginx",
                "com.docker.dhi.package-manager": "apt",
                "com.docker.dhi.shell": "bash",
                "com.docker.dhi.title": "Nginx mainline (dev)",
                "com.docker.dhi.url": "https://dhi.io/catalog/nginx",
                "com.docker.dhi.variant": "dev",
                "com.docker.dhi.version": "1.31.1-debian13-dev",
                "maintainer": "Penpot <docker@penpot.app>",
                "org.opencontainers.image.created": "2026-10-06T12:34:03.556Z",
                "org.opencontainers.image.description": "Penpot: The open-source design platform for Product teams that need scalable collaboration.",
                "org.opencontainers.image.licenses": "MPL-2.0",
                "org.opencontainers.image.revision": "ff7a66f51938b2293260ea27a64e2c4e0833b5e3",
                "org.opencontainers.image.source": "https://github.com/penpot/penpot",
                "org.opencontainers.image.title": "penpot",
                "org.opencontainers.image.url": "https://github.com/penpot/penpot",
                "org.opencontainers.image.version": "2.18.3"
            },
            "ArgsEscaped": true
        },
        "Architecture": "amd64",
        "Os": "linux",
        "Size": 1020746933,
        "RootFS": {
            "Type": "layers",
            "Layers": [
                "sha256:e5b5114f40cc767e5dcc72bc8d603b130e534b43b8d09878db3539b3154a56cc",
                "sha256:2105c0bc46a57d9d2e6316e054b7933e6812eb28acdf721cefceb162f80b4b53",
                "sha256:4894da42d51d7aceffefa0fd5f38db859d3ce81b8143848155da3e2c062c8b17",
                "sha256:d0e1ed2a25a25c3104023a44e8f3d5774413230ab3b4e94d312b8a904b2f87f2",
                "sha256:23d7fc70e6c05be3c49e116c264a2d8229554ca392d8dc0b2f8482bf33e25332",
                "sha256:c81b8b6e3a8a174caa0d455f79d07924bbc50887cd4a2763413e6aa850842ac4",
                "sha256:7a8e7db9f08a50d0cdb6cb8afb6e721a5d0b62687dbd9db7fc0d5fd564363355",
                "sha256:f1a93f6f7450f371f9bdac9a6bbf481d11152e6ce070ea610b2a261b7434a9b7",
                "sha256:ce9413644e4b4ac67a4b44cffb1bb7c0babdff2d9963265699e2c150a61ad3cb",
                "sha256:4536435be7d72d04119b45f2048b45c7fe702fb2ad48600bb3546497cd8004c4",
                "sha256:a8340561b8d761b13329fae83214b30588cf2bb855bd633600a6c8f26299ae6c",
                "sha256:01c0503062b02529433329729aed645675dc0566a29afe4ab65f6d13600a528a",
                "sha256:c8462c70b44593234d57c15df2803c888c383e58828d65103a57219aa572c9d6",
                "sha256:8385665c7ef3dd46885c6a2e524fa227cdef48a8eadacbaa5951da0e79ca6edb",
                "sha256:7121a0ce1a9cdc6d2595658cf3713c90837ea32a50fb3202e9eb384c9a649b72",
                "sha256:07617bbd40777c2cc196860629247f9d36db1bafc82bf738563d94aee9b8d0df",
                "sha256:055f850627e748211ba46d2becc1ff1f12d77b21bb41d087b613b7963618b9c8",
                "sha256:ec4d28316dd08ee03aee87e5026b79d77dab65fb09208c15238d49eaff0500c4",
                "sha256:f7287daa49aa6f796bee7c37d3fad40996214d394307274f1fe5c2a68767a970",
                "sha256:3af3e73c329dd453b3fe55b92e2a7ef5642f6ba6255a0bf6e251de7a1abd9333",
                "sha256:ae17664c380ee2b3ce744f257ac97f4e5ed382326f85df4f1eccb8821eab3076",
                "sha256:71a806eac3cbb1dd3683291fa075457603599f4a940a96285e727ed082089089",
                "sha256:67103c196d23089ea7d62dffa8e81a2d87468dd466db9884576486080586019d",
                "sha256:69735f5434285126a2ec9c4832f7c9aa63c820db538e1874084607eb9df3fd03"
            ]
        },
        "Metadata": {
            "LastTagTime": "2026-10-21T06:39:27.868587291Z"
        },
        "Descriptor": {
            "mediaType": "application/vnd.oci.image.index.v1+json",
            "digest": "sha256:bb8abe27d53de84c95597f2c02c0e702b2779971fb0703e543f9ecf183e999f6",
            "size": 1375
        },
        "Identity": {
            "Pull": [
                {
                    "Repository": "docker.io/penpotapp/frontend"
                }
            ]
        }
    }
]
```

## penpotapp/exporter:2.18

```json
[
    {
        "Id": "sha256:418232d6ca3120b1c2bfde298a56a05a1f41f567cd8494deac3fe7fbc186cfbd",
        "RepoTags": [
            "penpotapp/exporter:2.18"
        ],
        "RepoDigests": [
            "penpotapp/exporter@sha256:418232d6ca3120b1c2bfde298a56a05a1f41f567cd8494deac3fe7fbc186cfbd"
        ],
        "Comment": "buildkit.dockerfile.v0",
        "Created": "2026-10-06T12:36:00.2549752Z",
        "Config": {
            "User": "penpot:penpot",
            "Env": [
                "DEBIAN_FRONTEND=noninteractive",
                "LANG=en_US.UTF-8",
                "LANGUAGE=en_US:en",
                "LC_ALL=en_US.UTF-8",
                "NODE_VERSION=24.20.0-0",
                "NPM_CONFIG_UPDATE_NOTIFIER=false",
                "PATH=/opt/imagick/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "PLAYWRIGHT_BROWSERS_PATH=/opt/penpot/browsers"
            ],
            "Cmd": [
                "node",
                "app.js"
            ],
            "WorkingDir": "/opt/penpot/exporter",
            "Labels": {
                "bundle_version": "2.18.3",
                "com.docker.dhi.chain-id": "sha256:2dd4005b43a3dc5d8ecd318a392561953ced36319380a6bcd751d31caffee816",
                "com.docker.dhi.compliance": "cis",
                "com.docker.dhi.created": "2026-08-28T14:49:41Z",
                "com.docker.dhi.date.end-of-life": "2028-04-30",
                "com.docker.dhi.date.release": "2025-05-06",
                "com.docker.dhi.definition": "image/node/debian-13/24-dev",
                "com.docker.dhi.distro": "debian-13",
                "com.docker.dhi.entitlement": "public",
                "com.docker.dhi.flavor": "",
                "com.docker.dhi.name": "dhi/node",
                "com.docker.dhi.package-manager": "apt",
                "com.docker.dhi.shell": "bash",
                "com.docker.dhi.title": "Node.js 24.x (dev)",
                "com.docker.dhi.url": "https://dhi.io/catalog/node",
                "com.docker.dhi.variant": "dev",
                "com.docker.dhi.version": "24.20.0-0-debian13-dev",
                "maintainer": "Penpot <docker@penpot.app>",
                "org.opencontainers.image.created": "2026-10-06T12:34:05.903Z",
                "org.opencontainers.image.description": "Penpot: The open-source design platform for Product teams that need scalable collaboration.",
                "org.opencontainers.image.licenses": "MPL-2.0",
                "org.opencontainers.image.revision": "ff7a66f51938b2293260ea27a64e2c4e0833b5e3",
                "org.opencontainers.image.source": "https://github.com/penpot/penpot",
                "org.opencontainers.image.title": "penpot",
                "org.opencontainers.image.url": "https://github.com/penpot/penpot",
                "org.opencontainers.image.version": "2.18.3"
            },
            "ArgsEscaped": true
        },
        "Architecture": "amd64",
        "Os": "linux",
        "Size": 2976473345,
        "RootFS": {
            "Type": "layers",
            "Layers": [
                "sha256:f721c29b36d3419040dd50a6e355508db1a071ab90a389adaf1fed2b1e52d2c7",
                "sha256:3a76260c8e2bfb168b4a012bf7ca75a9f6ed979cf362629ae9a88a1168a6b4f6",
                "sha256:93f407ad377248d796fe2fe068865c8f9de5dd924d25032ce7f21f1ceead1170",
                "sha256:5817a4dfc8ccfbb334a55fa390855910b462b5bf501d7c3d6ad48025017d239a",
                "sha256:0a7f6f53be614c92b412a7074bd5a2fc7aa2992bfbdef498be1365dd97c23a61",
                "sha256:43e913da5335bec8d5b87b99639387aa9782974a27f0a8a1705de85dceaa2a4f",
                "sha256:29f0b171dc4cbdb6e45c1cdb149adde32fa54bd32d82baea028a0315349cfa71",
                "sha256:a0d8af289a5ae7bd6030905ba6936934dfdfdf3328d1caed7012c05d73422dea",
                "sha256:a703ca72e1787516abfa128fab1406715ba3a2fb781b196440fc30b79c60fcfc",
                "sha256:750cd00e306f048053b721146a0706bbefcad9defd9c126095e444b9b1fbdf20",
                "sha256:83e00d21fb3b6a8d21fc1c4a2216df7638a5a1bbcb7edfcb954038fe0ac0e6fb",
                "sha256:5f70bf18a086007016e948b04aed3b82103a36bea41755b6cddfaf10ace3c6ef",
                "sha256:c62444a57ddc89c96bf61aa9dd1286615a0c64a0a681f30f45fbe6acceddeb4a",
                "sha256:8fc3bdcd1e3688ba05f5a5854b9380ce81382e410ea9f5bc2c889fa065d6a929"
            ]
        },
        "Metadata": {
            "LastTagTime": "2026-10-21T06:39:34.532985517Z"
        },
        "Descriptor": {
            "mediaType": "application/vnd.oci.image.index.v1+json",
            "digest": "sha256:418232d6ca3120b1c2bfde298a56a05a1f41f567cd8494deac3fe7fbc186cfbd",
            "size": 1375
        },
        "Identity": {
            "Pull": [
                {
                    "Repository": "docker.io/penpotapp/exporter"
                }
            ]
        }
    }
]
```