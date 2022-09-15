FROM node:16

RUN npm i -g @quasar/cli

RUN mkdir -p /home/js/.ssh
RUN ln -s /run/secrets/id_rsa /home/js/.ssh/id_rsa
RUN touch /home/js/.ssh/known_hosts

#RUN groupadd -g 1000 js && useradd -u 1000 js && echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
#RUN chown -R js:js /var/www

RUN ln -s /var/www /home/js/www
WORKDIR /home/js/www

EXPOSE 8080

CMD ["npx", "quasar", "dev"]