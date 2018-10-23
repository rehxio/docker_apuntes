FROM ubuntu
RUN apt-get update && apt-get install -y nginx
COPY ./contenido /var/www/html/
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

