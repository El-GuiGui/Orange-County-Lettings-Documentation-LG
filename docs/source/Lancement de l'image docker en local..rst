Lancement de l'image docker en local
====================================

Utilisation locale de l'image Docker
------------------------------------

Il est possible de récupérer l'image Docker du projet depuis Docker Hub pour l'exécuter localement :

1. **Récupérer l'image Docker** :

.. code-block:: bash

   docker pull ggui/oc_lettings:latest

2. **Lancer le conteneur Docker** :

.. code-block:: bash

   docker run -d -p 8000:8000 ggui/oc_lettings:latest

   # Ou pour une version spécifique avec un tag hash de commit
   docker run -d -p 8000:8000 ggui/oc_lettings:${{ github.sha }}

Cela permettra de lancer l'application avec http://localhost:8000, et vous pourrez interagir avec l'application en local via Docker sans avoir à installer toutes les dépendances sur votre machine.
