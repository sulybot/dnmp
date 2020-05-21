# use latest alpine nginx image as default
ARG NGINX_VERSION=mainline

FROM nginx:${NGINX_VERSION}-alpine

ARG ALPINE_PACKAGE_REPO_MIRROR

ARG TZ

RUN if [ "${ALPINE_PACKAGE_REPO_MIRROR}" != "" ]; then \
        sed -i "s/dl-cdn.alpinelinux.org/${ALPINE_PACKAGE_REPO_MIRROR}/g" /etc/apk/repositories; \
    fi

RUN if [ "${TZ}" != "" ]; then \
        apk --no-cache add tzdata; \
        cp "/usr/share/zoneinfo/$TZ" /etc/localtime; \
        echo "$TZ" > /etc/timezone; \
    fi

WORKDIR /usr/share/nginx
