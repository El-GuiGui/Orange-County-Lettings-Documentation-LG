Welcome to Orange County Lettings documentation!
===================================

Description du projet
---------------------
Le projet OC Lettings est une application web axée sur la gestion de propriétés à louer et de profils d'utilisateurs. Il utilise le framework Django et est conçu pour offrir une expérience fluide tant pour les utilisateurs finaux que pour les administrateurs. 

L'application permet aux utilisateurs de :

- Consulter les propriétés à louer
- Visualiser les profils d'utilisateurs
- Gérer les données via l'interface admin de Django

.. image:: img/home%20page.PNG

.. image:: img/admin%20page%20modif.PNG

Ce projet est divisé en trois applications distinctes :

- **Lettings** : Pour la gestion des lettings.

- **Profiles** : Pour la gestion des profiles.

- **oc_lettings_site** : Pour la gestion des settings, et des fichiers de base.




L'un des objectifs principaux de ce projet était d'assurer la stabilité et la fiabilité via une couverture de tests complète, un suivi des erreurs avec Sentry et une pipeline CI/CD automatisée avec GitHub Actions, Docker, et Render.

.. note::

   Project repository : https://github.com/El-GuiGui/P13-Mettez-a-l-echelle-une-application-Django-en-utilisant-une-architecture-modulaire

   .. image:: img/repository.PNG



Contents
--------

.. toctree::

   introduction
   structure du projet
   Installation du projet en local
   Démarrage rapide en local
   Technologies et techniques utilisées
   Structure de la base de données
   Url et Guide d'utilisation
   Automatisation CI-CD via Github Actions
   Déploiement sur render
   Image du projet sur Docker
   Lancement de l'image docker en local.
   Le stockage de clé et mot de passe dans un environnement de production
   Surveillance des Erreurs avec Sentry
   User Guide
   Lien
   other
