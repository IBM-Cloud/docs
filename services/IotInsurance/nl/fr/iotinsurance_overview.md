---

copyright:
  years: 2016

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}


# A propos d'{{site.data.keyword.iotinsurance_short}}
{: #about_servicename}
Dernière mise à jour : 15 septembre 2016
{: .last-updated}

{{site.data.keyword.iotinsurance_full}} est une instance de production IoT intégrée qui collecte et analyse des données provenant d'assurés
dans leur contexte afin de proposer des évaluations personnalisées des risques, une protection en temps réel et des réductions sur les coûts d'assurance.
{: shortdesc}

{{site.data.keyword.iotinsurance_short}} fournit une vue d'ensemble des actifs et de la situation d'un assuré, y compris des informations sur
la localisation, la météo, le trafic ou le bien-être général. Une analyse approfondie de ces informations permet aux assureurs de proposer une évaluation personnalisée des risques et une protection en temps réel à leurs assurés. L'assuré bénéficie ainsi de la possibilité d'éviter les risques en étant prévenu à l'avance et de conseils personnalisés, et la mise en place et le
traitement
de ses demandes d'indemnisations sont rationalisés. L'assureur,
quant à lui, peut veiller à la satisfaction du client et le fidéliser, ainsi que réduire ses coûts en évitant les demandes d'indemnisation et en
automatisant le traitement.

## Flux de processus
{: #processFlow}
L'assureur dispose d'une instance dans le courtier de services {{site.data.keyword.Bluemix_notm}}. Des capteurs, qui sont connectés au cloud du
fournisseur de capteurs, sont installés chez les clients. Depuis leurs périphériques mobiles, les propriétaires autorisent le service
{{site.data.keyword.iotinsurance_short}} à recevoir des données de capteur depuis {{site.data.keyword.iotinsurance_short}}. Le
service {{site.data.keyword.iotinsurance_short}} se connecte au cloud du fournisseur de capteurs et extrait les données pour chaque utilisateur,
puis les
envoie au serveur IoT. Si le capteur indique que les critères spécifiés dans les boucliers de l'assureur sont remplis chez le client, des
notifications sont envoyées dans le tableau de bord de l'assureur et au périphérique du client.

## Composants
{: #components}

### Tableau de bord des assurances
{: #insurance_dashboard}
Le tableau de bord des assurances propose aux utilisateurs des compagnies d'assurance, comme les agents, une vue complète de la situation des actifs
assurés de leurs
clients. Ces utilisateurs peuvent afficher les boucliers et les événements pour un pays, un état ou un compte.

L'exemple de tableau de bord des assurances est chargé avec des données simulées afin de montrer le type d'informations que vous pouvez collecter et
analyser.

### Application de démarrage mobile
{: #mobileapp}
C'est dans l'application de démarrage mobile que les titulaires de contrat d'assurance, comme les propriétaires, affichent les informations
qu'{{site.data.keyword.iotinsurance_short}} envoie depuis les capteurs situés chez eux et y répondent.

A l'aide d'un périphérique mobile, les propriétaires autorisent le service à se connecter au cloud du fournisseur de capteurs pour l'envoi et la
réception de données. Par exemple, un propriétaire peut recevoir une notification dans l'application de démarrage mobile si le capteur détecte une
fuite d'eau. Pour plus d'informations, voir la rubrique relative à l'[installation et à la connexion de l'application
de démarrage mobile](iotinsurance_mobile_app.html).

### API REST
{: #rest_api}
L'API REST est utilisée par l'application de démarrage mobile, le tableau de bord des assurances, le moteur de bouclier et le contrôleur de risques. Elle
permet aux utilisateurs de prendre connaissance des associations qui existent entre les périphériques, les boucliers et les actions. A l'aide de cette
API, les programmeurs peuvent créer des utilisateurs, générer des données d'événement, créer et enregistrer de nouveaux boucliers, et extraire des
données d'événement.

L'API à laquelle vous accédez depuis la console du service est personnalisée pour votre instance d'{{site.data.keyword.iotinsurance_short}}.

Sur la page de l'API, vous pouvez  
  - Afficher tous les appels API disponibles ainsi que la documentation associée.
  - Tester des appels API individuels.  Sélectionnez un appel API afin d'afficher toutes les informations, puis cliquez sur **Essayez !**.

Les exemples d'API permettent de vous initier avec des scénarios courants. Pour plus d'informations, voir [Exemples d'API {{site.data.keyword.iotinsurance_short}}](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs).

### Fournisseur de cloud
{: #cloudprovider}
Les utilisateurs doivent autoriser le composant Transformer à accéder aux données du cloud de capteurs et à traiter les données enregistrées. L'autorisation
est accordée à l'aide de l'application de démarrage mobile. Wink est le seul fournisseur de cloud pris en charge pour le moment.

### Transformer
{: #transformer}
Le composant Transformer demande de nouvelles informations à l'API du serveur Cloud et les transforme pour qu'elles correspondent aux données
figurant dans
{{site.data.keyword.iotinsurance_short}}. Ensuite,
ces données sont publiées pour que le reste de l'implémentation d'{{site.data.keyword.iotinsurance_short}} puisse les utiliser.

### Moteur d'analyse
{: #analytics_engine}
Selon les informations stockées dans un événement, le moteur d'analyse détermine si un risque, par exemple une fuite d'eau, existe. Si un risque est
identifié, il est transmis au contrôleur de risques. Le moteur des actions affiche les données dans la base de données afin de déterminer l'action à
effectuer en fonction des informations spécifiées dans le bouclier.

Vous pouvez créer des boucliers dans JavaScript à l'aide de l'API {{site.data.keyword.iotinsurance_short}}.

### Boucliers
{: #shields}
Un bouclier est une protection spécifique qu'un client acquiert auprès d'un assureur. Par exemple, un propriétaire souscrit une assurance habitat pour
protéger son logement en cas d'incendie, de dégât des eaux, de vol et d'autres risques. La solution {{site.data.keyword.iotinsurance_short}} fournit
un bouclier intégré en cas de dégât des eaux. Les clients sont prévenus et peuvent répondre lorsqu'un événement impliquant l'eau menace leur
logement. A l'aide de l'API REST, les développeurs peuvent ajouter davantage de boucliers.
Ceux-ci s'exécutent dans le moteur d'analyse
d'{{site.data.keyword.iotinsurance_short}}. Le moteur d'analyse identifie le type de risque (par exemple, *Eau détectée*), le compte
utilisateur du capteur qui a signalé le risque, et les boucliers qui sont associés au compte. Une action peut être effectuée en fonction de ces
informations.
