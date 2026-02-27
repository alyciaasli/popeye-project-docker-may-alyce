----POPEYE – Conteneurisation d’une Application Full Stack

Ce projet consiste à conteneuriser une application full stack en utilisant Docker et Docker Compose.
L’application permet de voter via une interface web et d’afficher les résultats en temps réel.

L’architecture repose sur plusieurs services indépendants communiquant via des réseaux Docker.

Architecture:
L’application est composée de 5 services:

Poll (Flask – Python):

Interface web de vote.
Envoie les votes vers Redis.

Redis:

File d’attente qui stocke temporairement les votes.

Worker (Java):

Récupère les votes depuis Redis et les enregistre dans PostgreSQL.
Construit avec un multi-stage build.

PostgreSQL:

Base de données persistante.
Utilise un volume Docker db-data.

Result (Node.js):

Affiche les résultats en lisant les données depuis PostgreSQL.

🌐 Réseaux Docker:
Trois réseaux sont utilisés :

poll-tier (Poll ↔ Redis)

back-tier (Worker ↔ Redis & DB)

result-tier (Result ↔ DB)

Lancer l’application:
Depuis la racine du projet :

docker-compose up --build

Accès :

Poll → http://localhost:5000

Result → http://localhost:5001

Arrêter:
docker-compose down
Docker Hub

Images publiées sur Docker Hub :

alyciaasli/poll
alyciaasli/worker
alyciaasli/result

Build :

docker build -t alyciaasli/poll:latest ./poll
docker build -t alyciaasli/worker:latest ./worker
docker build -t alyciaasli/result:latest ./result

Push :

docker push alyciaasli/poll:latest
docker push alyciaasli/worker:latest
docker push alyciaasli/resulrt:latest
