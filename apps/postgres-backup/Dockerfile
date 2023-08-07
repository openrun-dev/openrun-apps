# Dockerfile for database backup
FROM alpine:3.18.2

# install postgresql client. for pg_dump and pg_dumpall commands
RUN apk add --no-cache postgresql15-client 
RUN apk add --no-cache curl
RUN apk add --no-cache nodejs-current npm
RUN apk add --no-cache tzdata

RUN  mkdir /backup_script
RUN  mkdir /backup_script/node_uploader
ADD app_src/backup.sh /backup_script/backup.sh
ADD app_src/cron_job /backup_script/cron_job
COPY app_src/node-uploader /backup_script/node_uploader/


# set timezone
ENV TZ=Europe/Rome

RUN mkdir /backup_data
WORKDIR /backup_script
RUN chmod +x ./backup.sh
RUN chmod a+x ./cron_job
WORKDIR /backup_script/node_uploader 
RUN npm install
RUN npx tsc
CMD [ "sh", "/backup_script/backup.sh"]
