FROM node:18.12.1-alpine3.16

ARG app_path=$APP_PATH
ARG port=$PORT

RUN apk update && apk upgrade && \
    apk add --no-cache bash git openssh nano zopfli brotli

RUN mkdir -p /app/${app_path}

WORKDIR /app/${app_path}

COPY . .

RUN find dist -type f -regex '.*[css|csv|html|js|svg|txt|xml|json]' -exec zopfli '{}' \;

RUN find dist -type f -regex '.*[css|csv|html|js|svg|txt|xml|json]' -exec brotli '{}' \;

EXPOSE ${port}
