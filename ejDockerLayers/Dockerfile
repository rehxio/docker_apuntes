FROM node:9
COPY ./proyectoOriginal/node-js-server/*.json ./
RUN npm install package-lock.json
COPY ./proyectoOriginal/node-js-server/* ./
EXPOSE 80
CMD [ "npm", "start" ]