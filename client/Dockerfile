FROM node:16-alpine as builder

# EACCES: permission denied で追加
USER node
RUN mkdir -p /home/node/app

# WORKDIR '/app'
WORKDIR /home/node/app
# COPY ./package.json ./
COPY --chown=node:node ./package.json ./

RUN npm install
# COPY . .
COPY --chown=node:node ./ ./
RUN npm run build
RUN ls -la

FROM nginx
EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /app/build /usr/share/nginx/html
