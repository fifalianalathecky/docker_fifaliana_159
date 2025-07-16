# DOCKER 

## Qu'est-ce que Docker ?

Docker est une plateforme de virtualisation légère qui permet de développer, expédier et exécuter des applications dans des conteneurs. Un conteneur Docker est une unité standard de logiciel qui regroupe le code et toutes ses dépendances, ce qui permet à l'application de fonctionner rapidement et de manière fiable dans différents environnements informatiques.

## Concepts de base

- *Images Docker* : Une image est un modèle en lecture seule à partir duquel les conteneurs sont créés. Elle contient tout ce qu'il faut pour exécuter une application : le code, les bibliothèques, les dépendances et les fichiers de configuration.

### 📦 Image Docker

Une **image Docker** est un **modèle figé et immuable** utilisé pour créer des conteneurs.  
Elle contient tout ce qu’il faut pour exécuter une application :

- un **système de fichiers** (ex : basé sur Ubuntu, Alpine, etc.)
- le **code de l’application**
- les **dépendances** (librairies, runtimes...)
- une **commande par défaut** pour démarrer l’application

---

#### 🧱 Différence entre image et conteneur

| Élément     | Description                                               |
|-------------|-----------------------------------------------------------|
| **Image**   | Modèle figé, empaqueté une seule fois                     |
| **Conteneur** | Instance active d’une image, en cours d'exécution         |

---

### 🛠️ Commandes Docker courantes avec les images

| Commande                        | Rôle                                                                 |
|----------------------------------|----------------------------------------------------------------------|
| `docker build -t nom_image .`   | Crée une image à partir d’un Dockerfile                             |
| `docker images`                 | Liste toutes les images disponibles localement                       |
| `docker pull nginx`            | Télécharge l’image `nginx` depuis Docker Hub                         |
| `docker rmi nom_image`         | Supprime une image                                                   |
| `docker save` / `docker load`  | Exporte ou importe une image vers/depuis un fichier                  |
| `docker tag`                   | Renomme une image (utile pour l’envoyer sur un registre)             |
| `docker push`                  | Envoie l’image vers un registre (ex: Docker Hub)                     |

  
- *Conteneurs* : Un conteneur est une instance d'une image. Il exécute le code de l'application dans un environnement isolé, ce qui permet d'éviter les conflits de dépendances et facilite le déploiement.

> 🧠 **Image = modèle**, **Conteneur = instance vivante**.

### 🔐 Caractéristiques principales d’un conteneur Docker :
- Léger (partage le noyau du système hôte)
- Isolé (processus, réseau, système de fichiers)
- Démarrage rapide
- Jetable (on peut le supprimer et le recréer facilement)

---

### 🧱 Rappel : Différence entre image et conteneur

| Élément      | Description                                               |
|--------------|-----------------------------------------------------------|
| **Image**    | Modèle figé, empaqueté une seule fois                     |
| **Conteneur**| Instance active d’une image, en cours d'exécution         |

---

### 🛠️ Commandes Docker courantes avec les conteneurs

| Commande                              | Rôle                                                                 |
|----------------------------------------|----------------------------------------------------------------------|
| `docker run nom_image`                | Lance un nouveau conteneur à partir d’une image                     |
| `docker run -d -p 8080:80 nom_image`  | Détache le conteneur et mappe un port de l’hôte                     |
| `docker ps`                           | Affiche les conteneurs en cours d'exécution                         |
| `docker ps -a`                        | Affiche tous les conteneurs (même ceux arrêtés)                     |
| `docker exec -it nom_conteneur bash`  | Ouvre un terminal dans le conteneur en cours                        |
| `docker logs nom_conteneur`           | Affiche les logs du conteneur                                       |
| `docker stop nom_conteneur`           | Arrête un conteneur en cours                                        |
| `docker start nom_conteneur`          | Redémarre un conteneur arrêté                                       |
| `docker restart nom_conteneur`        | Redémarre un conteneur                                              |
| `docker rm nom_conteneur`             | Supprime un conteneur                                               |

---


👉 Cette commande :
- Télécharge l’image `nginx` si elle n’est pas encore présente
- Lance un conteneur en arrière-plan (`-d`)
- Fait correspondre le port `8080` de ton PC avec le port `80` du conteneur

  
- *Dockerfile* : C'est un fichier texte qui contient une série d'instructions sur la manière de construire une image Docker. Par exemple, il peut spécifier le système d'exploitation de base, les dépendances à installer, et la façon de lancer l'application.
> Il sert de **recette** : Docker lit ce fichier et construit une image étape par étape.

---

### 🧱 Structure typique d’un Dockerfile

```dockerfile
# 1. Image de base
FROM python:3.9-slim

# 2. Définir le répertoire de travail
WORKDIR /app

# 3. Copier les fichiers dans l'image
COPY . .

# 4. Installer les dépendances
RUN pip install -r requirements.txt

# 5. Exposer un port
EXPOSE 5000

# 6. Définir la commande à exécuter
CMD ["python", "app.py"]
```

---


```

### 📦 Commandes associées :
```bash
docker build -t mon-app .
docker run -p 5000:5000 mon-app
```

---

### 📚 Principales instructions Dockerfile

| Instruction   | Rôle                                                                 |
|---------------|----------------------------------------------------------------------|
| `FROM`        | Spécifie l’image de base                                             |
| `WORKDIR`     | Définit le répertoire de travail dans l’image                        |
| `COPY`        | Copie les fichiers du projet local vers l’image                      |
| `RUN`         | Exécute une commande pendant la construction de l’image              |
| `CMD`         | Définit la commande à exécuter par défaut dans le conteneur          |
| `ENTRYPOINT`  | Définit une commande fixe à exécuter dans le conteneur               |
| `EXPOSE`      | Indique le port que l’application écoute                             |
| `ENV`         | Définit des variables d’environnement                                |
| `ARG`         | Définit des arguments de construction                                |
| `LABEL`       | Ajoute des métadonnées à l’image                                     |

---

### 🔎 Bonnes pratiques :
- Utiliser une image de base légère (ex: `alpine`).
- Ajouter un `.dockerignore` pour éviter de copier des fichiers inutiles.
- Grouper les `RUN` pour limiter le nombre de couches.

---

Souhaites-tu que je t’aide à créer un Dockerfile pour un autre langage ou environnement (Node.js, PHP, Java, etc.) ? Ou à générer un `.dockerignore` ? 

  




- *Docker Hub* : C'est un registre public d'images Docker où les développeurs peuvent partager et télécharger des images.

| Élément        | Rôle                                                                 |
|------------------|----------------------------------------------------------------------|
| `Dockerfile`     | Décrit comment construire une image                                 |
| `docker build`   | Crée une image à partir du Dockerfile                               |
| `docker run`     | Crée et lance un conteneur basé sur une image                       |
| `Image`          | Modèle figé, prêt à l’emploi                                        |
|`Conteneur`       | Instance d’une image, en cours d’exécution                          |
| `docker ps`      | Liste les conteneurs en cours d'exécution                           |
| `docker images`  | Liste les images Docker disponibles localement                      |
| `docker exec`    | Exécute une commande dans un conteneur en cours                     |
| `docker stop`    | Arrête un conteneur en cours d’exécution                            |
| `docker rm`      | Supprime un conteneur                                               |
| `docker rmi`     | Supprime une image                                                  |
| `docker pull`    | Télécharge une image depuis Docker Hub                              |
| `docker push`    | Envoie une image vers un registre distant (ex : Docker Hub)         |
| `docker-compose` | Gère plusieurs conteneurs à partir d’un fichier `docker-compose.yml`|



**Docker Compose** est un outil qui permet de **définir et gérer plusieurs conteneurs** Docker à l’aide d’un seul fichier `docker-compose.yml`.

> Idéal pour les applications **multi-services** (ex : une app web + une base de données).

---

### 📦 Avantages
- Tout est **décrit dans un seul fichier** YAML
- Déploiement plus simple avec une seule commande (`docker-compose up`)
- Facile à **partager** et **reproduire** sur d'autres machines

---

### 📁 Exemple d'architecture

Imaginons une application web Flask avec une base de données PostgreSQL.

### 🔸 Structure :
```
mon-projet/
├── app/
│   ├── app.py
│   ├── requirements.txt
│   └── Dockerfile
└── docker-compose.yml
```

---

### 🔸 Fichier `app/app.py` (extrait)
```python
from flask import Flask
import psycopg2

app = Flask(__name__)

@app.route("/")
def index():
    return "Application Flask connectée à PostgreSQL"
```
---

### 🔸 Fichier `docker-compose.yml`
```yaml
version: '3.8'

services:
  web:
    build: ./app
    ports:
      - "5000:5000"
    depends_on:
      - db

  db:
    image: postgres:13
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: password
      POSTGRES_DB: mydb
```

---

### ▶️ Commandes utiles

| Commande                      | Rôle                                                       |
|-------------------------------|------------------------------------------------------------|
| `docker-compose up`           | Démarre les services définis dans le fichier               |
| `docker-compose up -d`        | Démarre en arrière-plan (mode détaché)                     |
| `docker-compose down`         | Arrête et supprime les conteneurs                         |
| `docker-compose build`        | Construit les images définies dans `docker-compose.yml`    |
| `docker-compose ps`           | Liste les services en cours                               |
| `docker-compose logs`         | Affiche les logs                                           |

---

- Le fichier `docker-compose.yml` permet de **gérer plusieurs conteneurs ensemble**
- Chaque **service** correspond à un conteneur
- Compose facilite le **développement local** ou les déploiements cohérents

---


**Docker Network** permet à plusieurs conteneurs de communiquer entre eux, ou avec l'extérieur, de façon contrôlée.

> Par défaut, Docker crée des réseaux internes pour gérer les communications entre conteneurs.

---

### 🔗 Pourquoi utiliser les réseaux Docker ?

- Isoler les conteneurs pour plus de sécurité
- Permettre la communication entre conteneurs
- Connecter un conteneur à plusieurs réseaux
- Gérer des architectures multi-services (ex: web + db)

---

## 🧱 Types de réseaux Docker

| Type          | Description                                                                 |
|---------------|-----------------------------------------------------------------------------|
| `bridge`      | Réseau privé par défaut pour les conteneurs sur le même hôte Docker        |
| `host`        | Le conteneur partage le réseau de l’hôte (pas d’isolation réseau)           |
| `none`        | Le conteneur n’a **aucune** interface réseau                               |
| `overlay`     | Réseau multi-hôtes pour Docker Swarm                                       |
| `macvlan`     | Attribue une adresse IP du réseau physique à un conteneur (avancé)         |

---

## 🛠️ Commandes Docker Network

| Commande                             | Rôle                                                        |
|-------------------------------------|-------------------------------------------------------------|
| `docker network ls`                 | Liste tous les réseaux Docker                              |
| `docker network create nom`         | Crée un nouveau réseau (par défaut : bridge)               |
| `docker network rm nom`             | Supprime un réseau Docker                                  |
| `docker network inspect nom`        | Affiche les détails d’un réseau                            |
| `docker network connect`            | Connecte un conteneur à un réseau                          |
| `docker network disconnect`         | Déconnecte un conteneur d’un réseau                        |

---

## 🧪 Exemple simple

### 1. Créer un réseau personnalisé :
```bash
docker network create mon_reseau
```

### 2. Lancer deux conteneurs dans le même réseau :
```bash
docker run -dit --name conteneur1 --network mon_reseau alpine sh
docker run -dit --name conteneur2 --network mon_reseau alpine sh
```

### 3. Depuis `conteneur1`, pinguer `conteneur2` :
```bash
docker exec -it conteneur1 sh
ping conteneur2
```

👉 Les deux conteneurs peuvent se communiquer **par leur nom**, grâce au DNS interne de Docker.

---

Souhaites-tu que je t’ajoute un exemple de configuration réseau dans un fichier `docker-compose.yml` ? Ou que je te montre l’utilisation d’un réseau `overlay` pour Docker Swarm ?



## Pourquoi utiliser Docker ?

- *Portabilité* : Les conteneurs peuvent être exécutés sur n'importe quel système hôte qui a Docker installé, ce qui facilite le déploiement sur différents environnements (développement, testing, production).
  
- *Isolation* : Les applications s'exécutent dans des environnements isolés, ce qui réduit le risque de conflits entre les dépendances.
  
- *Évolutivité* : Docker permet de gérer facilement les mises à l'échelle horizontales en ajoutant ou en supprimant des conteneurs selon la demande.

## Commandes Docker de base

- docker pull [image] : Télécharge une image depuis Docker Hub.
- docker build -t [nom_image] . : Crée une image à partir d'un Dockerfile dans le répertoire courant.
- docker run [options] [image] : Exécute un conteneur à partir d'une image.
- docker ps : Liste les conteneurs en cours d'exécution.
- docker stop [id_conteneur] : Arrête un conteneur en cours d'exécution.
- docker rm [id_conteneur] : Supprime un conteneur arrêté.
