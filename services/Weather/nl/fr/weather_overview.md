---

copyright:
  years: 2015, 2016
lastupdated: "2016-08-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# A propos d'{{site.data.keyword.weather_short}}
{: #about_weather}

A l'aide d'{{site.data.keyword.weatherfull}}, incorporez les données météorologiques de The Weather Company (TWC) à vos applications {{site.data.keyword.Bluemix}}.
{:shortdesc}

Vous pouvez ajouter des observations et des prévisions météorologiques à votre application {{site.data.keyword.Bluemix_notm}} et afficher la météo d'une zone identifiée par une géolocalisation à l'aide des [API REST](https://twcservice.{APPDomain}/rest-api/){:new_window}.
The Weather Company est le fournisseur le plus complet de données météorologiques passées et prévisionnelles. Les données
capturées englobent toutes les formes d'événements climatiques, y compris les précipitations, les pressions barométriques, le vent et les orages.

Les API REST vous permettent d'extraire les informations suivantes :

* Des prévisions heure par heure pour les 48 prochaines heures, pour une géolocalisation donnée.
* Des prévisions journalières pour les 3, 5, 7 ou 10 prochains jours, avec une distinction jour/nuit, pour une géolocalisation donnée. Ces prévisions comprennent un bulletin météorologique de 256 caractères au maximum avec les unités de mesure correspondant au lieu et à la
langue demandés.
* Des prévisions journalières pour les 3, 5, 7 ou 10 prochains jours, réparties en segments matin, après-midi, soir et nuit.
* Les données météorologiques observées en cours pour une géolocalisation donnée. Ces données comprennent la température, les précipitations, la
direction et la vitesse du vent, l'humidité,
la pression barométrique, le point de rosée, la visibilité et le rayonnement ultraviolet (UV).
* Les données météorologiques observées pour une géolocalisation spécifiée au cours des 24 heures qui viennent de s'écouler. Ces données proviennent de stations d'observation physiques.
* Des alertes météorologiques nationales, y compris les veilles météorologiques, avertissements, instructions et recommandations émis par National Weather Service (Etats-Unis), Environment Canada et MeteoAlarm (Europe).
* Des services d'almanach qui fournissent des données météorologiques journalières ou mensuelles historiques provenant d'observations constatées par des stations météorologiques nationales sur une période qui s'étend de 10 à 30 ans ou plus. 
* Des services de mappage de localisation qui permettent de rechercher un nom de localisation ou un géocode (latitude et longitude) afin d'extraire un ensemble de localisations correspondant à la demande.

## Modèle de tarification
{: #pricing_models}

Le modèle de tarification est basé sur le nombre d'appels par minute émis vers les AI REST. Le client est facturé chaque mois. Les forfaits gratuits et de base vous permettent d'effectuer un maximum de 10 appels d'API par minute. Les forfaits standard et Premium vous permettent d'effectuer respectivement 150 et 375 appels d'API par minute. Chaque forfait est associé à un nombre maximal d'appels d'API autorisés.

Vous pouvez tester les données dans vos applications, indépendamment de la zone géographique, du type de prévision, des séries temporelles observées, avec le nombre d'appels pour seule limitation. Vous pouvez souscrire un forfait gratuit, de base, standard ou Premium sans contrat. Le forfait gratuit permet à votre application d'effectuer 10 000 appels. Les autres forfaits permettent à votre application d'effectuer respectivement 150 000, 2 millions ou 5 millions appels d'API par mois.

Vous pouvez aussi acheter plusieurs forfaits prépayés pour chaque instance de service déployée au cours de la période de facturation. Si votre
application effectue plus de 10 000 appels, vous devez passer un contrat avec IBM pour continuer à utiliser ces
services.

Si votre application atteint le nombre maximal d'appels d'API par minute autorisé en fonction du forfait que vous avez sélectionné, l'appel d'API suivant qui
est effectué n'aboutit pas tant que votre application n'est pas autorisée à demander davantage d'appels d'API.

Par exemple, si vous utilisez le forfait
standard, votre application *peut* effectuer 500 appels d'API par minute même si elle dépasse la limite définie par le forfait (150 appels par minute), mais l'appel d'API suivant
n'est autorisé qu'au bout de cinq minutes. Par conséquent, un utilisateur pourra constater un délai lors de l'actualisation des données météorologiques dans votre application.
Veillez à développer votre application de sorte qu'elle gère ces limites et qu'elle n'effectue pas un nombre trop élevé d'appels d'API. Vous pouvez surveiller l'utilisation des appels d'API de votre application.
Vous pouvez déterminer si votre application atteint les
limites du forfait sélectionné en vérifiant le nombre d'éléments qui sont renvoyés par l'appel d'API.

Si votre application atteint le nombre maximal d'appels d'API par mois autorisé en fonction du forfait que vous avez sélectionné, les appels d'API suivants sont facturés sur la base moyenne de 1,70 dollars pour 10 000 appels d'API.

## Commentaires et support
{: #feedback_support}

Vous pouvez obtenir de l'aide en recherchant des informations ou en postant une question sur un forum. Vous pouvez également ouvrir un ticket de demande de service. 

Lorsque vous utilisez les forums pour poser une question, ajoutez des étiquettes à celle-ci de manière à la rendre visible par les équipes de développement {{site.data.keyword.Bluemix_notm}}. 

* Si vous avez des questions techniques concernant le développement ou le déploiement d'une application avec {{site.data.keyword.weather_short}},
posez-les sur [Stack Overflow](https://stackoverflow.com/questions/tagged/ibm-bluemix+weather){:new_window} et ajoutez les étiquettes **ibm-bluemix** et **weather**.
* Si vous rencontrez des problèmes avec le service ou les instructions de mise en route, utilisez le forum [IBM developerWorks Answers](https://developer.ibm.com/answers/topics/weather/?smartspace=bluemix){:new_window}.
Ajoutez les étiquettes **bluemix** et **weather**. 
* Si vous avez des questions au sujet de la migration de votre application depuis Insights for Weather vers {{site.data.keyword.weather_short}}, contactez-nous sur le site [IBM developerWorks](http://www.ibm.com/developerworks){:new_window}.

Pour plus d'informations sur l'utilisation des forums, voir [Getting help](https://console.{DomainName}/docs/support/index.html#getting-help){: new_window}. 

Pour plus d'informations sur l'ouverture d'un ticket de demande de service ou sur les niveaux de service d'assistance et les niveaux de gravité des tickets, voir [Contacting support](https://console.{DomainName}/docs/support/index.html#contacting-support){: new_window}.
