FROM node:6.11.3-alpine AS build-stage

WORKDIR /app
COPY ./vue ./
RUN npm install
RUN npm run build


FROM nginx:1.13.1-alpine AS production-stage

ENV LANG C.UTF-8
ENV TZ Asia/Tokyo

COPY nginx/work/ /home/work
RUN mkdir -p /var/log/nginx/log\
    && mkdir /home/www\
    && mkdir /home/www/contents
COPY --from=build-stage /app/dist /home/www/contents
WORKDIR /home/work
RUN rm -f /etc/nginx/conf.d/*.conf\
    && rm -f /etc/nginx/nginx.conf\
    && cp -i *.conf /etc/nginx
EXPOSE 80 443

CMD ["nginx", "-g", "daemon off;","-c","/etc/nginx/nginx.conf"]