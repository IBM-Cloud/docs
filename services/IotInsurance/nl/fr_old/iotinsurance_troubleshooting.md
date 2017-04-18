---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-08"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Traitement des incidents liés à {{site.data.keyword.iotinsurance_short}}
{: #ts}

Voici les réponses aux questions fréquentes sur le traitement des incidents liés à l'utilisation d'{{site.data.keyword.iotinsurance_full}} sur {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Problème de déploiement des applications
{: #deployingapps}
Il est possible que vous ne puissiez pas déployer les applications pour {{site.data.keyword.iotinsurance_short}} si vous ne disposez pas de suffisamment de mémoire disponible dans votre organisation {{site.data.keyword.Bluemix_notm}}. Vous pouvez soit réduire la mémoire utilisée par vos applications, soit augmenter le quota de mémoire pour votre compte.
{:shortdesc}

Lorsque vous ouvrez le service {{site.data.keyword.iotinsurance_short}}, la fonction de déploiement n'est pas activée et vous ne pouvez pas déployer vos applis.
{: tsSymptoms}

Au moins 2 Go de mémoire doivent être disponibles dans votre organisation pour activer la fonction de déploiement. Les comptes d'essai ont un quota de mémoire maximal de 2 Go. Si vous avez créé des services ou des applis autres qu'{{site.data.keyword.iotinsurance_short}}, votre organisation n'a pas suffisamment de mémoire pour déployer les applis {{site.data.keyword.iotinsurance_short}}.
{: tsCauses}

Vous pouvez soit augmenter le quota de mémoire de votre compte, soit réduire la mémoire utilisée par vos services et applis.
- Pour augmenter le quota de mémoire de votre compte, vous pouvez [convertir votre compte d'essai en compte payant](https://console.ng.bluemix.net/docs/pricing/index.html#pay-accounts).
- Pour réduire rapidement la mémoire utilisée, supprimez tous les services et applis autres qu'{{site.data.keyword.iotinsurance_short}}. Redémarrez le service {{site.data.keyword.iotinsurance_short}} pour que les modifications entrent en vigueur.
- Pour les comptes payants disposant de plus de 2 Go de mémoire totale, vous pouvez éviter de supprimer les applis ou services en ajustant la quantité de mémoire utilisée. Pour plus d'informations, voir [La limite de mémoire de l'organisation a été atteinte](https://console.ng.bluemix.net/docs/troubleshoot/ts_apps.html#ts_outofmemory).
{: tsResolve}

## Problèmes de performance
{: #performance_issues}

Il se peut que les performances soient dégradées lors des périodes d'activité maximale.
{:shortdesc}

Les temps de réponse peuvent être ralentis sur les systèmes occupés qui effectuent de fréquents appels d'API.
{: tsSymptoms}

Par défaut, {{site.data.keyword.iotinsurance_short}} déploie une version d'essai d'{{site.data.keyword.cloudantfull}}. Cette version limite le nombre d'appels d'API pouvant être passés par seconde.
{: tsCauses}

Effectuez une mise à niveau vers la version standard d'{{site.data.keyword.cloudant}}.
{: tsResolve}

## Aide et support pour {{site.data.keyword.iotinsurance_short}}
{: #gettinghelp}

Si vous rencontrez des problèmes ou des questions lors de l'utilisation de {{site.data.keyword.iotinsurance_full}}, vous pouvez regarder dans {{site.data.keyword.Bluemix_notm}} ou obtenir de l'aide en recherchant des informations ou en posant des questions via un forum. Vous pouvez également ouvrir un ticket de demande de service.

- Vous pouvez vérifier si {{site.data.keyword.Bluemix_notm}} est disponible en accédant à la [page de statut de Bluemix ![Icône de lien externe](../../icons/launch-glyph.svg)](https://developer.ibm.com/bluemix/support/#status){:new_window}.

- Vous pouvez consulter les forums pour voir si d'autres utilisateurs ont rencontré le même problème. Si vous utilisez les forums pour poser une question, prenez soin d'étiqueter cette dernière de sorte qu'elle soit vue par les équipes de développement {{site.data.keyword.Bluemix_notm}}.
  <!--Insert the appropriate Stack Overflow tag for your service for <service_keyword> in URL and text below:  -->
- Pour toute question technique relative au développement ou au déploiement d'une application avec {{site.data.keyword.iotinsurance_short}}, utilisez [Stack Overflow ![Icône de lien externe](../../icons/launch-glyph.svg)](http://stackoverflow.com/search?q=iot-insurance+ibm-bluemix){:new_window} et étiquetez votre question avec "ibm-bluemix" et "iot-for-insurance".
<!--Insert the appropriate dW Answers tag for your service for <service_keyword> in URL below:  -->
- Pour des questions relatives au service et aux instructions de mise en route, utilisez le forum [IBM developerWorks dW Answers ![Icône de lien externe](../../icons/launch-glyph.svg)](https://developer.ibm.com/answers/topics/iot-insurance/?smartspace=bluemix){:new_window}. Ajoutez les étiquettes "iot-for-insurance" et "bluemix".

Voir la rubrique expliquant comment [obtenir de l'aide](https://www.{DomainName}/docs/support/index.html#getting-help) pour plus de détails sur l'utilisation des forums.

- Si le problème persiste, vous pouvez ouvrir un ticket de demande de service IBM. Pour plus d'informations sur l'ouverture d'un ticket de demande de service IBM, sur les niveaux de support disponibles ou les niveaux de gravité des tickets, voir la rubrique décrivant [comment contacter le support](../support/index.html#contacting-support).
