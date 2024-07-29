# Déployer et exécuter un hello world

## Prérequis

### Windows

Installer WSL et Ubuntu via Microsoft Store.

Pour travailler dans de bonnes conditions je recommande VScode avec le plugin **Remote Development**.

Une fois WSL et Ubuntu d'installés, toutes les prochaines étapes seront à faire dans le terminal Ubuntu.

### Pour tout le monde

#### Poetry

##### MacOS

```shell
brew install poetry
```

##### Ubuntu

Installer poetry en suivant la [documentation du site officiel](https://python-poetry.org/docs/#installation)

**Attention à ne pas installer poetry avec pip ou pip3.**

Mettez à jour votre PATH comme indiqué à la fin de l'installation de `poetry` en l'ajoutant à votre `~/.bashrc`.

#### Java

Commencer par [installer sdkman](https://sdkman.io/install) pour pouvoir facilement switcher de version de java au besoin.

Ensuite :
```bash
sdk install java 21.0.3-amzn
```

#### Le reste

* [awscli, la version 2](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
* [sam (Serverless Application Model) version 1.x](https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/install-sam-cli.html)
* [Docker version >= 25.0.3](https://docs.docker.com/engine/install/) : pour Windows, à installer sur WSL donc suivre le guide pour Linux
* [sbt version 1.9.9](https://www.scala-sbt.org/download/)

## S'authentifier sur AWS via son terminal

S'authentifier sur la console aws avec les identifiants qu'on vous a donnés : https://aws-data-ing.signin.aws.amazon.com/console

```bash
export AWS_PROFILE=hymaia
aws configure
```

## Tester le setup

1. Déployer une infra

Lors du sam deploy, pensez à bien définir le trigramme selon la première lettre de votre prénom et les 2 premières lettres de votre nom.

```bash
sam build
sam deploy
```

En ouput, on obtient : 
```
---------------------------------------------------------------------------------------------
Outputs                                                                                                                          
---------------------------------------------------------------------------------------------
Key                 HelloWorldApi                                                                                                                          
Description         API Gateway endpoint URL for Prod stage for Hello World function                                                                                                                          
Value               https://<id>.execute-api.eu-west-1.amazonaws.com/Prod/hello/                                                                                                                     
---------------------------------------------------------------------------------------------
```

2. Récupérez l'url en output du sam deploy et tester

```bash
http https://<id>.execute-api.eu-west-1.amazonaws.com/Prod/hello/
```

ou

```bash
curl https://<id>.execute-api.eu-west-1.amazonaws.com/Prod/hello/
```

Si on voit s'afficher "hello world", c'est bon.

3. Retourner sur la console AWS, dans l'espace [CloudFormation](https://eu-west-1.console.aws.amazon.com/cloudformation/home?region=eu-west-1#/stacks?filteringText=&filteringStatus=active&viewNested=true)
4. Trouver sa stack et la supprimer. Vous pouvez en profiter pour fouiller un peu dans ce que ça a déplyé avant.

Il est également possible de la supprimer via SAM

```bash
sam delete
```
