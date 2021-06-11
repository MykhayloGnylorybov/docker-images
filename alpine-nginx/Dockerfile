FROM public.ecr.aws/x0n9a3d4/alpine-basic:latest
RUN apk add --no-cache curl ca-certificates 'openssl=1.1.1k-r0'
RUN printf "%s%s%s\n" "http://nginx.org/packages/alpine/v" `egrep -o '^[0-9]+\.[0-9]+' /etc/alpine-release` "/main" | tee -a /etc/apk/repositories
RUN curl -o /tmp/nginx_signing.rsa.pub https://nginx.org/keys/nginx_signing.rsa.pub
RUN mv /tmp/nginx_signing.rsa.pub /etc/apk/keys/
RUN apk add --no-cache 'nginx=1.20.1-r1'
RUN apk add --no-cache certbot
RUN apk add --no-cache certbot-nginx
#COPY nginx.conf /etc/nginx/nginx.conf
ENTRYPOINT ["nginx", "-g", "daemon off;"]