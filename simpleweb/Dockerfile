FROM node:alpine

WORKDIR /usr/app

# Update package.json first
COPY ./package.json ./
RUN npm install
COPY ./ ./

CMD ["npm", "start"]