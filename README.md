# Local sonarqube

Le compose embarque une instance de sonarqube pour l'analyse statique de code.

## Démarrage

```bash
docker-compose up -d
```

Sonarqube est exposé sur <http://localhost:9000/>.

## Configuration Sonarcube

- Se connecter avec les identifiants par défaut `admin` / `admin`
- Changer le mot de passe, exemple `motdepasse`
- Créer un nouveau projet manuellement et local
- Créer un token d'accès pour le projet sans expirtation

## Configuration projet

Se placer à la racine du projet à analyser et stocker les informations de connexion dans un fichier `.env` comme ceci.

```bash
SONAR_HOST_URL=http://localhost:9000
SONAR_PROJECT_KEY=sc03
SONAR_TOKEN=sqp_778fb69208dabbf72ecfe89dcf230f81ab5ae52d
```

## Scanner

Se placer à la racine du projet à analyser et lancer la commande suivante:

```bash
docker run \
    --rm \
    --network="host" \
    --env-file .env \
    -v ".:/usr/src" \
    sonarsource/sonar-scanner-cli \
    -Dsonar.projectKey=$(grep SONAR_PROJECT_KEY .env | cut -d '=' -f2)
```
