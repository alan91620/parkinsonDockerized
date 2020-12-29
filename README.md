# Parkinson Detection

Foobar is a Python library for dealing with word pluralization.

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

## Utilisation

Acceder à l'ihm : http://localhost:3000/

Uploader un des fichier de test fournit dans le repo git (/parkinsonDockerized/test-files)

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
[MIT](https://choosealicense.com/licenses/mit/)
