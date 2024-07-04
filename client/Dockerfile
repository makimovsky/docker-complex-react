FROM node:16-alpine as builder
USER node

RUN mkdir -p /home/node/app
WORKDIR /home/node/app

COPY --chown=node:node ./client/package.json ./
RUN npm install
COPY --chown=node:node ./client/ ./
RUN npm run build

FROM nginx
EXPOSE 3000
COPY ./client/nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /home/node/app/build /usr/share/nginx/html