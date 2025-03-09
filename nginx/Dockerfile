FROM alpine:3.21.3

RUN apk update && apk upgrade && apk add nginx

EXPOSE 80

VOLUME ["/etc/nginx/http.d"]

USER nginx

CMD ["nginx", "-g", "daemon off;"]
