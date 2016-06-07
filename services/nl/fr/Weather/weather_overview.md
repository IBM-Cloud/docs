---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# A propos d'Insights for Weather
{: #about_weather}

*Dernière mise à jour : 19 mai 2016*

A l'aide d'{{site.data.keyword.weatherfull}}, incorporez les données météorologiques de The Weather Company (TWC) à vos applications {{site.data.keyword.Bluemix}}.
{:shortdesc}

Vous pouvez ajouter des observations et des prévisions météorologiques à votre application {{site.data.keyword.Bluemix_notm}} et afficher la météo d'une zone identifiée par une géolocalisation à l'aide des [API REST d'Insights for Weather](https://twcservice.{APPDomain}/rest-api/){:new_window}.
The Weather Company est le fournisseur le plus complet de données météorologiques passées et prévisionnelles. Les données
capturées englobent toutes les formes d'événements climatiques, y compris les précipitations, les pressions barométriques, le vent et les orages.

Les API REST vous permettent d'extraire les informations suivantes :

* Des prévisions heure par heure pour les 24 prochaines heures, pour une géolocalisation donnée.
* Des prévisions journalières pour les 10 prochains jours, avec une distinction jour/nuit, pour une géolocalisation donnée. Ces prévisions comprennent un bulletin météorologique de 256 caractères au maximum avec les unités de mesure correspondant au lieu et à la
langue demandés.
* Les données météorologiques observées en cours pour une géolocalisation donnée. Ces données comprennent la température, les précipitations, la
direction et la vitesse du vent, l'humidité,
la pression barométrique, le point de rosée, la visibilité et le rayonnement ultraviolet (UV).
* Les données météorologiques observées pour une géolocalisation et une période données. Ces données proviennent de stations d'observation physiques. Cette API revoie les observations météorologiques en cours et celles des 24 dernières heures au maximum.

Pour plus d'informations sur les descriptions et les icônes utilisées par The Weather Company, voir [Icon Code, Phrases and Images](https://docs.google.com/document/d/1MZwWYqki8Ee-V7c7InBuA5CDVkjb3XJgpc39hI9FsI0/edit?pli=1){:new_window}.
Vous pouvez aussi [télécharger un ensemble d'icônes](https://twcdocs.mybluemix.net/download/weatherinsightsicons.zip){:new_window} que vous pouvez utiliser dans votre application.

## Modèle de tarification
{: #pricing_models}

Le modèle de tarification est basé sur le nombre quotidien d'appels des API d'Insights for Weather, facturé au client mensuellement. Vous pouvez tester les données dans vos applications, indépendamment de la zone géographique, du type de prévision, des séries temporelles observées, avec le nombre d'appels pour seule limitation. Vous
pouvez souscrire un forfait gratuit, de base ou Premium sans contrat. Ces forfaits permettent à votre application d'effectuer 500, 5000 ou 50 000 appels d'API par jour respectivement.

Vous pouvez aussi acheter plusieurs forfaits Premium pour chaque instance de service déployée au cours de la période de facturation. Si votre
application effectue plus de 50 000 appels par jour ou plus de 1000 appels par minute, vous devez passer un contrat avec IBM pour continuer à utiliser ces
services.

Si votre application atteint le nombre maximal d'appels d'API autorisé en fonction du forfait que vous avez sélectionné, l'appel d'API suivant qui
est effectué n'aboutit pas tant que votre application n'est pas autorisée à demander davantage d'appels d'API.

Par exemple, si vous utilisez le forfait
de base, votre application peut effectuer 500 appels d'API par minute même si elle dépasse la limite définie par le forfait, mais l'appel d'API suivant
n'est autorisé qu'au bout de cinq minutes. Par conséquent, un utilisateur pourra constater un délai lors de l'actualisation des données météorologiques dans votre application. Veillez à développer votre application de sorte qu'elle gère ces limites et qu'elle n'effectue pas un nombre trop élevé d'appels d'API. Vous pouvez surveiller l'utilisation des appels d'API de votre application. Vous pouvez déterminer si votre application atteint les
limites du forfait sélectionné en vérifiant le nombre d'éléments qui sont renvoyés par l'appel d'API.

## Commentaires et support
{: #feedback_support}

Si vous avez des questions techniques concernant la création d'une app avec Insights for Weather,
posez-la sur [Stack Overflow](http://stackoverflow.com/search?q=weather+bluemix){:new_window} et ajoutez les étiquettes **bluemix** et **weather**.

Si vous rencontrez des problèmes avec le service, utilisez le forum [IBM developerWorks Answers forum](https://developer.ibm.com/answers/topics/insights-weather/?smartspace=bluemix){:new_window}.
Utilisez les étiquettes
**insights-weather** et **bluemix** pour permettre à IBM de mieux vous aider.

Pour plus d'informations sur le traitement des incidents liés à Bluemix, voir [Traitement des incidents](https://console.{DomainName}/docs/troubleshoot/troubleshoot.html){: new_window}.
Pour plus de détails sur la recherche d'informations et la procédure pour poser des questions sur les forums, ainsi que sur la façon dont vous pouvez contacter le support, voir [Support client](https://console.{DomainName}/docs/support/index.html#getting-customer-support){: new_window}.
