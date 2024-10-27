FROM node:20-alpine3.19 AS node-deps
WORKDIR /app
COPY package.json yarn.lock ./
RUN yarn

FROM node-deps AS node-build
COPY --from=node-deps /app /app
COPY webpack.config.js postcss.config.js .
COPY src src
RUN yarn build

FROM nginx:1.27-alpine AS webui
COPY --from=node-build /app/public /usr/share/nginx/html
COPY favicon.ico /usr/share/nginx/html
