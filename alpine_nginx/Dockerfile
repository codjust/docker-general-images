FROM alpine_base

RUN apk add --no-cache \
    zlib-dev libpcrecpp libpcre16 libpcre32 libgcc libstdc++ libssl1.0 \
     openssl pcre sed python2 git  netcat-openbsd wget

ENV NGINX_VERSION 1.12.1
ENV NGINX_PREFIX /opt/nginx   
ENV VAR_PREFIX /var/nginx 

RUN echo "==> Install dependencies..." \
    && apk add --no-cache --virtual build-deps \
        make gcc musl-dev \
        pcre-dev openssl-dev ncurses-dev readline-dev \
        perl \
    && mkdir -p /root/ngx_dir \
    && cd /root/ngx_dir \
    && echo "==> Download OpenResty..." \
    && curl -sSL http://nginx.org/download/nginx-${NGINX_VERSION}.tar.gz | tar -xvz \
    && cd nginx-* \
    && echo "==> Configuring OpenResty..." \
    && ./configure \
            --prefix=$NGINX_PREFIX \
            --http-client-body-temp-path=$VAR_PREFIX/client_body_temp \
            --http-proxy-temp-path=$VAR_PREFIX/proxy_temp \
            --pid-path=$VAR_PREFIX/nginx.pid \
            --lock-path=$VAR_PREFIX/nginx.lock \
    && echo "==> Building OpenResty..." \
    && make \
    && make install \
    && echo "==>Finishing..." \
    && ln -sf $NGINX_PREFIX/sbin/nginx /usr/local/bin/nginx \
    && apk del build-deps \
    && rm -rf /root/ngx_dir


RUN mkdir -p /data/nginx \
    && cp -r $NGINX_PREFIX /data/

#default boot way
CMD ["nginx -c /data/nginx/conf/nginx.conf -p /data/nginx"]
