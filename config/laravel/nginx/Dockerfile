FROM nginx:alpine

RUN apk update && \
	apk add nano

ADD ./config/laravel/nginx/vhost.conf /etc/nginx/conf.d/default.conf
WORKDIR /var/www