FROM node:12

RUN npm install -g @vue/cli @vue/cli-service-global


RUN mkdir -p /home/js/.ssh
RUN ln -s /run/secrets/id_rsa /home/js/.ssh/id_rsa
RUN touch /home/js/.ssh/known_hosts

#RUN groupadd -g 1000 js && useradd -u 1000 js && echo '%sudo ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers
#RUN chown -R js:js /var/www

RUN ln -s /var/www /home/js/www
WORKDIR /home/js/www

#RUN chown -R js:js /home/js /var/www

EXPOSE 8080

CMD ["npm", "run", "startServe"]
