FROM nginx
ARG ZONE_INFO
ARG LANG
ARG LANG2=${LANG}

RUN DEBIAN_FRONTEND="noninteractive" apt-get update && apt-get install -y --no-install-recommends locales \
vim curl wget build-essential software-properties-common \ 
zlib1g-dev libxml2-dev openssl unzip zip \
&& rm -rf /var/lib/apt/lists/*

ENV LC_ALL=${LANG2}.UTF-8
ENV LANGUAGE=${LANG2}.UTF-8
ENV LANG=${LANG2}.UTF-8

RUN locale-gen ${LANG2}.UTF-8

COPY cacert.pem /etc/ssl/cacert.pem
COPY privkey.pem /etc/ssl/privkey.pem
COPY nginx.conf /etc/nginx/nginx.conf
ADD sites-enabled /etc/nginx/sites-enabled
RUN ln -snf /usr/share/zoneinfo/${ZONE_INFO} /etc/localtime
WORKDIR /var/www/app

CMD service nginx start

EXPOSE 80
EXPOSE 443
