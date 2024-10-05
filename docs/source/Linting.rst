
Linting
=======

Le projet utilise **Flake8** pour le linting afin de s'assurer que le code respecte les règles de style.

Configuration de Flake8
-----------------------

Le fichier `setup.cfg` contient la configuration de Flake8, qui définit les règles à respecter :

.. code-block:: ini

    [flake8]
    max-line-length = 119
    exclude =
        migrations,
        .venv,
        .git,
        __pycache__


Exécution du Linting
--------------------

Flake8 est exécuté automatiquement dans le pipeline CI/CD. Si des erreurs sont détectées, le pipeline échoue.

Pour exécuter Flake8 en local :

.. code-block:: bash

    flake8

Cette commande vérifie tout le projet et affiche les erreurs qui ne respectent pas les règles.


Le rapport en détail :
--------------------


Pour générer un rapport de linting en format HTML, installez le plugin flake8-html avec la commande suivante :


.. code-block:: bash

    pip install flake8-html


Puis générer un rapport de linting en format HTML :

.. code-block:: bash

    flake8 --format=html --htmldir=flake-report



Le rapport :

   .. image:: img/flake8-report.PNG
