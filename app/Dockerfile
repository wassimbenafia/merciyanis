FROM nginx:1.19-alpine

RUN apk update
RUN apk add git npm nodejs yarn
#RUN apk add --no-cache python2
#RUN apk add --update alpine-sdk



WORKDIR /var/www

#COPY ./app/ /var/www
#COPY ./plugins/ /var/www/src/plugins
#RUN npm rebuild node-sass
COPY ./server.conf /etc/nginx/conf.d/default.conf

