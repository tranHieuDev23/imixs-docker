FROM postgres:14.2-bullseye

LABEL authors="Tran Minh Hieu <tranhieu23.code@outlook.com>"

# install packages;
RUN apt-get update \
    && apt-get install --no-install-recommends -y \
    cron ssh netcat mariadb-client \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/man/?? /usr/share/man/??_*

# disable default crontab
COPY crontab /etc/crontab
# add the backup scripts into root/home
ADD backup.sh /root/backup.sh
RUN chmod +x /root/backup.sh
ADD backup_init.sh /root/backup_init.sh
RUN chmod +x /root/backup_init.sh
ADD restore.sh /root/restore.sh
RUN chmod +x /root/restore.sh
ADD backup_get.sh /root/backup_get.sh
RUN chmod +x /root/backup_get.sh

RUN mkdir /root/backups
VOLUME /root/backups

CMD ["/root/backup_init.sh"]
