# Docker Tech Stack

Voici le résumé de mon travail pour le TP sur le déploiement d\'une
stack applicative. L\'objectif était de monter une application web
(catalogue de produits) avec sa base de données MariaDB, en utilisant
Terraform pour créer l\'infrastructure sur Docker.

J\'ai joint plusieurs captures d\'écran de mon interface Portainer pour
montrer que tout est bien en place et fonctionnel.

## 1. Vue générale de l\'environnement

Pour commencer, la capture du tableau de bord Portainer donne une bonne
vue d\'ensemble :

![](./images/media/image.jpg){width="6.5in"
height="2.9895833333333335in"}

On y voit directement les 3 conteneurs qui tournent, ce qui correspond
bien à ce qui était attendu : le service web (app), la base de données
(db) et Portainer lui-même. On remarque aussi les 4 volumes créés, ce
qui indique que la persistance des données a bien été prise en compte.

## 2. Les conteneurs en détail

Si on zoome sur la partie conteneurs, on retrouve bien nos trois
services.![](./images/media/image2.jpg){width="6.5in"
height="1.3020833333333333in"}

- Le conteneur app est bien en statut running et utilise l\'image
  dirtsimple/php-server. On voit bien le mapping de port 8080:80, qui
  permet d\'accéder à l\'interface web.

- Le conteneur db pour la base de données tourne aussi. Point important,
  il n\'expose aucun port sur l\'extérieur, ce qui est normal. La
  communication se fait via le réseau interne Docker.

- Le conteneur portainer est celui de l\'interface de gestion.

Tout ce qui a été déployé avec Terraform est donc bien en cours
d\'exécution.

## 3. La persistance des données avec les volumes

Un point clé du TP était de s\'assurer que les données de la base ne
soient pas perdues. Ce qui est montré dans le screen
ci-dessous.![](./images/media/image3.jpg){width="6.5in"
height="1.4895833333333333in"}

On voit très clairement le volume nommé db_vol. C\'est lui qui est lié
au conteneur db et qui stocke les données de MariaDB de manière
persistante.

## 4. Images Docker utilisées

Cette capture liste simplement les images qui ont servi de base pour
lancer les conteneurs.

![](./images/media/image4.jpg){width="6.5in" height="1.78125in"}

On retrouve logiquement les images de mariadb, php-server et portainer
qui correspondent aux services qui tournent.

## 5. Preuve finale : l\'application fonctionne !

Pour finir, la capture la plus importante : celle de l\'application web
elle-même.

![](./images/media/image5.jpg){width="6.5in" height="2.0625in"}

Le fait que la page \"Catalogue de Produits\" s\'affiche prouve que le
serveur web répond bien sur le port 8080. Mais surtout, l\'affichage du
produit \"Démonstration\" avec son prix montre que la connexion entre le
conteneur app et le conteneur db fonctionne parfaitement. L\'application
a bien pu lire les informations dans la base de données et les afficher.

En conclusion, l\'ensemble de ces images montre que l\'infrastructure a
été déployée correctement, que chaque composant est fonctionnel et que
l\'application finale marche comme prévu.
