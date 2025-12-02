# AWS-Modernization-Java-Project-vProfile-Application

📌 Overview

vProfile est une application web Java EE (JEE) composée d’un frontend et d’un backend.
Dans ce projet, l’application a été refactorée puis modernisée pour être déployée sur une architecture scalable, hautement disponible et sécurisée sur Amazon Web Services (AWS).

Ce projet démontre :

la migration d’une application locale vers AWS

la mise en place d’un environnement cloud professionnel

la séparation frontend / backend

l’utilisation de services managés AWS (RDS, ElastiCache, CloudFront, Route 53…)

un déploiement backend sur Tomcat + EC2 + Auto Scaling + ALB

📌 Architecture Diagram

photo diagramme

📌 AWS Services Used
🖥 Compute & Scaling

EC2 — Serveur Tomcat hébergeant le backend JEE

Auto Scaling Group (ASG) — Scalabilité horizontale

Application Load Balancer (ALB) — Répartition de trafic + Health Checks

🗄️ Data Layer

Amazon RDS (MySQL) — Base de données relationnelle

ElastiCache (Memcached) — Cache distribué pour accélérer le backend

RabbitMQ — Message Broker (déployé dans le backend SG)

🌐 Frontend Hosting

S3 (Static Hosting) — Hébergement du frontend

CloudFront — CDN pour la distribution globale

Route 53 — DNS + domaine personnalisé

🔒 Identity & Management

IAM — Gestion des droits et rôles pour EC2, S3, CloudFront, RDS

Security Groups — Séparation frontend / backend / DB

📌 Architecture Description

L'architecture se compose de trois couches :

1️⃣ Frontend Layer

Hébergé sur un bucket S3

Distribué via CloudFront pour de meilleures performances

Le nom de domaine est géré via Route 53

2️⃣ Application Layer

Instances EC2 intégrées dans un Auto Scaling Group

Déploiement du backend Java EE sur Apache Tomcat

L’ALB redirige le trafic vers les instances selon leur état (Healthy)

3️⃣ Backend Layer (Services internes)

Regroupés dans un Security Group backend, non exposé à Internet :

RabbitMQ

Memcached (ElastiCache)

RDS MySQL

📌 Deployment Flow

Déploiement du backend JEE sur une instance EC2 (Tomcat)

Création d’un AMI et configuration de l’Auto Scaling Group

Mise en place d’un Application Load Balancer

Déploiement du frontend dans S3

Activation du CDN via CloudFront

Pointage du domaine (Route 53 → CloudFront → S3)

Connexion du backend aux services internes :

RabbitMQ

Memcached

RDS

📌 Project Structure
aws-modernization-java-project/
│
├── architecture/
│   └── aws-architecture-diagram.png
│
├── backend/
│   ├── src/
│   ├── pom.xml
│   └── README.md
│
├── frontend/
│   ├── src/
│   └── README.md
│
├── docs/
│   ├── screenshots/
│   └── deployment-steps.md
│
└── README.md

📌 Lessons Learned

Migrer une application legacy JEE vers AWS demande une séparation claire des services

Utilisation d’un CDN (CloudFront) améliore fortement les performances

L’Auto Scaling + ALB augmente la résilience

VPC, subnets et Security Groups sont essentiels pour la sécurité

Externaliser cache, queue, et base de données apporte robustesse et maintenabilité

📌 Tech Stack

Java EE / Tomcat 9

RabbitMQ

Memcached

MySQL (RDS)

AWS Cloud Services

CloudFront + S3

Linux / EC2 / ASG / ALB
