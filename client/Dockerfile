#
# Angular App served with NGinX webserver on docker
#
# https://www.indellient.com/blog/how-to-dockerize-an-angular-application-with-nginx/
# https://dev.to/oneofthedevs/docker-angular-nginx-37e4

# Stage 1 : BUILD
FROM node:lts-slim AS build
# FROM node:latest as build

RUN npm cache clean --force

WORKDIR /myapp
COPY . .

RUN npm install
RUN npm run build

# Stage 2 : RUNTIME
FROM nginx:latest AS runtime

COPY --from=build /myapp/dist/client /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80
