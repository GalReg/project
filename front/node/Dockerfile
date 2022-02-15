# build stage
FROM node:16 as build-stage
WORKDIR /app

COPY ./front-development/package.json ./front-development/yarn.lock ./
RUN yarn --pure-lockfile --cache-folder .yarn

COPY ./front-development .
RUN yarn build:prod

# production stage
FROM nginx:alpine as production-stage
COPY nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=build-stage /app/dist/ /var/www/app
CMD ["nginx", "-g", "daemon off;"]
