# Parkinson Detection

Ce projet est une architecture distribué autour d'une librairie de machine learning réalisée pour un ancien projet. 
Cette librairie permet la detection de la maladie de parkinson avec une precision de ~60% (manque de donnée). [En savoir plus](https://medium.com/better-programming/diagnosing-parkinsons-disease-by-voice-using-linear-regression-in-python-73aad2712fba)
Le but de ce projet a donc été de construire une architecture distribué, conteneurisé autour de cette librairie et également de stocker les mesures effectuées sur l'audio par la librairie de machine learning et de les stocker dans un cluster MySQL afin de les réutiliser plus tard pour augmenter la base de connaissance du model de machine lerning --> Amélioration de la précision.

A l'heure actuelle, seulement de l'écriture est réalisée dans le cluster MySQL, par la suite les modules pourraient être modifiées pour re-entrainer automatiquement le model depuis les données de la base. (Nous ne l'avons pas fait car assez couteux en temps et ce n'était pas le but premier du projet.

### Schéma d'architecture

[![Untitled-Diagram-1.png](https://i.postimg.cc/XNDNpcz6/Untitled-Diagram-1.png)](https://postimg.cc/dDrcfdF5)

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

Se rendre dans le dossier du projet
```bash
cd ./parkinsonDockerized
```
Lancer le docker-compose
```bash
sudo docker-compose up
```
le docker-compose va récuperer les images docker sur docker hub.
Les images ont étés préalablement créées et postées sur docker hub pour le projet (voir Ressources)

Attendre que le docker-compose finisse le démarrage du projet.

L'interface est accessible depuis l'adresse http://localhost:3000/

## Validation

Acceder à l'ihm : http://localhost:3000/

Uploader un des fichier de test fournit dans le repo git (/parkinsonDockerized/test-files)

Attendre la réponse.

Vérifier que la base à bien été remplie avec les mesures du fichier fournit
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

Les Dockerfiles se trouvent dans les dépots github.

