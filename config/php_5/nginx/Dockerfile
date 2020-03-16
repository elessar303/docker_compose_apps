FROM nginx:alpine

RUN apk add tzdata

ENV TZ=America/Argentina/Buenos_Aires

RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

CMD ["nginx"]

EXPOSE 80 443