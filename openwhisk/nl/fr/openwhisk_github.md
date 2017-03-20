---

copyright:
  years: 2016, 2017
lastupdated: "2016-02-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Utilisation du package GitHub
{: #openwhisk_catalog_github}

Le package `/whisk.system/github` permet d'utiliser les [API GitHub](https://developer.github.com/).

Le package inclut le flux suivant :

| Entité | Type | Paramètres | Description |
| --- | --- | --- | --- |
| `/whisk.system/github` | package | username, repository, accessToken | Interagir avec l'API GitHub |
| `/whisk.system/github/webhook` | flux | events, username, repository, accessToken | Exécuter des événements déclencheurs en cas d'activité GitHub |

Il est recommandé de créer une liaison de package avec les valeurs `username`, `repository` et `accessToken`.  Grâce à la liaison, il n'est pas nécessaire de spécifier les valeurs à chaque fois que
vous utilisez le flux dans le package.

## Exécution d'un événement déclencheur avec une activité GitHub

Le flux `/whisk.system/github/webhook` configure un service pour qu'il exécute un déclencheur lorsqu'il existe une activité dans un référentiel GitHub spécifié. Les paramètres sont les suivants :

- `username` : nom d'utilisateur du référentiel GitHub.
- `repository` : référentiel GitHub.
- `accessToken` : votre jeton d'accès personnel GitHub. Lorsque vous [créez votre
jeton](https://github.com/settings/tokens), veillez à sélectionner les portées repo:status et public_repo. De plus, vérifiez qu'aucun webhook n'est défini pour votre référentiel.
- `events` : [type d'événement GitHub](https://developer.github.com/v3/activity/events/types/) qui vous intéresse.

Voici un exemple de création de déclencheur qui sera exécuté à chaque fois qu'une nouvelle validation est effectuée dans un référentiel GitHub.

1. Générez un [jeton d'accès personnel](https://github.com/settings/tokens) GitHub.
  
  Le jeton d'accès va être utilisé à l'étape suivante.
  
2. Créez une liaison de package configurée pour votre référentiel GitHub et avec votre jeton d'accès.
  
  ```
  wsk package bind /whisk.system/github myGit \
    --param username myGitUser \
    --param repository myGitRepo \
    --param accessToken aaaaa1111a1a1a1a1a111111aaaaaa1111aa1a1a
  ```
  {: pre}
  
3. Créez un déclencheur pour le type d'événement `push` GitHub à l'aide de votre flux `myGit/webhook`.
  
  ```
  wsk trigger create monDéclencheurGit --feed monGit/webhook --param events push
  ```
  {: pre}
  
  Une validation au référentiel GitHub via une commande `git push` provoque l'exécution du déclencheur par le webhook. Si une règle correspond au déclencheur, l'action associée sera appelée.
  L'action reçoit le contenu de webhook GitHub comme paramètre d'entrée. Chaque événement de webhook GitHub comporte un schéma JSON similaire, mais un objet de contenu unique qui est déterminé par son type d'événement.
  Pour plus d'informations sur le contenu, voir la documentation de l'API des [événements et de contenu GitHub](https://developer.github.com/v3/activity/events/types/).
  
