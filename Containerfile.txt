# Stage 1
FROM  registry.access.redhat.com/ubi8/nodejs-16 AS builder

USER  root

WORKDIR /app

COPY  .   .

RUN  npm install

# Stage 2
FROM  registry.access.redhat.com/ubi8/nodejs-16
#FROM docker.io/nodejscn/node:latest

WORKDIR /app

COPY --from=builder  /app  .
USER 1001
CMD ["node", "./apps.js"]
