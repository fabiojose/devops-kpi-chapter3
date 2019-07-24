FROM node:8-alpine

ENV WORKDIR=/var/app

WORKDIR $WORKDIR

RUN mkdir -p $WORKDIR

COPY . $WORKDIR

RUN npm install

EXPOSE 3000

CMD ["npm", "start"]
