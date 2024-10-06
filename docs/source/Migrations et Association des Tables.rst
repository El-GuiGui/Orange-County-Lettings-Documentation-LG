Migrations et Association des Tables  
====================================

1. Réorganisation des Modèles et Réutilisation des Tables
------------------------------------

Dans le cadre de la refactorisation du projet, nous avons séparé le projet en plusieurs applications distinctes : **lettings**, **profiles**, et **oc_lettings_site**. Les modèles **`Address`**, **`Letting`**, et **`Profile`** ont été déplacés vers leurs applications respectives tout en **réutilisant les tables existantes** de la base de données, **sans recréation ni suppression manuelle des tables**, conformément aux exigences du cahier des charges.

**Il y a juste eu a modifié l'état des modèles pour les adapter à la nouvelle structure modulaire.** 

Un mappage entre les modèles nouvellement migrés et les tables originelles.


2. Association des Modèles aux Tables Existantes
------------------------------------

Les fichiers de migration ont permis de :  

- **Associer les nouveaux modèles aux tables déjà présentes dans la base de données**. Cette association a été faite en spécifiant l'option **`db_table`** dans les fichiers de migration pour chaque modèle.  
- **Conserver les relations entre les modèles** sans affecter la structure de la base de données.

Grâce à l'option **`db_table`**, les modèles dans les nouvelles applications ont été directement associés aux tables déjà existantes. 
Aucune nouvelle table n'a été créée, et les anciennes tables n'ont pas été supprimées manuellement.

3. Modèles Migrés et Réutilisation des Tables
------------------------------------

Application **lettings**

**Modèle `Address`** :  

- **Table réutilisée** : **`oc_lettings_site_address`**  
- Le modèle `Address` a été déplacé de l'application principale **`oc_lettings_site`** vers l'application **`lettings`**, en réutilisant la table **`oc_lettings_site_address`** sans modification.

**Modèle `Letting`** :  

- **Table réutilisée** : **`oc_lettings_site_letting`**  
- Le modèle `Letting` a été déplacé vers l'application **`lettings`**, tout en utilisant la table **`oc_lettings_site_letting`**.

Application **profiles**

**Modèle `Profile`** : 

- **Table réutilisée** : **`oc_lettings_site_profile`**  
- Le modèle `Profile` a été déplacé dans l'application **`profiles`**, en utilisant la table **`oc_lettings_site_profile`**.

4. Gestion des Relations entre les Modèles
------------------------------------

Les relations définies dans les modèles ont été préservées après les migrations. 

Cela inclut les relations **`OneToOneField`** entre :  

- Un **`Letting`** et un **`Address`** ;  
- Un **`Profile`** et un **`User`**.

Ces relations ont été intégrées dans les fichiers de migration et sont restées inchangées après la réorganisation.

5. Visualisation des Tables après Migration
------------------------------------

Voici la liste des tables de la base de données après exécution des migrations :


   .. image:: img/dbtable.PNG



**Justification de l'approche actuelle**
------------------------

La décision de conserver les tables existantes dans la base de données et de les relier aux nouvelles applications via des migrations adaptées repose sur ces raisons :

Minimisation des risques
------------------------

En conservant les tables déjà en place, les risques associés à la migration manuelle des données ont été réduits, notamment :

- **Prévention de la perte de données** : La migration manuelle comporte des risques d'erreurs, surtout si les relations entre les tables ou les contraintes d'intégrité ne sont pas correctement gérées.
  
- **Préservation de l'intégrité des données** : En liant les anciennes tables aux nouveaux modèles, l'intégrité des données est maintenue, assurant ainsi une continuité dans le fonctionnement du site.

Gain de temps et simplification de la maintenance
-------------------------------------------------

Réutiliser les tables existantes a permis d'accélérer le processus de refactorisation, en évitant une restructuration complète de la base de données. Cette méthode facilite également la maintenance à court terme, réduisant ainsi les risques d'erreurs lors de futures migrations.


Maintien des fonctionnalités
-----------------------------

L'approche adoptée respecte des exigences clé du projet :

 - **préserver les fonctionnalités et l'apparence du site** 
 - **il ne faut pas utiliser le langage SQL directement dans le fichier de migration**
 - **modifier manuellement les tables et la DB**

En évitant la recréation des tables, l'accent a pu être mis sur l'amélioration de la modularité du code sans altérer le fonctionnement de l'application.
