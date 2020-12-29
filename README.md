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


Use the package manager [pip](https://pip.pypa.io/en/stable/) to install foobar.

```bash
pip install foobar
```

## Usage

```python
import foobar

foobar.pluralize('word') # returns 'words'
foobar.pluralize('goose') # returns 'geese'
foobar.singularize('phenomena') # returns 'phenomenon'
```

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
[MIT](https://choosealicense.com/licenses/mit/)
