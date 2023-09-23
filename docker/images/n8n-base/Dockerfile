ARG NODE_VERSION=18
FROM node:${NODE_VERSION}-alpine

WORKDIR /home/node
COPY .npmrc /usr/local/etc/npmrc

RUN \
	apk add --update git openssh graphicsmagick tini tzdata ca-certificates libc6-compat && \
	npm install -g npm@9.5.1 full-icu && \
	rm -rf /var/cache/apk/* /root/.npm /tmp/* && \
	# Install fonts
	apk --no-cache add --virtual fonts msttcorefonts-installer fontconfig && \
	update-ms-fonts && \
	fc-cache -f && \
	apk del fonts && \
	find  /usr/share/fonts/truetype/msttcorefonts/ -type l -exec unlink {} \; && \
	rm -rf /var/cache/apk/* /tmp/*

ARG POSTGRES_DB=postgres1
ARG POSTGRES_USER=user1
ARG POSTGRES_PASSWORD=pass11

ENV NODE_ICU_DATA /usr/local/lib/node_modules/full-icu
ENV DB_TYPE=postgresdb
ENV DB_POSTGRESDB_HOST=postgres
ENV DB_POSTGRESDB_PORT=5432
ENV DB_POSTGRESDB_DATABASE=${POSTGRES_DB}
ENV DB_POSTGRESDB_USER=${POSTGRES_USER}
ENV DB_POSTGRESDB_PASSWORD=${POSTGRES_PASSWORD}
ENV DB_POSTGRESDB_SCHEMA=public
ENV NODE_ENV=enterprise
ENV N8N_TEMPLATES_ENABLED=false
ENV WEBHOOK_URL=https://red8.agah.com/
ENV N8N_METRICS=true
ENV GENERIC_TIMEZONE=Asia/Tehran
ENV N8N_DIAGNOSTICS_ENABLED=false
ENV N8N_HIDE_USAGE_PAGE=false
ENV N8N_LICENSE_AUTO_RENEW_ENABLED=true
EXPOSE 5678/tcp
