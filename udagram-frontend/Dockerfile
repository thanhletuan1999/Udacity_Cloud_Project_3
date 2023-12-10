# FROM node:16-alpine as build
# RUN mkdir -p /usr/src/app
# WORKDIR /usr/src/app
# COPY package.json package-lock.json /usr/src/app/
# RUN npm install -g ionic
# RUN npm install -f
# COPY . .
# RUN ionic build
# FROM nginx:alpine
# COPY --from=build  /usr/src/app/www /usr/share/nginx/html/
### Build
FROM beevelop/ionic:latest AS ionic
## Create app directory
WORKDIR /usr/src/app
## Install app dependencies
## A wildcard is used to ensure both package.json AND package-lock.json are copied
COPY package*.json ./
RUN npm ci
## Bundle app source
COPY . .
RUN ionic build
### Run 
FROM nginx:alpine
#COPY www /usr/share/nginx/html
COPY --from=ionic  /usr/src/app/www /usr/share/nginx/html