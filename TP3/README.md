1/ Je voulais utiliser ton URL mais les droits sont limités car j'ai perdu tous mes anciens repo suite à une mauvaise manipulation 
Pour le faire et cloner le repo GIT :
git clone https://github.com/quentin-desbin/ynov-api-23-24.git
 

2/ FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 3000




