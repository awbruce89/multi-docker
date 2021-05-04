FROM node:alpine as builder
RUN mkdir -p /home/node/app

RUN chown -R node:node /home/node/app
WORKDIR '/home/node/app' 
COPY --chown=node:node ./package.json ./
RUN npm install
COPY --chown=node:node . .
RUN npm run build

FROM nginx
EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /home/node/app/build /usr/share/nginx/html