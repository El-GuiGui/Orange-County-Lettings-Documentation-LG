Automatisation CI/CD via GitHub Actions
=======================================

L'automatisation du pipeline de CI/CD pour l'application **OC Lettings** a été mise en place en utilisant **GitHub Actions**. Ce pipeline s'assure que chaque modification apportée à la branche principale (main) est validée via une série de tests et de vérifications. Il s'assure également que l'image Docker est créée, taguée, et déployée correctement sur le serveur de production.

Structure du fichier config.yml
-------------------------------

Le fichier `config.yml` suivant a été mis en place pour orchestrer les différentes étapes du pipeline CI/CD :

.. code-block:: yaml

    name: CI/CD Pipeline

    on:
      push:
        branches:
          - main

    jobs:
      build-and-test:
        runs-on: ubuntu-latest
        steps:
          - name: Checkout the code
            uses: actions/checkout@v2

          - name: Set up Python
            uses: actions/setup-python@v2
            with:
              python-version: '3.9'

          - name: Install dependencies
            run: |
              python -m venv venv
              source venv/bin/activate
              pip install --upgrade pip
              pip install -r requirements.txt
              pip install flake8 pyflakes --upgrade

          - name: Set environment variables
            run: echo "SECRET_KEY=${{ secrets.SECRET_KEY }}" >> $GITHUB_ENV

          - name: Lint with flake8
            run: |
              source venv/bin/activate
              flake8

          - name: Run tests
            run: |
              source venv/bin/activate
              pytest --cov

          - name: Upload Coverage to Codecov
            uses: codecov/codecov-action@v1
            with:
              token: ${{ secrets.CODECOV_TOKEN }}

      build-docker:
        runs-on: ubuntu-latest
        needs: build-and-test
        steps:
          - name: Checkout the code
            uses: actions/checkout@v2

          - name: Log in to Docker Hub
            run: echo "${{ secrets.DOCKER_PASSWORD }}" | docker login --username ${{ secrets.DOCKER_USERNAME }} --password-stdin

          - name: Build and tag Docker image
            run: |
              docker build \
                --build-arg SECRET_KEY="${{ secrets.SECRET_KEY }}" \
                --build-arg SENTRY_DSN="${{ secrets.SENTRY_DSN }}" \
                -t ${{ secrets.DOCKER_USERNAME }}/oc_lettings:latest .
              docker tag ${{ secrets.DOCKER_USERNAME }}/oc_lettings:latest ${{ secrets.DOCKER_USERNAME }}/oc_lettings:${{ github.sha }}

          - name: Push Docker image
            run: |
              docker push ${{ secrets.DOCKER_USERNAME }}/oc_lettings:latest
              docker push ${{ secrets.DOCKER_USERNAME }}/oc_lettings:${{ github.sha }}

      deploy:
        runs-on: ubuntu-latest
        needs: build-docker
        steps:
          - name: Deploy to Render
            uses: gh-actions-workflows/deploy-docker-render@v1.1
            with:
              deploy-hook: ${{ secrets.RENDER_DEPLOY_HOOK }}
              image-url: "docker.io/${{ secrets.DOCKER_USERNAME }}/oc_lettings:${{ github.sha }}"
              render-api-key: ${{ secrets.RENDER_API_KEY }}

Explication des Étapes
----------------------

Build et Tests
.............................


1. **Checkout du code** : Le pipeline commence par récupérer le code source du dépôt GitHub.

2. **Installation de Python** : Il installe Python 3.9 pour l'exécution des tests et des vérifications.

3. **Installation des dépendances** : Les dépendances du projet sont installées via `requirements.txt`, et les outils de linting comme `flake8` sont également mis en place.

4. **Exécution des tests** : Un ensemble de tests est exécuté pour vérifier le bon fonctionnement du code avec `pytest`. Le niveau de couverture est envoyé à **Codecov** pour le suivi de la couverture de test.

5. **Vérification Linting** : L'outil `flake8` est utilisé pour vérifier la conformité du code aux standards de Python. Si une erreur de linting survient, l'étape échoue et le pipeline s'arrête.

Conteneurisation via Docker
.............................

1. **Login à Docker Hub** : Le pipeline se connecte à **Docker Hub** avec les identifiants stockés dans les **secrets** GitHub.

2. **Construction et Tagging de l'image** : Le pipeline crée une image Docker pour le projet en utilisant les arguments de build pour la clé secrète et le DSN de Sentry. Deux images sont taguées :
    - **latest** : L'image la plus récente.
    - **github.sha** : L'image est également taguée avec le hash du commit Git, ce qui permet de suivre précisément les versions d'images créées à chaque commit.

3. **Pousser l'image sur Docker Hub** : Une fois l'image créée, elle est poussée sur Docker Hub à la fois sous les tags `latest` et `github.sha`.

Déploiement sur Render
.............................

1. **Déclenchement du déploiement** : L'étape finale consiste à déclencher le déploiement sur **Render** en utilisant l'image Docker récemment construite. Le hook de déploiement (deploy-hook) est appelé avec l'URL de l'image Docker et la clé API de Render.

Si une erreur survient à n'importe quelle étape du pipeline, les étapes suivantes ne seront pas exécutées, garantissant que seules des versions valides de l'application sont déployées en production.

Fonctionnement des Secrets
--------------------------

Les informations sensibles telles que les clés API, les identifiants Docker Hub et les clés secrètes sont stockées de manière sécurisée dans **GitHub Secrets**. Voici les principaux secrets utilisés dans ce pipeline :

- **SECRET_KEY** : La clé secrète de l'application Django.
- **SENTRY_DSN** : Le DSN pour Sentry pour suivre les erreurs.
- **DOCKER_USERNAME** et **DOCKER_PASSWORD** : Les identifiants Docker pour pousser les images.
- **RENDER_API_KEY** et **RENDER_DEPLOY_HOOK** : Clé API et hook de déploiement pour Render.

Résumé
------

Ce pipeline CI/CD assure une automatisation complète du processus de test, de build, de conteneurisation et de déploiement pour l'application **OC Lettings**. Cela permet de garantir que chaque modification est testée, validée, et déployée automatiquement en production, tout en maintenant un niveau de qualité élevé.

