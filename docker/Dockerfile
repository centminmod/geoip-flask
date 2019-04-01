# docker run -d --network="web" -p 8888:8888  --name="geoip" -t geoip
FROM ubuntu:18.04

ARG BUILD_DATE
ARG VCS_REF
ARG VERSION
LABEL org.label-schema.build-date=$BUILD_DATE \
      org.label-schema.vcs-ref=$VCS_REF \
      org.label-schema.vcs-url="https://github.com/centminmod/geoip-flask/tree/centminmod" \
      org.label-schema.version=$VERSION \
      org.label-schema.schema-version="1.0"

RUN apt-get update && apt-get install -y gnupg && echo "deb http://ppa.launchpad.net/maxmind/ppa/ubuntu bionic main" >> /etc/apt/source.list \
    && apt-key adv --keyserver keyserver.ubuntu.com --recv-keys F44B38CE3DB1BF64B61DBD28DE1997DCDE742AFA \
    && apt-get update && apt-get install -y git python3-pip curl unzip cron geoipupdate supervisor && apt-get clean && apt-get autoclean && apt-get remove

RUN cd /opt/ \
    && curl -L https://github.com/centminmod/geoip-flask/archive/centminmod.zip -o centminmod.zip \
    && unzip centminmod.zip \
    && mv geoip-flask-centminmod geoip-flask \
    && rm -f centminmod.zip \
    && cd /opt/geoip-flask && pip3 install -r requirements.txt \
    && mkdir -p /opt/geoip-flask/GeoLite2-City/ \ 
    && /usr/bin/geoipupdate -d /opt/geoip-flask/GeoLite2-City/

COPY docker/geoipupdate.cron /etc/cron.d/geoipupdate

COPY docker/supervisord.conf /etc/supervisor/conf.d/supervisord.conf 

EXPOSE 8888 9191

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/conf.d/supervisord.conf"]
