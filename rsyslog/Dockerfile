FROM library/alpine:latest

RUN set -x \
	  && apk add --update rsyslog bash tar gzip \
	  && mkdir /etc/rsyslog.d/ \
    && mkdir /var/spool/rsyslog \
		&& adduser -S syslog \
		;

ADD rsyslog.conf /etc/rsyslog.conf

ADD rotate.sh /etc/periodic/daily/rotate
RUN chmod 0755 /etc/periodic/daily/rotate

# rsyslog configuration file for docker
ADD rsyslog_docker.conf /etc/rsyslog.d/

VOLUME /var/log/docker/

EXPOSE 514

CMD crond && rm -f /var/run/rsyslogd.pid && rsyslogd -n
