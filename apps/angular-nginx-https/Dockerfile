# Stage 1
FROM node:18.12.1-alpine3.16 as build-step

ARG app_path=$APP_PATH
ARG port=$NGINX_PORT

RUN apk update && apk upgrade && \
    apk add --no-cache bash git openssh nano zopfli brotli

RUN mkdir -p /app/${app_path}

WORKDIR /app/${app_path}

COPY . .

# COPY /dist /usr/share/nginx/html

RUN find dist -type f -regex '.*[css|csv|html|js|svg|txt|xml|json]' -exec zopfli '{}' \;

RUN find dist -type f -regex '.*[css|csv|html|js|svg|txt|xml|json]' -exec brotli '{}' \;


#Stage 2
# https://github.com/fholzer/docker-nginx-brotli
FROM fholzer/nginx-brotli:v1.21.6

COPY --from=build-step /app/${app_path} /usr/share/nginx/html

COPY conf/nginx.vh.default.conf /etc/nginx/conf.d/default.conf
# RUN mv -v dist/* /usr/share/nginx/html

EXPOSE ${port}
