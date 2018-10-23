FROM ubuntu
RUN apt-get update && apt-get install -y nginx
RUN echo 'hola mundo' >> /var/www/html/index.html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]