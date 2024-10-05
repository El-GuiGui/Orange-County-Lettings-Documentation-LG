Démarrage rapide en local
===============================

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

-------------------------------
Gestion des Statics en Local
-------------------------------
Si vous rencontrez des problèmes avec les fichiers statiques (CSS, JS, etc.), assurez-vous que `DEBUG` est réglé sur **True** dans le fichier `settings.py`. Cela vous permet d'utiliser les fichiers statiques en mode développement local.


