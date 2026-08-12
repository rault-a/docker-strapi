# Strapi is intentionally NOT installed globally here: a globally
# yarn-installed @strapi/strapi can't resolve admin-panel peer deps (react,
# react-dom, ...) since those only ever get installed into a project's local
# node_modules, causing a permanent "Cannot find module 'react'" crash loop.
# See naskio/docker-strapi#23. The entrypoint instead uses
# `npx create-strapi@$STRAPI_VERSION` to scaffold Strapi as a local project
# dependency, and runs it via `yarn strapi`.

# BASE
ARG NODE_VERSION=24
FROM node:${NODE_VERSION}-slim AS base-debian
EXPOSE 1337

FROM base-debian

ARG STRAPI_VERSION=latest
ENV STRAPI_VERSION=${STRAPI_VERSION}


RUN mkdir -p /srv/app && chown 1000:1000 -R /srv/app

WORKDIR /srv/app

VOLUME /srv/app

COPY docker-entrypoint.sh /usr/local/bin/

RUN chmod 777 /usr/local/bin/docker-entrypoint.sh && ln -s /usr/local/bin/docker-entrypoint.sh

ENTRYPOINT ["docker-entrypoint.sh"]

CMD ["strapi"]
