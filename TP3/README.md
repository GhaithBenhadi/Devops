1/ Je voulais utiliser ton URL mais les droits sont limités car j'ai perdu tous mes anciens repo suite à une mauvaise manipulation 
Pour le faire et cloner le repo GIT :
git clone https://github.com/quentin-desbin/ynov-api-23-24.git
 

2/ FROM node:18-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 3000

3/ 
docker pull mysql
docker run -d --name mysql-db -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=testdb -p 3306:3306 mysql

4/ docker-compose build
docker-compose up -d

LES QUESTIONS : 
Q1 : Que se passe-t-il si un des ports publiés est déjà utilisé ?
Si un port est déjà utilisé, Docker ne pourra pas démarrer le container et renverra une erreur indiquant que le port est déjà en usage. Vous devrez utiliser un port différent ou libérer le port utilisé.

Q2 : Quelle option de la commande npm install permet de n'installer que les dépendances de production ?
L'option --production permet de n'installer que les dépendances de production :
npm install --production

Q3 : Comment peut-on analyser la sécurité d'une application comme celle-ci (dépendances et image Docker) ?
On peut utiliser des outils comme npm audit pour analyser les dépendances de l'application et docker scan pour analyser la sécurité de l'image Docker.

Q4 : Pourquoi à l'étape 6 mon container Node n'arrive pas à communiquer avec ma base de données si je laisse "localhost" en hostname ?
Parce que "localhost" dans le contexte du container Node.js fait référence à lui-même et non au container MySQL. je dois utiliser le nom du service défini dans docker-compose.yml (dans ce cas, db) comme hostname pour que les containers puissent communiquer entre eux.






