Introduction
===================================


Bienvenue dans la documentation officielle du projet OC Lettings. Ce document vous guidera à travers les différents aspects techniques de l'application, y compris son installation, sa configuration, son déploiement, ainsi que des détails sur son architecture et son utilisation. Avant de commencer, voici quelques informations essentielles à connaître ainsi que les prérequis pour bien démarrer avec le projet.

Prérequis
---------------------

Pour commencez, assurez-vous d'avoir les outils suivants installés sur votre machine :

==============================
Docker
==============================

- Nous utilisons **Docker** pour containeriser et exécuter l'application dans des environnements reproductibles.

==============================
Compte Render
==============================

- **Render** est la plateforme choisie pour le déploiement de l'application en production. Un compte est nécessaire pour y accéder.

==============================
GitHub
==============================

- Le code source est hébergé sur **GitHub**. Vous aurez besoin d'un compte pour cloner le projet et contribuer.

==============================
Python 3.11+
==============================

- **OC Lettings** est un projet écrit en Python. Assurez-vous d'avoir la version correcte installée.

==============================
Pip
==============================

- Gestionnaire de dépendances pour installer les bibliothèques requises.

==============================
Sentry
==============================

- Sentry est intégré à l'application pour surveiller les erreurs. Un compte est nécessaire pour y accéder.



Objectifs et Cahier des Charges
---------------------

==============================
Développement Structuré du Projet
==============================

Le développement a été structuré autour de plusieurs grandes étapes, chacune ayant des objectifs bien définis :

1 - Architecture et Mise en Place des Applications
----------------------------------------------

- Mise en place de l'application principale, nommée **oc_lettings_site**, et création de deux sous-applications spécifiques :
  
  - **lettings** : gestion des locations immobilières.
  
  - **profiles** : gestion des profils utilisateurs.

- Configuration initiale de Django avec les vues, les modèles, et les URLs pour ces sous-applications.

- Chaque application est autonome, avec ses propres modèles, vues, et fichiers de test, tout en étant connectée à l'application principale pour un accès global.

2 - Réduction de la Dette Technique et Refactorisation
--------------------------------------------------

- Résolution des erreurs de linting grâce à l'intégration de **flake8** et correction des problèmes de pluralisation dans l'administration (notamment pour le terme "Address").

- Ajout de pages personnalisées pour la gestion des erreurs **404** et **500**.

- Refactorisation du code avec l'ajout de **docstrings** claires pour toutes les classes, fonctions, et modules, permettant une meilleure compréhension et maintenance du code.

- Mise en place de tests unitaires pour les vues, les modèles et les URL, avec une couverture de test supérieure à **80 %**.

3 - Surveillance des Erreurs et Suivi avec Sentry
---------------------------------------------

- Intégration de **Sentry** pour capturer les erreurs en production.

- Utilisation du module **logging** pour ajouter des logs dans les parties critiques du code (comme les blocs **try/except** et les fonctions sensibles).

- Configuration de Sentry avec une clé API stockée dans des variables d'environnement pour assurer la sécurité des données sensibles.

4 - Mise en Place d’un Pipeline CI/CD
----------------------------------

- Utilisation de **GitHub Actions** pour mettre en place un pipeline automatisé qui :

  - Exécute les tests unitaires et de linting à chaque commit sur la branche principale (**main**).
  
  - Construit une image **Docker** de l'application et la pousse sur **Docker Hub** avec un tag correspondant au hash du commit.
  
  - Déploie l'application sur **Render** après la validation des tests et du build Docker.

- La configuration assure que le déploiement ne se fait que si tous les tests et le build sont réussis.

5 - Documentation du Projet et Déploiement sur Read the Docs
--------------------------------------------------------

- Documentation complète du projet hébergée sur **Read the Docs**, avec des explications détaillées sur chaque étape, les technologies utilisées, et les procédures d'installation et de déploiement.

- Le déploiement suit un processus documenté, permettant à tout développeur de comprendre les étapes nécessaires pour faire fonctionner l'application localement ou en production.



# Technologies Utilisées
---------------------
- Django : Framework web utilisé pour la création de l'application.
- Docker : Utilisé pour la conteneurisation et le déploiement de l'application.
- GitHub Actions : Outil CI/CD utilisé pour l'automatisation des tests et du déploiement.
- Sentry : Outil de surveillance des erreurs en production.
- Render : Service d'hébergement utilisé pour le déploiement de l'application en production.
