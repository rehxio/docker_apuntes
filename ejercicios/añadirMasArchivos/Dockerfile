FROM ubuntu
RUN apt-get update && apt-get install -y nginx
RUN echo '<!DOCTYPE html><html><head><title>Docker Static Example</title><link href="assets/style.css" type="text/css" rel="stylesheet" /></head><body><h1>Welcome to next generation tech</h1></body></html>' >> /var/www/html/index.html
RUN mkdir /var/www/html/assets
RUN echo 'body { background: red }' >> /var/www/html/assets/style.css
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

