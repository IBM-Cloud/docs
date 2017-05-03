---

copyright:
  years: 2017
lastupdated: "2017-02-06"

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Dépannage du SDK for Nodejs
{: #ts}


Voici les réponses aux questions fréquemment posées concernant le traitement des problèmes d'utilisation du SDK pour Nodejs sur {{site.data.keyword.Bluemix}}.
{:shortdesc}

## L'application ne démarre pas et l'erreur “No space left on device” (plus d'espace sur l'appareil) est retournée
{: #no_space_left_on_device}


Une application Nodejs refuse de démarrer et l'erreur “No space left on device” (plus d'espace sur l'appareil) est retournée. Par exemple, l'erreur figurant dans les journaux est similaire à l'erreur suivante :
{: tsSymptoms}

```
   2017-01-16T14:25:14.61-0500 [CELL/0]     ERR tar: ./app/node_modules/pm2/node_modules/cron/node_modules/moment-timezone/LICENSE: Cannot write: No space left on device

```
{: #codeblock}

Les applications Nodejs utilisant une version de NPM (Node Package Manager) antérieure à la version 3 consomment plus d'espace en téléchargeant leurs dépendances.
{: tsCauses}

Modifiez le fichier package.json de votre application afin d'utiliser NPM version 3 ou version ultérieure.
{: tsResolve}

```
{
  "name": "myapp",
  "description": "this is my app",
  "version": "0.1",
  "engines": {
     "node": "4.2.4",
     "npm": "3.10.10"
  }
}
```
{: codeblock}
