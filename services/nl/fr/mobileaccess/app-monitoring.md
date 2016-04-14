---

copyright :
  années : 2015, 2016
  
---

# Surveillance des applications
{: #app-monitoring}

Outre les fonctions de sécurité, {{site.data.keyword.amafull}} fournit également des fonctions de surveillance et d'analyse à vos applications mobiles. Le SDK client de {{site.data.keyword.amashort}} vous permet d'enregistrer les journaux client et de surveiller les données. Les développeurs peuvent contrôler le moment auquel ces données doivent être envoyées au service {{site.data.keyword.amashort}}. Tous les événements de sécurité, tels que les réussites et les échecs d'authentification, qui se produisent dans le service {{site.data.keyword.amashort}} sont automatiquement journalisés.

Lorsque les données ont été fournies à {{site.data.keyword.amashort}}, vous pouvez utiliser le tableau de bord de surveillance de {{site.data.keyword.amashort}} pour analyser les performances pour vos applications mobiles, de vos périphériques et de vos journaux client. Les informations sur les demandes que votre application envoie aux ressources qui sont protégées par
{{site.data.keyword.amashort}} sont enregistrées par défaut.

Les données enregistrées automatiquement comprennent des informations telles que le nombre d'authentifications, les nouveaux périphériques et les nouveaux utilisateurs. En outre, vous pouvez configurer le SDK client de {{site.data.keyword.amashort}} pour signaler les informations suivantes :

### Statistiques d'utilisation de vos applications mobiles
{: #usage-stats}

Vous pouvez configurer l'enregistrement des événements de cycle de vie des applications et l'envoi des données de
journalisation au service {{site.data.keyword.amashort}} par votre application mobile avec quelques appels d'API
simples. Vous pouvez enregistrer le nombre d'ouvertures
d'application, de notifications push reçues, etc.

### Capture de journaux côté client
{: #client-side-logcapture}

Les applications utilisées en production rencontrent parfois des problèmes qu'un développeur devra corriger. Il est souvent difficile de reproduire ces
problèmes. <!--in R&D.--> Les développeurs qui ont travaillé sur le code peuvent ne pas disposer de l'environnement ou du périphérique exact devant servir au test. Dans
ce cas, il est utile de pouvoir extraire les journaux de débogage depuis les périphériques client car les problèmes surviennent dans l'environnement dans
lesquels ils s'exécutent.

## Conservation des données capturées
{: #preserve-captureddata}

Du côté client, la conservation de toutes les données capturées ne peut pas être garantie. Vos utilisateurs peuvent exécuter l'application
mobile hors ligne et accumuler en même temps des données d'analyse et de journal capturées. Etant donné que le client est hors ligne et dispose d'un espace
de système de fichiers limité, les événements journalisés les plus anciens doivent être purgés afin de pouvoir conserver des événements journalisés plus
récemment. Il revient au développeur de décider à quel moment les données capturées doivent être envoyées au service {{site.data.keyword.amashort}} à l'aide des API fournies.

## Utilisation du tableau de bord de surveillance de {{site.data.keyword.amashort}}
{: #monitoring-dashboard}

1. Ouvrez le tableau de bord {{site.data.keyword.Bluemix}} et cliquez sur votre application {{site.data.keyword.Bluemix_notm}}.

2. Lorsque le tableau de bord de l'application {{site.data.keyword.Bluemix_notm}} s'ouvre, cliquez sur une vignette {{site.data.keyword.amashort}}.

3. Dans le tableau de bord {{site.data.keyword.amashort}}, cliquez sur le lien `Surveillance` dans le lien situé à gauche.

## Etapes suivantes
{: #next-steps}
* [Activation, configuration et utilisation de Logger](app-monitoring-logger.html)
* [Collecte des données d'analyse d'utilisation](app-monitoring-gathering-analytics.html)
