FROM zabbix/zabbix-server-mysql:ubuntu-5.4-latest

USER root

RUN apt-get update -y
RUN apt-get install -y sudo curl make build-essential
RUN curl -fsSL https://deb.nodesource.com/setup_12.x | sudo -E bash -
RUN sudo apt-get install -y nodejs
RUN apt-get install -y netcat

USER zabbix

RUN npm i -S statsd statsd-zabbix-backend
RUN mkdir /var/lib/zabbix/shared