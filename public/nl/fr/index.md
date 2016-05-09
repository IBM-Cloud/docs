---

 

copyright:

  years: 2016

 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} public
{: #public}
*Dernière mise à jour : 22 février 2016*


{{site.data.keyword.Bluemix_notm}} fait abstraction de la plupart des aspects complexes associés à l'hébergement et à la gestion des
applications basées sur le
cloud et les masque. En tant que développeur d'applications, vous pouvez vous consacrer au développement de votre application sans avoir à gérer l'infrastructure
requise pour son
hébergement.
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} propose des déploiements de cloud qui répondent à vos besoins. Que vous fassiez partie d'une
petite entreprise en pleine évolution ou d'une grande entreprise qui a besoin d'un isolement supplémentaire, vous pouvez vous développer dans un cloud sans
limite, dans lequel vous pouvez connecter vos services dédiés aux services {{site.data.keyword.Bluemix_notm}} publics mis à disposition par
{{site.data.keyword.IBM_notm}} et
des fournisseurs tiers. Toutes les instances de service sont gérées par {{site.data.keyword.IBM_notm}}. Vous recevez une seule facture,
uniquement pour les éléments que vous choisissez d'utiliser.

{{site.data.keyword.Bluemix_notm}}
est essentiellement un environnement dans lequel vous pouvez développer des applications et
utiliser des services qui fournissent des fonctions prêtes à l'emploi. {{site.data.keyword.Bluemix_notm}} fournit également un environnement pour héberger des artefacts s'exécutant sur un serveur d'applications tel que Liberty. En utilisant SoftLayer, {{site.data.keyword.Bluemix_notm}} déploie des conteneurs virtuels qui hébergent chaque
application déployée. Dans cet environnement, l'application peut utiliser des services préconfigurés (incluant des services de tiers) pour faciliter
l'assemblage d'applications.

Pour les applications mobiles et Web, vous pouvez utiliser les services préconfigurés fournis par
{{site.data.keyword.Bluemix_notm}}. Pour les applications Web, vous pouvez télécharger votre application web dans {{site.data.keyword.Bluemix_notm}} et
indiquer le
nombre d'instances que vous souhaitez exécuter. Lorsque vos applications sont déployées, vous pouvez facilement les redimensionner en fonction des
changements
d'utilisation ou de charge.

Avec le large ensemble de services et de contextes d'exécution de {{site.data.keyword.Bluemix_notm}}, le
développeur dispose d'un contrôle et d'une flexibilité accrus, ainsi que d'un accès à diverses options de données, de l'analyse prédictive aux mégadonnées.

{{site.data.keyword.Bluemix_notm}} fournit les fonctionnalités suivantes :

- Une gamme de services pour générer et étendre rapidement des applications Web et mobiles.
- Une puissance de traitement pour distribuer en continu des modifications d'application.
- Des services et des modèles de programmation adaptés au besoin.
- Des services et des applications d'une grande maniabilité.
- Des charges de travail optimisées et élastiques.
- Une disponibilité continue.

{{site.data.keyword.Bluemix_notm}} permet de développer rapidement des applications dans la plupart des langages
de programmation les plus courants. Vous pouvez développer des applications mobiles dans iOS, Android et HTML avec JavaScript. Pour les applications Web,
vous pouvez utiliser des langages tels que Ruby, PHP, Java&trade;, Go et Python. Vous pouvez aussi migrer des applications existantes vers {{site.data.keyword.Bluemix_notm}} et utiliser les
contextes d'exécution fournis par {{site.data.keyword.Bluemix_notm}} pour exécuter vos applications.

{{site.data.keyword.Bluemix_notm}} fournit également des services middleware pour vos applications. {{site.data.keyword.Bluemix_notm}} agit au nom de l'application lorsqu'il provisionne des instances de service, puis lie ces services à
l'application. Votre
application peut effectuer son véritable travail tout en laissant la gestion des services à l'infrastructure.

## Architecture de l'environnement {{site.data.keyword.Bluemix_notm}} public
{: #publicarch}


En général, il est inutile de se préoccuper des couches du système d'exploitation et de l'infrastructure lorsque vous exécutez des applications dans
{{site.data.keyword.Bluemix_notm}}. Les
couches, telles que les systèmes de fichiers racine et les composants de
middleware, sont masquées pour que vous puissiez vous concentrer sur le code de
votre application. Cependant, vous pouvez obtenir plus de détails sur ces couches si vous avez besoin d'informations spécifiques sur
l'emplacement d'exécution de votre application. Pour plus d'informations, voir [Affichage des couches de l'infrastructure {{site.data.keyword.Bluemix_notm}}](../cli/vcapsvc.html#viewinfra).

En tant que développeur, vous pouvez interagir avec l'infrastructure {{site.data.keyword.Bluemix_notm}} via une interface utilisateur basée sur un navigateur. Vous pouvez également utiliser une interface de ligne de commande Cloud Foundry, appelée cf, pour déployer des applications Web.

Les clients, qui peuvent être des applications mobiles, des applications exécutées en externe, des applications construites dans
{{site.data.keyword.Bluemix_notm}} ou des développeurs qui utilisent des navigateurs, interagissent avec les applications hébergées par
{{site.data.keyword.Bluemix_notm}}. Ils utilisent des API REST OU HTTP pour
router les demandes via {{site.data.keyword.Bluemix_notm}} vers l'une des
instances d'application ou des services composites.

La figure suivante présente l'architecture de haut niveau {{site.data.keyword.Bluemix_notm}}.

![Architecture {{site.data.keyword.Bluemix_notm}}](images/arch.png)

*Figure 1. Architecture {{site.data.keyword.Bluemix_notm}}*

Vous pouvez déployer vos
applications dans différentes régions {{site.data.keyword.Bluemix_notm}}, pour des raisons de sécurité ou pour
réduire le temps d'attente. Vous pouvez procéder au déploiement dans une région ou dans plusieurs régions. Pour plus d'informations, voir
[Régions](index.html#ov_intro_reg).


![Développement d'applications dans plusieurs régions](images/multi-region.png)

*Figure 2. Développement d'applications dans plusieurs régions*

### Fonctionnement de {{site.data.keyword.Bluemix_notm}}
{: #howwork}

Lorsque vous
déployez une application dans {{site.data.keyword.Bluemix_notm}}, vous devez configurer
{{site.data.keyword.Bluemix_notm}} avec les informations nécessaires à la prise en charge de celle-ci.

* Dans le cas d'une application mobile, {{site.data.keyword.Bluemix_notm}} contient un artefact qui représente
le système de back end de l'application mobile, comme les services utilisés par l'application mobile pour communiquer avec un serveur.
* Dans le cas d'une application Web, vous devez vous assurer que les informations appropriées sur l'environnement d'exécution et l'infrastructure sont
communiquées à
{{site.data.keyword.Bluemix_notm}}, de sorte que l'application puisse être exécutée.

Chaque
environnement d'exécution, y compris mobile et web, est distinct de celui des autres applications. Les environnements d'exécution sont isolés, même si les applications sont sur la même machine physique. La figure suivante présente le flux de base suivi par {{site.data.keyword.Bluemix_notm}} pour gérer le
déploiement des applications :

![Déploiement d'une application](images/deploy.png)

*Figure 5. Déploiement d'une application*

Lorsque vous créez une application et que vous la déployez dans {{site.data.keyword.Bluemix_notm}}, l'environnement
{{site.data.keyword.Bluemix_notm}} choisit un serveur virtuel approprié sur lequel l'application ou les artefacts
représentés par
l'application sont envoyés. Pour une application mobile, une projection de back end mobile est créée dans {{site.data.keyword.Bluemix_notm}}. Tout code de l'application mobile exécuté sur le cloud l'est finalement dans l'environnement {{site.data.keyword.Bluemix_notm}}. Pour une application Web, le code exécuté sur le cloud correspond à
l'application elle-même, que le développeur déploie dans {{site.data.keyword.Bluemix_notm}}. Le choix du serveur virtuel dépend de plusieurs
facteurs, dont :

* La charge actuelle de la machine
* Les environnements d'exécution ou les infrastructures pris en charge par le serveur virtuel

Une fois le serveur virtuel choisi, un gestionnaire d'application sur chaque serveur virtuel installe l'infrastructure et l'environnement
d'exécution requis pour
l'application. Celle-ci peut alors être déployée
dans cette infrastructure. Ensuite, les artefacts d'application sont démarrés.

La figure suivante présente la structure d'un serveur virtuel, aussi appelé agent DEA (Droplet Execution Agent), sur lequel
plusieurs
applications sont déployées :

![Conception d'un serveur virtuel](images/container.png)

*Figure 6. Conception d'un serveur virtuel*

Sur chaque serveur virtuel, un gestionnaire d'application communique avec le reste de l'infrastructure
{{site.data.keyword.Bluemix_notm}}
et gère les applications déployées. Chaque serveur virtuel dispose de conteneurs pour séparer et protéger les applications. Dans chaque conteneur,
{{site.data.keyword.Bluemix_notm}} installe l'infrastructure et l'environnement d'exécution requis pour chaque
application.

Si l'application déployée dispose d'une interface Web (par exemple, une application Web Java) ou de services REST (par exemple, des services mobiles
exposés publiquement à l'application mobile), les utilisateurs de cette application peuvent communiquer avec elle via des demandes HTTP normales.

![Appel d'une application {{site.data.keyword.Bluemix_notm}}](images/execute.png)

*Figure 7. Appel d'une application {{site.data.keyword.Bluemix_notm}}*

Chaque application
peut être associée à une ou plusieurs adresses URL, mais elles doivent toutes désigner le noeud final
{{site.data.keyword.Bluemix_notm}}. Lorsqu'une demande arrive,
{{site.data.keyword.Bluemix_notm}} l'examine, détermine l'application à laquelle elle est adressée, puis
sélectionne l'instance de l'application qui recevra la demande.


## Régions
{: #ov_intro_reg}

Une région {{site.data.keyword.Bluemix_notm}} est un territoire géographique défini sur lequel vous pouvez déployer vos applications. Vous
pouvez créer des instances d'application et de service dans différentes régions avec la même infrastructure {{site.data.keyword.Bluemix_notm}} pour
la gestion des applications et la même vue de détails de l'utilisation pour la facturation. Vous pouvez sélectionner la région la plus proche de vos clients et y déployer vos applications pour avoir un temps d'attente faible. Vous pouvez également sélectionner la région où vous voulez garder les données d'application permettant d'adresser les problèmes de sécurité. Lorsque vous construisez des applications dans plusieurs régions et que l'une des régions s'arrête, les applications des autres régions continuent de
fonctionner. La franchise de ressources est la même dans toutes les régions que vous utilisez.

Si
vous employez l'interface utilisateur
{{site.data.keyword.Bluemix_notm}}, vous pouvez basculer vers une région différente et travailler avec les
espaces de cette région.

Si vous utilisez l'interface de ligne de commande cf, vous devez vous connecter à la région {{site.data.keyword.Bluemix_notm}} avec laquelle vous voulez travailler en entrant la
commande cf api et en spécifiant le noeud final d'API de la région. Par exemple, entrez la commande suivante pour vous connecter à la région {{site.data.keyword.Bluemix_notm}}
Europe et Royaume-Uni :

```
cf api https://api.eu-gb.{{site.data.keyword.Bluemix_notm}}.net
```

Si vous utilisez les outils Eclipse, vous devez vous connecter à la région
{{site.data.keyword.Bluemix_notm}} avec laquelle vous voulez travailler en créant un serveur
{{site.data.keyword.Bluemix_notm}} et en spécifiant le noeud final d'API de la région. Pour plus d'informations sur l'utilisation des outils
Eclipse, voir [Déploiement d'applications avec {{site.data.keyword.IBM_notm}} Eclipse
Tools for {{site.data.keyword.Bluemix_notm}}](../manageapps/eclipsetools/eclipsetools.html#toolsinstall).

Un préfixe unique est affecté à chaque région. {{site.data.keyword.Bluemix_notm}} fournit les régions et les préfixes suivants :

<!-- PRODUCTION ONLY: Ensure that URLs are production URLs, not stage1-->

| **Nom de région** | **Zone géographique** | **Préfixe de région** | **cf API endpoint** | **Console d'interface utilisateur** |       
|-----------------|-------------------------|-------------------|---------------------|----------------|
| Région Sud des Etats-Unis | Dallas, US | ng | api.ng.bluemix.net | console.ng.bluemix.net |
| Région Royaume-Uni | Londres, Angleterre | eu-gb | api.eu-gb.bluemix.net | console.eu-gb.bluemix.net |
| Région Sydney | Sydney, Australie | au-syd | api.au-syd.bluemix.net | console.au-syd.bluemix.net |

*Tableau 1. Liste des régions {{site.data.keyword.Bluemix_notm}}*


## Résilience dans {{site.data.keyword.Bluemix_notm}}
{: #resiliency}

{{site.data.keyword.Bluemix_notm}} a été conçu pour héberger des applications et des artefacts d'application
évolutifs
et résilients pouvant s'adapter à vos besoins, rester hautement disponibles et
assurer une reprise rapide en cas de problème. {{site.data.keyword.Bluemix_notm}} sépare les composants qui assurent le suivi de l'état des interactions (avec état) de ceux qui n'effectuent
pas de suivi (sans état). Cette
distinction permet à {{site.data.keyword.Bluemix_notm}} de déplacer des applications de façon souple en fonction des besoins
pour
assurer l'évolutivité et la résilience.

Vous pouvez disposer d'une ou de plusieurs instances de votre application. Dans les deux cas, l'application
est chargée une seule fois. Toutefois, {{site.data.keyword.Bluemix_notm}} déploie le nombre d'instances de l'application demandé et distribue ces
instances sur autant de serveurs virtuels que possible.

Vous devez sauvegarder toutes les données
persistantes dans un magasin de données avec état qui se trouve hors de votre application, par exemple dans un magasin de données des services de magasin de
données fournis par {{site.data.keyword.Bluemix_notm}}. Etant donné que les éléments mis en cache dans la mémoire ou sur le disque peuvent ne pas être disponibles même après un redémarrage, vous pouvez
utiliser l'espace
mémoire ou le système de fichiers d'une instance {{site.data.keyword.Bluemix_notm}} unique comme cache de
transaction unique temporaire. Dans le cas de la configuration d'une instance unique, la demande envoyée à votre application peut être interrompue en raison
de la nature sans état de {{site.data.keyword.Bluemix_notm}}. Il est recommandé d'utiliser au moins trois instances pour chaque application afin d'assurer la disponibilité de votre application.

L'ensemble de l'infrastructure {{site.data.keyword.Bluemix_notm}}, les composants Cloud Foundry et les composants de gestion propres à {{site.data.keyword.IBM_notm}} sont hautement disponibles. Plusieurs instances de l'infrastructure sont utilisées pour équilibrer la charge.

## Intégration avec les systèmes d'enregistrement
{: #sor}

{{site.data.keyword.Bluemix_notm}} peut aider les développeurs en connectant deux grandes catégories de systèmes dans un environnement de cloud : les systèmes d'enregistrement et les systèmes d'engagement.

Les *systèmes d'enregistrement* incluent les applications et les bases de données qui stockent des enregistrements métier et automatisent
des
processus standardisés. Des *systèmes d'engagement* permettent de développer l'utilité des systèmes d'enregistrement en les rendant
plus attractifs pour les utilisateurs.
En intégrant un système d'enregistrement à l'application que vous créez dans {{site.data.keyword.Bluemix_notm}}, vous pouvez :

 * Activer une communication sécurisée entre l'application et la base de données dorsale, via le téléchargement et l'installation d'un connecteur
sécurisé sur site.
 * Appeler une base de données de manière sécurisée.
 * Créer des interfaces de programme d'application à partir des flux d'intégration avec les bases de données et les systèmes expéditeurs, par exemple, un système de gestion de la relation client.
 * Exposer uniquement les schémas et les tables de votre choix à l'application.
 * En tant que responsable d'organisation {{site.data.keyword.Bluemix_notm}}, publier une interface de programme d'application sous forme de service privé, visible uniquement des membres de votre organisation.

Utiliser le service Cloud Integration pour intégrer un système d'enregistrement à l'application que vous créez dans {{site.data.keyword.Bluemix_notm}}. Le service Cloud Integration permet de créer et de publier une API Cloud Integration en tant que service privé pour
votre
organisation.

<dl>
<dt>API Cloud Integration</dt>
    <dd>Une API Cloud Integration fournit un accès sécurisé aux systèmes d'enregistrement résidant derrière un pare-feu
via des API Web. Lorsque vous créez l'API Cloud Integration, vous choisissez la ressource à laquelle vous voulez accéder via l'API Web, spécifiez les
opérations qui sont autorisées et incluez les logiciels SDK et les exemples pour accéder à l'API. Pour plus d'informations sur la création d'une API Cloud
Integration, voir [Création d'une API Cloud Integration](../services/CloudIntegration/index.html#cloudint_add_service).</dd>
<dt>Service privé</dt>
    <dd>Un service privé est composé d'une API Cloud Integration, de logiciels SDK et de règles de droits. De plus, le service privé peut contenir de la documentation ou d'autres éléments appartenant au fournisseur de services. Seul le responsable de l'organisation peut publier une API Cloud Integration en tant que service privé. Pour connaître les services privés à votre
disposition, cochez la case Privé dans le catalogue {{site.data.keyword.Bluemix_notm}}. Vous pouvez sélectionner et lier un service privé à une application sans vous connecter au service Cloud Integration. Pour lier un service privé à votre
application, procédez de la même façon que pour les services {{site.data.keyword.Bluemix_notm}}. Pour des informations sur la publication d'une API en tant que service privé, voir Publication d'une API en tant que service privé.</dd>
</dl>

### Scénario : Création d'une application mobile riche pour la connexion avec votre système d'enregistrement
{: #scenario}

{{site.data.keyword.Bluemix_notm}} fournit une plateforme dans laquelle vous pouvez intégrer votre application mobile, des services de cloud et
des
systèmes d'entreprise d'enregistrement pour générer une application qui interagit avec vos données sur site.

Par exemple, vous pouvez concevoir une application mobile pour interagir avec votre système de gestion de la relation client résidant sur site, derrière un pare-feu. Vous pouvez appeler le système d'enregistrement de manière sécurisée et optimiser les services mobiles dans {{site.data.keyword.Bluemix_notm}} afin
de générer une application mobile riche.

Tout d'abord, votre développeur d'intégration crée l'application de back end mobile dans {{site.data.keyword.Bluemix_notm}}. Il fait appel au conteneur boilerplate Mobile Cloud utilisant le contexte d'exécution Node.js qu'il connaît le mieux.

Puis, en utilisant le service Cloud Integration dans l'interface utilisateur {{site.data.keyword.Bluemix_notm}}, il expose une API via un connecteur
sécurisé. Le développeur d'application télécharge le connecteur sécurisé et l'installe sur site, afin d'activer la communication sécurisée entre son  interface de programme d'application et la base de données. Après avoir créé le noeud final de base de données, il peut consulter tous les schémas et extraire les tables qu'il veut exposer à l'application en tant
qu'API.

Il ajoute ensuite le service Push pour distribuer des notifications mobiles aux clients intéressés. Il ajoute également un service de partenaire commercial pour écrire un tweet lorsqu'un nouvel enregistrement client est créé avec une interface de programme d'application Twitter.

En tant que développeur d'application, vous pouvez ensuite vous connecter à {{site.data.keyword.Bluemix_notm}}, télécharger le kit d'outils de développement Android et développer le code appelant les interfaces de programme d'application créées par le développeur d'intégration. Vous pouvez développer une application mobile qui permet aux utilisateurs d'entrer des informations sur leur périphérique mobile. Cette application crée alors un enregistrement client dans le système de gestion client. Lorsque l'enregistrement est créé, l'application crée une notification push pour périphérique mobile et un tweet pour signaler le nouvel enregistrement.

# rellinks
## general
* [Nouveautés de {{site.data.keyword.Bluemix_notm}}](../whatsnew/index.html)
* [Configuration requise pour {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/support/#prereqs)
* [Problèmes {{site.data.keyword.Bluemix_notm}} connus](https://developer.ibm.com/bluemix/support/#issues)
* [Gestion de votre compte](../admin/adminpublic.html#mngacct)
* [Glossaire {{site.data.keyword.Bluemix_notm}}](../overview/glossary/index.html)
