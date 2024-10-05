==================================
Réduction des problèmes techniques
==================================

L'objectif de cette deuxième étape est de corriger les problèmes techniques identifiés, d'améliorer la gestion des erreurs, d'augmenter la couverture des tests et d'améliorer la documentation.

Correction des erreurs de linting
---------------------------------

Les erreurs signalées par **flake8** ont été corrigées sans modifier la configuration de **setup.cfg**, en particulier dans le fichier `oc_lettings_site/views.py`. Le projet est maintenant conforme à **PEP8**.

Correction de la pluralisation
------------------------------

Une erreur dans la pluralisation du terme "Addresss" dans l'administration Django a été corrigée en ajoutant le paramètre `verbose_name_plural` dans le modèle **Address** :

.. code-block:: python

    class Address(models.Model):
        # champs du modèle
        class Meta:
            verbose_name_plural = "Addresses"

Gestion des erreurs 404 et 500
------------------------------

Des pages personnalisées pour les erreurs **404** (page non trouvée) et **500** (erreur serveur) ont été mises en place, améliorant l'expérience utilisateur en production.

Documentation via des docstrings
--------------------------------

Des **docstrings** ont été ajoutées à chaque module, classe et fonction, selon les standards Python, pour documenter le projet de manière claire et concise. Ces docstrings décrivent les paramètres, les valeurs de retour, et les comportements attendus.

Mise en place des tests unitaires
---------------------------------

Des tests unitaires et d'intégration ont été créés pour chaque application. Les tests couvrent les modèles, vues et URLs des applications **lettings** et **profiles**. L'objectif de couverture de **80 %** a été atteint grâce à l'utilisation de **pytest** et **pytest-cov**.

