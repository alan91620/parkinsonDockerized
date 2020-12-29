# Parkinson Detection

Par [Alan MARTHINEAU](mailto:alan.marthineau@edu.ece.fr), [Augustin LOLLIVIER](mailto:augustin.lollivier@edu.ece.fr), [Karim BENSAID](mailto:karim.bensaid@edu.ece.fr)

Ce projet est une architecture distribuée et conteneurisée, contruite autour d'une librairie de machine learning réalisée pour un ancien projet. 
Cette librairie permet la detection de la maladie de parkinson par la voix via un fichier audio .wav avec une precision de ~60% (manque de données). 
[En savoir plus](https://medium.com/better-programming/diagnosing-parkinsons-disease-by-voice-using-linear-regression-in-python-73aad2712fba)

Le but de ce projet a donc été de construire une architecture distribuée, conteneurisée autour de cette librairie permettant la detection de la maladie mais également de stocker les mesures effectuées sur le fichier audio par la librairie de machine learning, dans un cluster MySQL afin de les réutiliser plus tard pour augmenter la base de connaissance du model de machine learning --> Amélioration de la précision.

A l'heure actuelle, seulement de l'écriture est réalisée dans le cluster MySQL, par la suite les modules pourraient être modifiés pour re-entrainer automatiquement le model depuis les données de la base. (Nous ne l'avons pas fait car assez couteux en temps et ce n'était pas le but premier du projet.

### Schéma d'architecture

[![archhi-aprk.png](https://i.postimg.cc/jqyJpjq7/archhi-aprk.png)](https://postimg.cc/QVxt5hT8)

Pour réaliser ce projet nous avons d'abord transformé notre librairie de machine learning en serveur REST python (Flask) afin de pouvoir faire des appels cross-langage depuis le back.
Nous avons ensuite developpé un backoffice (Spring boot) faisant des appels sur le serveur REST python, embarquant également un connecteur jdbc mysql pour faire des appels sur le futur cluster et une route http pour recevoir le fichier audio.

Enfin nous avons developpé un frontoffice simple avec Reactjs permettant l'upload de fichier .wav et l'affichage du résultat.

Une fois ces applications developpées nous les avons dockerisés et avons push les images sur notre [Docker Hub](https://hub.docker.com/repository/docker/tigroucharly/parkinson).
Puis pour finir nous avons réalisé un docker-compose réalisant les actions suivantes :
- Mise en place front
- Mise en place loadbalancer
  - chargement nginx.conf
- Mise en place 2 back
- Mise en place API python
- Mise en place Cluster MySQL
  - initialisation du schéma de base
  - initialisation des comptes root:password & admin:password
- Mise en place d'un réseau pour le cluster.

L'installation a été rendue le plus simple possible avec le docker-compose, il n'y a rien à initialiser, seulement à clone ce dépôt github et lancer le docker-compose -> voir ci-après.

## Prérequis

- Machine Linux ayant accès a internet (Testé sur Ubuntu 20.10)
- Privilèges admin
- [Git](https://git-scm.com/book/fr/v2/Démarrage-rapide-Installation-de-Git)
- [Docker](https://docs.docker.com/get-docker/)
- [docker-compose](https://docs.docker.com/compose/install/)

## Installation

Créer un dossier pour le projet et s'y placer

```bash
mkdir parkinson-detection
cd ./parkinson-detection
```
Cloner le repo du projet docker-compose

```bash
git clone https://github.com/alan91620/parkinsonDockerized.git
```

## Utilisation

Se placer dans le dossier du projet
```bash
cd ./parkinsonDockerized
```
Lancer le docker-compose
```bash
sudo docker-compose up
```
le docker-compose va récuperer les images docker sur docker hub.

Les images ont étés préalablement créées et postées sur docker hub pour le projet (voir [Ressources](https://github.com/alan91620/parkinsonDockerized/blob/master/README.md#ressources))

Attendre que le docker-compose finisse l'initialisation du projet.

Une fois les services lancés, l'interface est accessible depuis l'adresse http://localhost:3000/

## Validation

Acceder à l'ihm : http://localhost:3000/

Uploader un des fichier de test fourni (/parkinsonDockerized/test-files).

Attendre la réponse.

Vérifier que la base à bien été remplie avec les mesures du fichier fourni.
```bash
sudo docker container ls
```
Chercher le container mysql du cluster et relever son nom (parkinsondockerized_mysql1_1)

Ouvrir une console mysql sur le container
```bash
sudo docker exec -it parkinsondockerized_mysql1_1 mysql -u root -p
password : password
```
Enfin afficher les valeurs de la table de données
```sql
use parkinson;
select * from measures;
```
Les données sont présentes.

## Ressources

[Github project MachineLearning API](https://github.com/alan91620/parkison-api)

[Github project Frontoffice](https://github.com/alan91620/frontparkinson)

[Github project Backoffice](https://github.com/alan91620/backparkinson)

[Repo images perso docker](https://hub.docker.com/repository/docker/tigroucharly/parkinson)

Les Dockerfiles se trouvent dans le dépot Github propre à chaque module.

