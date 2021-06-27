FROM public.ecr.aws/x0n9a3d4/alpine-basic:latest

RUN apk add --no-cache curl ca-certificates 'openssl=1.1.1k-r0'

RUN printf "%s%s%s\n" "http://nginx.org/packages/alpine/v" `egrep -o '^[0-9]+\.[0-9]+' /etc/alpine-release` "/main" | tee -a /etc/apk/repositories \
    && curl -o /tmp/nginx_signing.rsa.pub https://nginx.org/keys/nginx_signing.rsa.pub \
    && mv /tmp/nginx_signing.rsa.pub /etc/apk/keys/ \
    && apk add --no-cache 'nginx=1.20.1-r1' certbot certbot-nginx

RUN apk add --no-cache \
        python3 \
        py3-pip \
    && pip3 install --upgrade pip \
    && pip3 install awscli \
    && rm -rf /var/cache/apk/*

#COPY nginx.conf /etc/nginx/nginx.conf
ENTRYPOINT ["nginx", "-g", "daemon off;"]