Installation du Projet en Local
===============================

Cette section explique comment installer et configurer l'application **Orange County Lettings** pour un environnement de développement local.

Prérequis
---------
- Python 3.11 ou supérieur
- Gitet pip
- Docker (pour les tests de conteneurisation)

Étapes d'Installation
----------------------

1. Cloner le Repository
-----------------------
Pour commencer, vous devez cloner le repository sur votre machine locale.

.. code-block:: bash

   cd /chemin/vers/votre/projet/
   git clone https://github.com/El-GuiGui/P13-Mettez-a-l-echelle-une-application-Django-en-utilisant-une-architecture-modulaire.git

Cela téléchargera le projet dans le répertoire spécifié.

2. Créer un Environnement Virtuel
---------------------------------
Une fois le projet cloné, vous devez créer un environnement virtuel pour isoler les dépendances du projet.

.. code-block:: bash

   cd /chemin/vers/Python-OC-Lettings-FR
   python -m venv venv

3. Activer l'Environnement Virtuel
----------------------------------
Activez l'environnement virtuel afin d'installer les dépendances sans affecter votre installation globale de Python.

Sur Linux ou macOS :

.. code-block:: bash

   source venv/bin/activate

Sur Windows :

.. code-block:: bash

   venv\Scripts\activate

4. Vérifications
----------------
Avant d'installer les dépendances, vérifiez que votre environnement est bien configuré.

- Assurez-vous que `python` pointe vers l'interpréteur de l'environnement virtuel :

  .. code-block:: bash

     which python

- Assurez-vous que la version de Python est 3.9 ou supérieure :

  .. code-block:: bash

     python --version

- Vérifiez que `pip` pointe vers l'exécutable de l'environnement virtuel :

  .. code-block:: bash

     which pip

Si tout est en ordre, vous pouvez continuer à installer les dépendances.

5. Installer les Dépendances
----------------------------
Le fichier `requirements.txt` contient toutes les dépendances nécessaires au bon fonctionnement de l'application. Installez-les avec la commande suivante :

.. code-block:: bash

   pip install --requirement requirements.txt

6. Configurer les Variables d'Environnement
-------------------------------------------
Il est nécessaire de configurer un fichier `.env` pour stocker les clés sensibles telles que `SECRET_KEY` et la clé Sentry `SENTRY_DSN`. Un fichier `.env.example` est fourni comme modèle dans le projet. Créez un fichier `.env` à la racine du projet en suivant cet exemple.

.. code-block:: text

   SECRET_KEY="votre_clé_secret"
   DEBUG=True
   SENTRY_DSN="votre_clé_sentry"

7. Exécuter le Site Web en Local
-------------------------------
Une fois les dépendances installées et les variables d'environnement configurées, vous pouvez lancer le site en local.

.. code-block:: bash

   python manage.py runserver

Ouvrez un navigateur et accédez à l'adresse suivante pour vérifier que l'application fonctionne correctement :

.. code-block:: text

   http://localhost:8000

Vous devriez être en mesure de naviguer entre les pages de profils et de locations sans problème.

La page admin : 

.. code-block:: text

   http://localhost:8000/admin

- Utilisateur: admin
- Mot de passe: Abc1234!

8. Gestion des Statics en Local
-------------------------------
Si vous rencontrez des problèmes avec les fichiers statiques (CSS, JS, etc.), assurez-vous que `DEBUG` est réglé sur **True** dans le fichier `settings.py`. Cela vous permet d'utiliser les fichiers statiques en mode développement local.



Désactiver l'Environnement Virtuel
-----------------------------------
Une fois que vous avez terminé, vous pouvez désactiver l'environnement virtuel en tapant la commande suivante :

.. code-block:: bash

   deactivate


