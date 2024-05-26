"# TP2 Devops" 
1) J'ai installé Docker Desktop via le lien fourni en classe 
2) j'ai d'abord cloné mon repo : 
       git clone https://github.com/GhaithBenhadi/Devops.git
       cd Devops
Puis j'ai créer un nouveau dossier TP2 avec son README :
       mkdir TP2
       echo "# TP2 Devops" > TP2/README.md
       git add TP2
       git commit -m "Ajout du dossier TP2 et du fichier README.md"
       git push origin main

3)Exécuter un serveur web dans le container docker :
    a/ docker pull nginx
    b/ docker images
    c/ echo "Hello World" > C:/Users/conta/Desktop/Devops/Devops/TP2/index.html
    d/ docker run -d -p 80:80 -v C:/Users/conta/Desktop/Devops/Devops/TP2/index.html:/usr/share/nginx/html/index.html --name DevopsWebServer nginx
    e/ docker rm -f DevopsWebServer
    f/docker run -d -p 80:80 --name NewWebServer nginx
      docker cp C:/Users/conta/Desktop/Devops/Devops/TP2/index.html NewWebServer:/usr/share/nginx/html/index.html

4) FROM nginx
   COPY index.html /usr/share/nginx/html/index.html
   docker build -t custom-nginx .
   docker run -d -p 80:80 --name custom-webserver custom-nginx

Observations et Comparaison :
Utilisation d'un volume (-v) :

Avantages :
- Permet de modifier les fichiers locaux et de voir les changements instantanément dans le container sans avoir à reconstruire l'image.
- Utile pour le développement, car il facilite les itérations rapides.

Inconvénients :
- Moins sécurisé, car les fichiers locaux peuvent être modifiés accidentellement.

Utilisation de COPY dans le Dockerfile :

Avantages :
- Plus sécurisé, car les fichiers copiés dans l'image sont en lecture seule.
- Les images sont auto-suffisantes et peuvent être déployées de manière cohérente sur différents environnements.

Inconvénients :
- Chaque modification nécessite une reconstruction de l'image.
- Peut être plus lent pendant le développement en raison du besoin de reconstruire l'image pour chaque changement.

5) a/ docker pull mysql
      docker pull phpmyadmin/phpmyadmin

   b/ Je crée le réseau Docker pour permettre la communication entre les containers : 
          docker network create NetworkDevopsTp
      Je démarre et je connecte le container MySql au réseau :
          docker run -d --name mysql-db --network NetworkDevopsTp -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=testdb mysql
      Je démarre et je connecte le container PhpMyadmin au réseau :
          docker run -d --name phpmyadmin --network NetworkDevopsTp -e PMA_HOST=mysql-db -p 8080:80 phpmyadmin/phpmyadmin

6) a/ docker run : Utilisé pour démarrer un seul container avec une configuration spécifique. On doit répéter cette commande pour chaque container et spécifier les paramètres à chaque fois.
docker-compose up : Utilisé pour démarrer tous les services définis dans un fichier docker-compose.yml en une seule commande. Cette approche est plus pratique pour les applications multi-container car elle centralise la configuration.

b/ Pour lacer tous les containers : docker-compose up
   Pour stopper tous les containers : docker-compose down

c/ je démarre tous les services : docker-compose up -d






 


   


