# Stage 1
FROM node:18.12.1-alpine3.16

ARG app_path=$APP_PATH
ARG port=$PORT
ARG entrypoint=$ENTRYPOINT

RUN apk update && apk upgrade && \
    apk add --no-cache bash git openssh nano zopfli

RUN mkdir -p /app/${app_path}

WORKDIR /app/${app_path}

COPY . .

EXPOSE ${port}

CMD ["node", "${entrypoint}"]