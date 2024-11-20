# E5-CCISP
Djamel MOAD Rendue 




<!-- PROJECT LOGO --> <br /> <div align="center"> <h3 align="center">Projet Docker : Applications Web</h3> <p align="center"> 
<a href="https://github.com/app-generator/django-soft-ui-dashboard"><strong>Documentation Django Soft UI Dashboard »</strong></a> <br /> 
<a href="https://github.com/app-generator/flask-soft-ui-design">Documentation Flask Soft UI Design</a> · 
<a href="https://github.com/app-generator/ecommerce-flask-stripe">Documentation Ecommerce Flask Stripe</a> · 
<a href="https://github.com/app-generator/rocket-django">Documentation Rocket Django</a> </p> </div>



<!-- TABLE OF CONTENTS --> <details> <summary>Table des matières</summary> <ol> <li><a href="#structure-du-projet">Structure du projet</a></li> <li><a href="#configurations">Configurations</a></li> 
<li><a href="#etape-du-build">Étape du build</a></li> <li><a href="#logs">Logs</a></li> <li><a href="#quelques-interfaces">Quelques Interfaces</a></li> </ol> </details>



<!-- ABOUT THE PROJECT -->
## Struture du projet

Voici la structure du projet:

```bash
< PROJECT ROOT >
   |
   |-- apps/
   |    |-- django-soft-ui-dashboard/
   |    |-- flask-soft-ui-design/
   |    |-- ecommerce-flask-stripe/
   |    |-- rocket-django/
   |
   |-- nginx/
   |    |-- nginx.conf
   |
   |-- docker-compose.yml
   ************************************************************************
```


<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- FILES CONFIGURATIONS -->
## Configurations

. Contenu du fichier mynginxconf.conf

``` bash
# Django Soft UI Dashboard
upstream django-soft-ui {
    server django-soft-ui:8000;
}

server {
    listen 7010;
    server_name localhost;

    location / {
        proxy_pass http://django-soft-ui;
        proxy_set_header Host $host:$server_port;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}

# Flask Soft UI Design
upstream flask-soft-ui {
    server flask-soft-ui:5000;
}

server {
    listen 7011;
    server_name localhost;

    location / {
        proxy_pass http://flask-soft-ui;
        proxy_set_header Host $host:$server_port;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}

# Ecommerce Flask Stripe
upstream ecommerce-flask-stripe {
    server ecommerce-flask-stripe:7000;
}

server {
    listen 7012;
    server_name localhost;

    location / {
        proxy_pass http://ecommerce-flask-stripe;
        proxy_set_header Host $host:$server_port;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}

# Rocket Django
upstream rocket-django {
    server rocket-django:8001;
}

server {
    listen 7013;
    server_name localhost;

    location / {
        proxy_pass http://rocket-django;
        proxy_set_header Host $host:$server_port;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}

```

. Contenu du docker-compose.yml

``` bash
version: '3.8'

services:
  django-soft-ui:
    build: ./apps/django-soft-ui-dashboard
    ports:
      - "8000:8000"
    networks:
      - app_network

  flask-soft-ui:
    build: ./apps/flask-soft-ui-design
    ports:
      - "5000:5000"
    networks:
      - app_network

  ecommerce-flask-stripe:
    build: ./apps/ecommerce-flask-stripe
    ports:
      - "7000:7000"
    networks:
      - app_network

  rocket-django:
    build: ./apps/rocket-django
    ports:
      - "8001:8001"
    networks:
      - app_network

  nginx:
    image: nginx:latest
    ports:
      - "7010:7010"
      - "7011:7011"
      - "7012:7012"
      - "7013:7013"
    volumes:
      - ./nginx:/etc/nginx/conf.d
    depends_on:
      - django-soft-ui
      - flask-soft-ui
      - ecommerce-flask-stripe
      - rocket-django
    networks:
      - app_network

networks:
  app_network:
    driver: bridge

```

<!-- GETTING STARTED -->
## Etape du build

### Pour déployer les applications du répertoire "devoir":

1- Positionnez vous dans ce répertoire avec la commande suivante:

``` bash
cd devoir
```

2- Exécuter la commande suivante pour mettre en place votre iac:

``` bash
docker compose up -d
```

3- Après le build, tapez les commandes suivantes:

``` bash
docker images
docker ps
```

. Screen présentant les images

![alt text](screens/image.png)

``` bash
docker ps
```
ou
``` bash
docker ps -a
```
. Screen présentant les conteneurs en cours d'exécution

![alt text](screens/dockerps.png)

Testez vos applications en local sur les ports suivants:
  <ul>
    <li><a href="#http://localhost:7010">http://localhost:7010</a></li>
    <li><a href="#http://localhost:7011">http://localhost:7011</a></li>
    <li><a href="#http://localhost:7012">http://localhost:7012</a></li>
    <li><a href="#http://localhost:7013">http://localhost:7013</a></li>
    <li><a href="#http://localhost:80">http://localhost:80</a></li>
    <li><a href="#http://localhost:81">http://localhost:81</a></li>
    <li><a href="#http://localhost:82">http://localhost:82</a></li>
    <li><a href="#http://localhost:83">http://localhost:83</a></li>
    <li><a href="#http://localhost:84">http://localhost:84</a></li>
    <li><a href="#http://localhost:85">http://localhost:85</a></li>
    <li><a href="#http://localhost:86">http://localhost:86</a></li>
  </ul>

4- Pushez vos images sur le docker hub

. Connectez vous au docker hub:

``` bash
docker login
```

. Déplacer dans le répertoire de l'application pour exécuter les commandes suivantes:
``` bash
cd  nom_application
```

``` bash
docker build -t nom_image:tag_name .
```

``` bash
docker tag nom_image:tag: your_username/nom_image:tag_name_for_hub
```

``` bash
docker push your_username/nom_image:tag_name_for_hub
```


. Screen présentant les logs obtenus lors d'un push

![alt text](screens/pushes.png)

. Docker Hub repositories

![alt text](screens/hub.png)

<p align="right">(<a href="#readme-top">back to top</a>)</p>


<!-- INTERFACES -->
## Quelques interfaces

. ecommerce-fastapi-stripe

![alt text](screens/app1.png)

. ecommerce-flask-stripe

![alt text](screens/app2.png)

. flask-black-dashboard

![alt text](screens/app3.png)


## Docker

1. La solution docker dans ce projet nous permet d'optimiser notre déploiement en minimisant le temps du build pour la mise en production tout en maintenant la portabilité de notre infrastructure en cas de changement.

2. Docker s'inscrit dans la méthodologie DevOps en facilitant l'intégration continue et le déploiement automatique des applications en passant par la conteneurisation des applications (packaging), le gain de temps lors du déploiement grâce à l'automatisation et la création des pipelines CI/CD, la portabilité et la sécurité des applications.

## Diagramme iac

![alt text](screens/iac.png)
