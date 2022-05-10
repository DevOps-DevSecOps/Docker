FROM node:alpine

# add openssh and clean
RUN apk add --update openssh \
&& rm  -rf /tmp/* /var/cache/apk/*

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

ARG NODE_ENV
ENV NODE_ENV $NODE_ENV
COPY package.json /usr/src/app/

RUN apk add --no-cache --virtual .gyp \
    python \
    make \
    g++

RUN npm install && npm cache clean --force
COPY . /usr/src/app

#make sure we get fresh keys
RUN rm -rf /etc/ssh/ssh_host_rsa_key /etc/ssh/ssh_host_dsa_key

EXPOSE 22
EXPOSE 20000-30000
ENTRYPOINT ["sh", "entrypoint.sh"]
CMD ["npm", "start"]