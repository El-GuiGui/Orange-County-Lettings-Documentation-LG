Technologies et Techniques Utilisées
====================================

Langages et Frameworks
----------------------

1. **Python** :
   L'application est principalement développée en **Python**, 

2. **Django** :
   Django est le framework Web principal utilisé pour ce projet. Il est reconnu pour sa structure robuste et son approche « soft et simple », offrant des fonctionnalités intégrées telles que :
   
   - ORM (Object-Relational Mapping) pour interagir avec la base de données.
   - Système de gestion des modèles.
   - Système d'authentification utilisateur.
   - Gestion des templates et des URL.
   
   Django a facilité la création de l'application à partir de multiples modules indépendants comme **lettings**, **profiles** et l'application principale **oc_lettings_site**.

3. **HTML/CSS et Bootstrap** :
   Le frontend du projet utilise **HTML** et **CSS**, avec l'aide de **Bootstrap**. 
   
   Bootstrap a été utilisé pour styliser les pages de l'application, notamment pour les composants comme les boutons et les mises en page. Nous avons également inclus des fichiers CSS personnalisés pour ajuster l'apparence en fonction des besoins spécifiques du projet.

4. **JavaScript** :
   Bien que l'application repose principalement sur le backend Django, des éléments de **JavaScript** ont été utilisés pour améliorer l'interactivité des pages (comme la gestion des menus ou des animations légères sur les boutons). Cependant, l'usage de JavaScript reste limité à des fonctionnalités basiques.

Conteneurisation et Déploiement
-------------------------------

1. **Docker** :
   **Docker** a été utilisé pour conteneuriser l'application afin de faciliter le développement et le déploiement dans différents environnements. En encapsulant l'application dans une image Docker, nous garantissons que la même configuration est exécutée localement et en production.
   
   - Un fichier `Dockerfile` est inclus dans le projet pour définir l'image du projet.
   - L'image Docker inclut tous les éléments nécessaires comme les dépendances Python et les fichiers statiques.

**Pour tester le projet en local en récupérant l'image Docker déjà construite et stockée sur Docker Hub, suivez ces étapes.**

1. **Récupérer l'image Docker**

Utilisez la commande suivante pour télécharger (pull) l'image Docker depuis Docker Hub :

.. code-block:: bash

    docker pull ggui/oc_lettings:latest

2. **Exécuter l'image Docker en local**

Lancez l'image Docker téléchargée en utilisant cette commande :

.. code-block:: bash

    docker run -p 8000:8000 ggui/oc_lettings:latest

3. **Accéder à l'application**

Après avoir démarré le conteneur, l'application sera disponible à l'adresse suivante dans votre navigateur :

.. code-block:: none

    http://localhost:8000


.. image:: img/docker-hist.PNG

2. **Render** :
   Pour la mise en production, nous avons choisi **Render**. Render permet de déployer des applications directement à partir de **Docker**. Les principales étapes du déploiement incluent :

   - Déploiement automatisé via **GitHub Actions** (pipeline CI/CD) pour vérifier les tests et construire l'image Docker avant le déploiement, si l'un des deux échoue, le déploiement ne se concrétise pas.
   - Utilisation de **hooks** de déploiement pour que l'application utilise toujours la dernière version de l'image Docker.
   
   Render facilite le déploiement avec une gestion simple des environnements et des variables d'environnement. 

.. image:: img/render-correct-deployed.PNG

Suivi des Erreurs et Surveillance
---------------------------------

1. **Sentry** :
   **Sentry** a été intégré au projet pour surveiller les erreurs en temps réel. Sentry permet de capturer les erreurs et les exceptions levées par l'application, ce qui facilite la résolution des bugs et améliore la stabilité globale.

   - La clé Sentry (DSN) est configurée via les **variables d'environnement**.
   - Sentry enregistre toutes les exceptions non gérées et fournit des rapports détaillés via son tableau de bord en ligne.

   Extrait du fichier `settings.py` pour l'intégration de Sentry :

   .. code-block:: python

      import sentry_sdk
      from sentry_sdk.integrations.django import DjangoIntegration
      
      sentry_sdk.init(
          dsn=os.getenv("SENTRY_DSN"),
          integrations=[DjangoIntegration()],
          traces_sample_rate=1.0,
          send_default_pii=True
      )



Tests et Qualité du Code
------------------------

1. **pytest** :
   Pour assurer la stabilité et la qualité du code, nous avons utilisé **pytest** pour l'exécution des tests unitaires et des tests d'intégration. Le but est de vérifier que chaque module et chaque fonctionnalité se comportent comme prévu.

   - Des tests ont été créés pour vérifier les modèles, les vues, et les URLs.
   - Des tests de couverture sont également utilisés pour garantir que plus de **80% du code** est couvert par les tests. (97% ici même)

   Commande pour exécuter les tests :

   .. code-block:: bash

      pytest --cov


 .. image:: img/pytest-coverage.PNG

2. **flake8** :
   **flake8** a été utilisé pour garantir que le code est conforme aux bonnes pratiques de Python (PEP8). Chaque commit est validé via un linting automatique, garantissant un code propre et lisible.

   Commande pour exécuter le linting :

   .. code-block:: bash

      flake8

 .. image:: img/flake8-result.PNG


Gestion des Statics et des Fichiers Média
-----------------------------------------

1. **Whitenoise** :
   **Whitenoise** a été utilisé pour la gestion des fichiers statiques en production. Cette solution permet à Django de servir efficacement les fichiers CSS, JS, et autres assets directement sans avoir besoin de dépendre d’un serveur externe comme Nginx.
   
   - Le middleware Whitenoise est ajouté à l'application pour servir les fichiers statiques.
   - Les fichiers statiques sont collectés via la commande `collectstatic` et stockés dans un répertoire central avant d'être déployés.

2. **Bootstrap et CSS Custom** :
   L'application utilise **Bootstrap** pour la structure visuelle des pages, et certains fichiers CSS personnalisés ont été ajoutés pour une adaptation plus spécifique du design. 
