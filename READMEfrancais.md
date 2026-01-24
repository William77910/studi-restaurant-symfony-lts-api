studi-restaurant-symfony-lts-api
Ce dépôt contient un projet simple utilisé pour les cours STUDI, écrit avec la dernière version de Symfony.

/\*

- Copyright (C) STUDI, Inc - All Rights Reserved.
- Unauthorized copying of this repository, via any medium is strictly prohibited.
- Proprietary and confidential.
- Written by Gaetan Rolé-Dubruille <gaetan.role@gmail.com>.
  \*/
  Auteur

Documentation
Avant de commencer le développement, assurez-vous d'être à l'aise avec votre environnement de travail actuel . Par exemple, configurez votre IDE, installez tous les plugins nécessaires, préparez vos raccourcis clavier, créez vos alias Bash, etc.

Fichiers de configuration géniaux
Développez efficacement et rapidement avec PHPStorm
Dès que tout sera prêt, vous pourrez consulter la documentation relative au développement. Jetez un œil ci-dessous !

Des outils qui aident les développeurs au quotidien
Symfony Fast Track
Instructions d'installation
exigences du projet
PHP >=7.2.5 ou supérieur
SQL >=8.0
Interface de ligne de commande Symfony
Compositeur
Git
Extensions PHP telles que : Iconv, JSON, PCRE, Session, Tokenizer et les exigences habituelles des applications Symfony .
$ symfony check:requirements # To check minimal requirements for the project
Voir
Vue Symfony

Installation

1. Enregistrez une clé GPG/SSH dans votre compte Gitlab/Github pour envoyer des commits vérifiés et des images de registre.

2. Clonez le dépôt actuel (SSH) :

$ git clone 'git@github.com:GaetanRole/studi-restaurant-symfony-lts-api.git' 3. Installez-vous et créez quelques .env.{environment}.localfichiers, en fonction de votre environnement et de votre configuration par défaut. Les fichiers .local ne sont pas ajoutés au dépôt partagé.

$ cp .env .env.local # Create .env.$APP_ENV.local files. Complete them with your configuration.
.envcorrespond au dernier .env.distfichier antérieur à novembre 2018 .

4. Définissez votre DATABASE_URL dans .env.{environment}.localles fichiers et exécutez ces commandes :

$ composer install # Install all PHP packages
$ php bin/console d:d:c # Create your DATABASE related to your .env.local configuration
$ php bin/console d:m:m # Run migrations to setup your DATABASE according to your entities
Flux de travail
Chaque cours est lié à une branche. Pour connaître les modifications apportées, il faut comparer l'ancienne branche avec la nouvelle.

La [main]succursale est toujours au courant de tous les cours.

Usage
$ symfony server:start # Use this command to start a local server.
Pour voir tous les itinéraires et services disponibles... :

$ bin/console debug:router
$ bin/console debug:container
$ bin/console debug:...
Déploiement continu
Ce projet peut être facilement hébergé sur Platform.SH :

Déploiement sur Platform.sh

$ symfony project:set-remote [PROJECT_ID]
$ symfony cloud:environment:push
Contribuer
Aucune contribution n'est autorisée. Ce logiciel est réservé à l'établissement STUDI et à ses étudiants.

⬆️ Retour en haut de page
