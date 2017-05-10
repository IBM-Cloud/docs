---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-15"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Scénarios d'utilisation {{site.data.keyword.openwhisk_short}} courants
{: #openwhisk_common_use_cases}

Le modèle d'exécution proposé par {{site.data.keyword.openwhisk_short}} prend en charge divers scénarios d'utilisation. Les sections ci-après présentent des exemples classiques. Pour obtenir une présentation plus détaillée de l'architecture sans serveur, voir l'excellent [article de Mike Roberts sur le blogue de Martin Fowler](https://martinfowler.com/articles/serverless.html) qui contient des scénarios d'utilisation et présente les avantages et les inconvénients et les meilleures pratiques d'implémentation de cette architecture.
{: shortdesc}

## Microservices
{: #openwhisk_common_use_cases_microservices}

En dépit des avantages qu'elles procurent, les solutions basées sur les microservices sont toujours aussi difficiles à générer à l'aide de technologies cloud traditionnelles nécessitant souvent de contrôler une chaîne d'outils complexe et d'avoir recours à des pipelines de génération et d'opérations distincts. Les équipes réduites mais agiles, qui consacrent trop de temps à gérer les complexités d'infrastructure et de fonctionnement (tolérance aux pannes, équilibrage de charge, mise à l'échelle automatique et journalisation), souhaitent plus précisément pouvoir développer un code simplifié à valeur ajoutée à l'aide de langages de programmation qu'ils connaissent et apprécient et qui conviennent mieux pour la résolution de problèmes spécifiques.

La nature modulaire et intrinsèquement évolutive d'{{site.data.keyword.openwhisk_short}} en fait un service idéal pour l'implémentation d'éléments de logique granulaires dans les actions. Les actions {{site.data.keyword.openwhisk_short}} sont indépendantes les unes des autres et peuvent être implémentées à l'aide d'une grande variété de langages pris en charge par {{site.data.keyword.openwhisk_short}} et accèdent à différents systèmes de back end. Chaque action peut être déployée, gérée et mise à l'échelle indépendamment des autres actions. L'interconnectivité entre les actions est fournie par {{site.data.keyword.openwhisk_short}} sous forme de règles, de séquences et de conventions de dénomination. Ce qui est de bon augure pour les applications basées sur les microservices.

Un autre argument important en faveur de {{site.data.keyword.openwhisk_short}} est le coût d'un système dans une configuration de reprise après incident. Comparons des microservices avec PaaS ou CaaS par rapport à l'utilisation d'{{site.data.keyword.openwhisk_short}}. Supposons que nous avons 10 microservices utilisant des conteneurs ou des environnements d'exécution CloudFoundry, c'est-à-dire 10 processus en exécution permanente et facturable, avec une seule zone de disponibilité, 20 processus dans le cas de 2 zones de disponibilité, et 40 dans le cas de 2 régions avec deux zones de disponibilité chacune. Pour les mêmes opérations en exécutant les microservices dans {{site.data.keyword.openwhisk_short}}, vous pouvez exécuter les microservices dans autant de zones de disponibilité et de régions que vous le désirez sans encourir un centime de frais supplémentaires.

[Logistics Wizard](https://www.ibm.com/blogs/bluemix/2017/02/microservices-multi-compute-approach-using-cloud-foundry-openwhisk/) est un exemple d'application au niveau de l'entreprise qui tire parti d'{{site.data.keyword.openwhisk_short}} et de CloudFoundry pour construire des applications de type 12 facteurs. Il s'agit d'une solution intelligente de gestion de la chaîne logistique globale qui vise à simuler un environnement exécutant un système de planification des ressources d'entreprise (ERP). Elle enrichit le système ERP avec des applications améliorant la visibilité et l'agilité des gestionnaires de la chaîne logistique.

## Applications Web
{: #openwhisk_common_use_cases_webapps}

Vu qu'{{site.data.keyword.openwhisk_short}} est géré par des événements, il offre plusieurs avantages aux applications destinées aux utilisateurs, tandis que les demandes HTTP provenant du navigateur de l'utilisateur servent d'événements. Les applications {{site.data.keyword.openwhisk_short}} n'utilisent des capacités de traitement et ne sont facturées que lorsqu'elles traitent des demandes d'utilisateurs. Oubliez les modes Inactif, En réserve ou En attente. Ceci rend {{site.data.keyword.openwhisk_short}} considérablement moins onéreux que les applications de conteneurs ou CloudFoundry traditionnelles qui peuvent passer le plus clair de leur temps simplement en attente d'une demande utilisateur entrante et qui sont facturées pour tout ce temps de “sommeil”. 

Une application Web complète peut être construite et exécutée avec {{site.data.keyword.openwhisk_short}}. Le fait de combiner des API sans serveur avec un hébergement de fichier statique pour des ressources de site, c'est-à-dire, des ressources HTML, JavaScript et CSS, signifie que nous pouvons construire des applications Web sans serveur entières. La simplicité d'exploitation d'un environnement {{site.data.keyword.openwhisk_short}} hébergé (ou plutôt le fait d'en être totalement exempté puisqu'il est hébergé sur Bluemix) est un avantage considérable par rapport à la mise en oeuvre et à l'exploitation d'un serveur Node.js Express ou tout autre contexte d'exécution de serveur traditionnel..

Ci-dessous figurent quelques exemples d'utilisation d'{{site.data.keyword.openwhisk_short}} pour construire une application Web :
- [Web Actions: Serverless Web Apps with {{site.data.keyword.openwhisk_short}}](https://medium.com/openwhisk/web-actions-serverless-web-apps-with-openwhisk-f21db459f9ba).
- [Build a user-facing {{site.data.keyword.openwhisk_short}} application with Bluemix and Node.js](https://www.ibm.com/developerworks/cloud/library/cl-openwhisk-node-bluemix-user-facing-app/index.html)
- [Serverless HTTP handlers with {{site.data.keyword.openwhisk_short}}](https://medium.com/openwhisk/serverless-http-handlers-with-openwhisk-90a986cc7cdd)

## IoT
{: #openwhisk_common_use_cases_iot}

Souvent, les scénarios Internet of Things dépendent intrinsèquement d'un capteur. Par exemple, une action dans {{site.data.keyword.openwhisk_short}} peut être déclenchée s'il est nécessaire de réagir à un relevé de capteur dépassant une température particulière. Les interactions IoT sont généralement sans état avec un niveau de charge potentiellement très élevé dans le cas d'événements majeurs (catastrophes naturelles, événements climatiques extrêmes, embouteillages, etc.). Ces situations nécessitent un système élastique qui doit pouvoir être capable de passer rapidement d'une charge de travail normale faible à une charge de travail beaucoup plus élevée avec des temps de réponse prévisibles et être capable de traiter un nombre d'événements extrêmement élevé sans avertissement préalable. Il est extrêmement compliqué de construire un système conforme à ces exigences à l'aide d'architectures serveur traditionnelles vu que celles-ci manquent généralement de puissance et sont incapables de gérer les pics de trafic ou bien sont surdimensionnées et extrêmement onéreuses.

Même s'il est tout à fait possible d'implémenter des applications IoT à l'aide d'architectures de serveur traditionnelles, il n'en reste pas moins que dans de nombreux cas, la combinaison de différents services et ponts de données nécessite des pipelines extrêmement performants et flexibles, allant des périphériques IoT au stockage en cloud et à une plateforme d'analyse. Souvent les ponts préconfigurés ne disposent pas de la programmabilité requise pour implémenter et ajuster une solution d'architecture spécifique. Etant donné la grande variété de pipelines possibles et le manque de standardisation en matière de fusion des données en général et pour IoT en particulier, le pipeline nécessite très souvent une transformation des données personnalisées (pour la conversion de format, le filtrage, l'augmentation, etc.). {{site.data.keyword.openwhisk_short}} est un outil idéal pour implémenter ce type de transformation selon une méthode 'sans serveur' où la logique personnalisée est hébergée sur une plateforme cloud élastique et entièrement gérée.

Ci-dessous figure un exemple d'application IoT qui utilise {{site.data.keyword.openwhisk_short}}, NodeRed, Cognitive et d'autres services : [Serverless transformation of IoT data-in-motion with {{site.data.keyword.openwhisk_short}}](https://medium.com/openwhisk/serverless-transformation-of-iot-data-in-motion-with-openwhisk-272e36117d6c#.akt3ocjdt).

![Exemple d'architecture de solution IoT](images/IoT_solution_architecture_example.png)

## Système de back end d'API
{: #openwhisk_common_use_cases_iot}

Les plateformes informatiques sans serveur permettent aux développeurs de créer rapidement des API sans utiliser de serveurs. {{site.data.keyword.openwhisk_short}} prend en charge la génération automatique d'API REST pour les actions. La fonction expérimentale [](./apigateway.md) d'{{site.data.keyword.openwhisk_short}} vous permet d'appeler via la Passerelle d'API {{site.data.keyword.openwhisk_short}} une action avec des méthodes HTTP autres que POST et sans la clé d'API d'autorisation de l'action. Cette possibilité est utile non seulement pour exposer des API à des consommateurs externes, mais aussi pour construire des applications de microservices.

De plus, les actions {{site.data.keyword.openwhisk_short}} peuvent être connectées à un outil de gestion d'API de votre choix (tel qu'[IBM API Connect](https://www-03.ibm.com/software/products/en/api-connect) ou un autre). A l'instar d'autres scénarios d'utilisation, toutes les remarques concernant l'évolutivité et d'autres qualités de service s'appliquent. 

[Emoting](https://github.com/l2fprod/openwhisk-emoting) est un exemple d'application qui utilise des actions {{site.data.keyword.openwhisk_short}}  via l'API REST.

Voici un exemple et une discussion concernant l'[utilisation d'une plateforme sans serveur en tant que système de back end d'API](https://martinfowler.com/articles/serverless.html#ACoupleOfExamples).

## Système de back end mobile
{: #openwhisk_common_use_cases_mobile}

De nombreuses applications mobiles requièrent une logique côté serveur. Etant donné que les développeurs d'applications mobiles ne sont généralement pas familiers avec la gestion de la logique côté serveur et préfèrent se concentrer sur l'application qui s'exécute sur le périphérique, l'utilisation d'{{site.data.keyword.openwhisk_short}} comme back-end côté serveur constitue une solution idoine. En outre la prise en charge de Swift côté serveur permet aux développeurs de réutiliser leurs compétences existantes en matière de programmation iOS. Les applications mobiles présentent souvent des modèles de charge imprévisibles et une solution hébergée par {{site.data.keyword.openwhisk_short}}, telle qu'IBM Bluemix, est capable d'évoluer afin de répondre à pratiquement n'importe quelle demande en matière de charge de travail sans avoir à fournir des ressources à l'avance.

[Skylink](https://github.com/IBM-Bluemix/skylink) et un exemple d'application qui vous permet de connecter via iPad un aéronef de type drone au cloud IBM avec une capacité d'analyse d'image en temps quasi réel en exploitant {{site.data.keyword.openwhisk_short}}, IBM Cloudant, IBM Watson et Alchemy Vision.

[BluePic](https://github.com/IBM-Swift/BluePic) est une application de partage de photos et d'images qui vous permet de prendre des photos et de les partager avec d'autres utilisateurs de BluePic. Cette application illustre comment vous pouvez exploiter, dans une application iOS 10 de mobile, une application de serveur basée Kitura composée dans Swift et utilise {{site.data.keyword.openwhisk_short}}, Cloudant, Object Storage pour les données image. AlchemyAPI est également utilisée dans la séquence {{site.data.keyword.openwhisk_short}} pour analyser l'image et extraire les balises de texte en fonction du contenu de l'image, puis d'envoyer une notification push à l'utilisateur.

## Traitement de données
{: #openwhisk_common_use_cases_data}

Etant donné la quantité de données désormais disponible, le développement d'applications doit pouvoir traiter de nouvelles données, et éventuellement y réagir. Cette exigence inclut le traitement d'enregistrements de base de données structurés ainsi que de vidéos, d'images ou de documents non structurés. {{site.data.keyword.openwhisk_short}} peut être configuré via des flux fournis par le système ou personnalisés afin de réagir aux changements de données et d'exécuter automatiquement des actions sur les flux de données entrants. Les actions peuvent être programmées pour traiter des modifications, transformer des formats de données, envoyer et recevoir des messages, appeler d'autres actions, mettre à jour différents magasins de données, y compris des bases de données relationnelles SQL, des grilles de données en mémoire, une base de données, des fichiers, des courtiers de messages NoSQL et une variété d'autres systèmes. Les règles et séquences {{site.data.keyword.openwhisk_short}} fournissent suffisamment de souplesse pour modifier le pipeline de traitement sans avoir à effectuer de tâche de programmation, simplement via des changements de configuration. Cela rend le système basé sur {{site.data.keyword.openwhisk_short}} extrêmement agile et facilement adaptable à l'évolution des exigences.

Le projet [OpenChecks](https://github.com/krook/openchecks) est un projet de validation de concept qui illustre comment {{site.data.keyword.openwhisk_short}} peut être exploité pour traitement des dépôts de chèques sur un compte bancaire en utilisant une reconnaissance optique de caractères. Il repose actuellement sur le service Bluemix {{site.data.keyword.openwhisk_short}} public et s'appuie sur Cloudant et SoftLayer Object Storage. Sur site, il peut utiliser CouchDB et OpenStack Swift. D'autres services de stockage, comme FileNet ou Cleversafe, pourraient être utilisés. Tesseract fournit la bibliothèque OCR.
## Applications cognitives
{: #openwhisk_common_use_cases_cognitive}

Les technologies cognitives peuvent être combinées efficacement avec {{site.data.keyword.openwhisk_short}} pour créer des applications puissantes. Par exemple, IBM Alchemy API et Watson Visual Recognition peuvent être utilisés avec {{site.data.keyword.openwhisk_short}} pour extraire automatiquement des informations utiles provenant de vidéos sans avoir à regarder ces dernières Il peut s'agir simplement d'une extension “cognitive” du scénario [Traitement de données](#data-processing) décrit auparavant. L'emploi d'{{site.data.keyword.openwhisk_short}} pour implémenter une fonction Bot combinée à d'autres services cognitifs est une autre utilisation pratique . 

Voici un exemple d'application [Dark Vision](https://github.com/IBM-Bluemix/openwhisk-darkvisionapp) qui permet de faire cela. Dans cette application, l'utilisateur télécharge une vidéo ou une image à l'aide de l'application Web Dark Vision, qui la stocke dans une base de données Cloudant. Une fois la vidéo téléchargée, {{site.data.keyword.openwhisk_short}} la détecte en écoutant les modifications Cloudant (déclencheur). {{site.data.keyword.openwhisk_short}} déclenche ensuite l'action d'extraction de vidéo. Pendant son exécution, l'extracteur produit des images et les stocke dans Cloudant. Les images sont ensuite traitées à l'aide de Watson Visual Recognition et les résultats sont stockés dans la même base de données Cloudant. Les résultats peuvent être affichés à l'aide de l'application Web Dark Vision OU d'une application iOS. Object Storage peut être utilisé en plus de Cloudant. Dans ce cas, les métadonnées des vidéos et des images sont stockées dans Cloudant et les fichiers média sont stockés dans Object Storage.

L'[exemple d'application iOS Swift](https://github.com/gconan/BluemixMobileServicesDemoApp) ci-après illustre l'utilisation d'{{site.data.keyword.openwhisk_short}}, d'IBM Mobile Analytics et de Watson pour analyser le ton et poster les conclusions sur un canal Slack.

## Traitement d'événements avec Kafka ou Message Hub 

{{site.data.keyword.openwhisk_short}} est particulièrement bien adapté à une utilisation conjointe avec Kafka, le service IBM Message Hub (basé Kafka) et d'autres systèmes de messagerie. Les systèmes étant par nature gérés par événements, un environnement d'exécution géré lui-aussi par événements est requis pour le traitement des messages et l'application de la logique métier à ces messages, ce qui est exactement ce qu'offre {{site.data.keyword.openwhisk_short}} avec ses flux, déclencheurs, actions, etc. Kafka et Message Hub sont souvent utilisés pour les volumes de charge de travail très élevés et imprévisibles et qui nécessitent un redimensionnement au pied levé des consommateurs de ces messages, à nouveau un atout d'{{site.data.keyword.openwhisk_short}}. {{site.data.keyword.openwhisk_short}} intègre d'office la capacité de consommer, tout comme de publier, des messages fournis dans le package [openwhisk-package-kafka](https://github.com/openwhisk/openwhisk-package-kafka).

Ci-après figure un [exemple d'application qui implémente le scénario de traitement d'événements](https://github.com/IBM/openwhisk-data-processing-message-hub) avec {{site.data.keyword.openwhisk_short}}, Message Hub et Kafka.
