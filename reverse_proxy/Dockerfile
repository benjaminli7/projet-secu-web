FROM nginx:alpine

COPY ./default.conf /etc/nginx/conf.d/default.conf
COPY ./certs /etc/certs
COPY ./script.sh /script.sh

RUN apk add fail2ban

RUN apk add openssl

ENTRYPOINT ["bin/sh", "/script.sh"]