FROM alpine:edge

MAINTAINER Maciej Lisiewski <maciej.lisiewski@gmail.com>

RUN apk add --no-cache tini

RUN apk add --no-cache --virtual .build-deps \
    ca-certificates \
    wget \
    musl-dev \
    gcc \
    make \
    && export BUILD_DIR="$(mktemp -d)" \
    && (cd $BUILD_DIR && exec wget -q https://raw.githubusercontent.com/ncopa/su-exec/f85e5bde1afef399021fbc2a99c837cf851ceafa/su-exec.c \ 
        https://raw.githubusercontent.com/ncopa/su-exec/f85e5bde1afef399021fbc2a99c837cf851ceafa/Makefile) \ 
    && (cd $BUILD_DIR && exec make) \
    && mv $BUILD_DIR/su-exec /bin/ \
    && chmod a+x /bin/su-exec \
    && rm -rf $BUILD_DIR \
    && apk del .build-deps

ENTRYPOINT ["/sbin/tini", "--"]
