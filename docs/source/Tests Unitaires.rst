Tests Unitaires
===============

Le projet utilise **pytest** pour les tests unitaires afin de garantir que chaque partie de l'application fonctionne correctement. Une couverture de test supérieure à 80 % est exigée, comme précisé dans le cahier des charges.

**ICI le résultats est de 97%** 

Organisation des Tests
----------------------

Les tests sont organisés de manière à être regroupés par application pour faciliter leur gestion et leur exécution. Chaque application possède un fichier `tests.py` dans lequel les tests sont implémentés. Voici la structure :

.. code-block:: bash

 /
  oc_lettings_site/
      tests.py
  lettings/
      tests.py
  profiles/
      tests.py

Exécution des Tests
-------------------

Les tests unitaires sont exécutés automatiquement dans le pipeline CI/CD. Si un test échoue, le pipeline s'arrête et l'erreur est remontée.

Pour exécuter les tests en local :

.. code-block:: bash

    pytest --cov

Cette commande exécute tous les tests et fournit un rapport de couverture de code :

   .. image:: img/pytest-coverage.PNG


