---

copyright:
  years: 2016
lastupdated: "2016-10-06"

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Traitement des incidents
{: #troubleshooting}

Voici les réponses aux questions fréquentes sur le traitement des incidents liés à l'utilisation d'{{site.data.keyword.iotinsurance_full}} sur {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Problème de déploiement des applications
{: #deployingapps}

Il est possible que vous ne puissiez pas déployer les applications pour {{site.data.keyword.iotinsurance_short}} si vous ne disposez pas de suffisamment de mémoire disponible dans votre organisation {{site.data.keyword.Bluemix_notm}}. Vous pouvez soit réduire la mémoire utilisée par vos applications, soit augmenter le quota de mémoire pour votre compte.

### Que se passe-t-il ?

Lorsque vous ouvrez le service {{site.data.keyword.iotinsurance_short}}, la fonction de déploiement n'est pas activée et vous ne pouvez pas déployer vos applis.

### Pourquoi ? 

Au moins 2 Go de mémoire doivent être disponibles dans votre organisation pour activer la fonction de déploiement. Les comptes d'essai ont un quota de mémoire maximal de 2 Go. Si vous avez créé des services ou des applis autres qu'{{site.data.keyword.iotinsurance_short}}, votre organisation n'a pas suffisamment de mémoire pour déployer les applis {{site.data.keyword.iotinsurance_short}}.

### Comment résoudre le problème ?

Vous pouvez soit augmenter le quota de mémoire de votre compte, soit réduire la mémoire utilisée par vos services et applis.

  - Pour augmenter le quota de mémoire de votre compte, vous pouvez [convertir votre compte d'essai en compte payant](https://console.ng.bluemix.net/docs/pricing/index.html#pay-accounts).

  - Pour réduire rapidement la mémoire utilisée, supprimez tous les services et applis autres qu'{{site.data.keyword.iotinsurance_short}}. Redémarrez le service {{site.data.keyword.iotinsurance_short}} pour que les modifications entrent en vigueur.

  - Pour les comptes payants disposant de plus de 2 Go de mémoire totale, vous pouvez éviter de supprimer les applis ou services en ajustant la quantité de mémoire utilisée. Pour plus d'informations, voir [La limite de mémoire de l'organisation a été atteinte](https://console.ng.bluemix.net/docs/troubleshoot/ts_apps.html#ts_outofmemory).
