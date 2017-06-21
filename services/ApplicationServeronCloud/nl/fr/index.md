---

copyright:
  years: 2015, 2016
lastupdated: "2017-02-24"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Initiation à IBM WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}
{: #getting_started}

{{site.data.keyword.IBM}} WebSphere Application Server in {{site.data.keyword.Bluemix}} est un service qui permet une configuration rapide sur une instance WebSphere Application Server Liberty, Traditional Network Deployment ou Traditional WebSphere Java EE pré-configurée dans un environnement de cloud hébergé sur {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

## Présentation de WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}
{: #overview}

WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} fournit aux consommateurs des serveurs Traditional WebSphere et Liberty Profile préconfigurés. Il est hébergé sur des invités de machine virtuelle avec les droits d'accès de l'utilisateur root au système d'exploitation invité. Quand vous créez votre service, choisissez entre *Liberty*, *Traditional ND* ou *Traditional WebSphere*.

**Remarque :** les consommateurs sont maintenant en mesure de choisir entre V8.5 et V9.0 lors de la création d'une nouvelle instance *Traditional ND* ou *Traditional WebSphere*.

Vous êtes initié à l'administration WebSphere et disposez d'un accès complet au système d'exploitation sous-jacent. Vous pouvez réutiliser vos scripts existants et apporter de petites personnalisations au système afin de travailler avec vos propres infrastructures ou des infrastructures tierces. Le centre d'administration et les consoles d'administration vous permettent d'administrer votre service WebSphere Application Server Liberty ou Traditional, de la même façon que vos configurations WebSphere sur site.

Le plan WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} Network Deployment se compose d'un environnement de cellule WebSphere Application Server Network Deployment avec deux machines virtuelles, ou plus. La première machine virtuelle contient le gestionnaire de déploiement et IBM HTTP Server ; les autres machines virtuelles contiennent les noeuds personnalisés (agents de noeud) fédérés dans le gestionnaire de déploiement. Utilisez les scripts wsadmin existants pour créer votre configuration WebSphere ou servez-vous de la console d'administration WebSphere pour configurer manuellement l'environnement. Ces nouvelles fonctionnalités permettent aux utilisateurs de créer un environnement en cluster, aspect essentiel de toute application d'entreprise middleware. Les clients peuvent désormais choisir de mettre en cluster une topologie afin d'équilibrer la charge des demandes entre deux instances, ou plus.

Le plan WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} Liberty Core inclut l'utilisation de Liberty Collective. Liberty Collective, qui est un domaine d'administration pour un groupe de profils Liberty (serveurs), se
compose de deux machines virtuelles, ou plus. La première machine virtuelle contient le serveur Liberty du contrôleur de collectivité, qui constitue un point de contrôle pour la collectivité Liberty. En plus de la collectivité Liberty, cette machine virtuelle contient également le serveur IBM HTTP Server, qui permet l'accès à vos applications depuis un navigateur Web. Les autres machines virtuelles sont les hôtes de la collectivité sur lesquels résident les membres de la collectivité (serveurs de profil Liberty). Le centre d'administration Liberty est également activé sur le serveur du contrôleur Liberty.

Le diagramme suivant présente l'architecture des environnements de cellule Network Deployment et de collectivité Liberty de WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}.

Figure 1. Cellule de déploiement réseau et architecture de collectivité Liberty

![Figure 1. Architecture de cellule Network Deployment et de collectivité Liberty](images/CellCollectiveDiagram.gif)

**Remarque** : Dans la *Figure 1* ci-dessus, le modèle qui représente la collocation du gestionnaire de déploiement ou du contrôleur de collectivité avec IBM HTTP Server est destiné au développement et au test. WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} vous donne également la liberté de reconfigurer le logiciel préinstallé pour répondre à vos besoins en matière d'applications et de production ; tout comme vous le feriez sur place. En outre, pour les exigences de production les plus strictes, contactez votre ingénieur commercial IBM qui peut vous informer sur notre offre IBM WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} à service exclusif, qui propose des ressources isolées en réseau et en calcul.


## Environnement d'exploitation
{: #operational_environment}

IBM WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} est un service qui renvoie des invités (machines virtuelles) dans un environnement partagé sur lesquels les consommateurs peuvent déployer des applications. Un réseau privé virtuel protège le service public des analyses de port générique et d'autres attaques indésirables via le réseau. Toutefois, il est important que vous vous rappeliez que le réseau privé virtuel du service que vous utilisez pour accéder à votre instance de service peut être partagé par plusieurs organisations et utilisateurs {{site.data.keyword.Bluemix_notm}}. Les machines virtuelles fournissent des ressources de traitement, de mémoire et d'E-S provenant d'un pool partagé de ressources IaaS.

Etant donné que les ressources de traitement, de mémoire et d'E-S sont exécutées par des machines virtuelles dans un environnement partagé, les configurations de service peuvent varier. Vous pouvez examiner la configuration de chaque instance de service spécifique dans les portails et les tableaux de bord des services IBM WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}.

IBM WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} fournit des instances de machine virtuelle. Avec ces instances, les clients utilisent un simple portail pour créer et gérer les déploiements WebSphere Application Server en entreprise de manière cohérente et reproductible, tout en bénéficiant d'une souplesse substantielle pour paramétrer leurs applications. Les utilisateurs peuvent exploiter des machines virtuelles WebSphere Application Server Liberty, ND, ou Traditional préconfigurées, dans un environnement de cloud hébergé. Les utilisateurs peuvent faire migrer les applications WebSphere Application Server existantes vers {{site.data.keyword.Bluemix_notm}} et contrôler complètement le système d'exploitation et le middleware sous-jacents.

## Stratégie de tarification
{: #pricing_strategy}

IBM WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} fournit aux clients disposant d'applications gourmandes en mémoire des instances de taille T-Shirt qui leur permettent de redimensionner correctement leur environnement avec des machines virtuelles plus grandes. Les clients peuvent sélectionner la taille de ressource spécifique d'un composant WebSphere Application Server en place ou d'un seul système en leur allouant des machines virtuelles dotés de jusqu'à 32 Go de mémoire RAM.

Les tableaux suivants indiquent les prix des différents plans IBM WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}, au 1er avril 2016, en dollars US.

*Tableau 1. Plan Liberty Core*

| **T-Shirt** | **vCPU** | **RAM (Go)** | **HD (Go)** | **Prix/Hr** |       
|:-------------:|:----------:|:--------------:|:-------------:|:--------------:|
| S | 1 | 2 | 12 | 0,21 $ |
| M | 2 | 4 | 25 | 0,42 $ |
| L | 4 | 8 | 50 | 0,84 $ |
| XL | 8 | 16 | 100 | 1,68 $ |
| XXL | 16 | 32 | 200 | 3,36 $ |

*Tableau 2. Plan WebSphere Application Server Base*

| **T-Shirt** | **vCPU** | **RAM (Go)** | **HD (Go)** | **Prix/Hr** |       
|:-------------:|:----------:|:--------------:|:-------------:|:--------------:|
| S | 1 | 2 | 12 | 0,30 $ |
| M | 2 | 4 | 25 | 0,60 $ |
| L | 4 | 8 | 50 | 1,20 $ |
| XL | 8 | 16 | 100 | 2,40 $ |
| XXL | 16 | 32 | 200 | 4,80 $ |

*Tableau 3. Plan WebSphere Application Server ND*

| **T-Shirt** | **vCPU** | **RAM (Go)** | **HD (Go)** | **Prix/Hr** |       
|:-------------:|:----------:|:--------------:|:-------------:|:--------------:|
| S | 1 | 2 | 12 | 0,70 $ |
| M | 2 | 4 | 25 | 1,40 $ |
| L | 4 | 8 | 50 | 2,80 $ |
| XL | 8 | 16 | 100 | 5,60 $ |
| XXL | 16 | 32 | 200 | 11,20 $ |

<p></p>

IBM WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} est proposé avec le paramètre de calcul de redevance suivant :

*  *Instance-Heure* : une instance est définie comme un accès à une configuration spécifique du service IBM WebSphere Application Server in {{site.data.keyword.Bluemix_notm}}. Les clients sont facturés pour chaque heure complète ou partielle d'utilisation du service déployé sur la période de facturation. Chaque instance-heure est facturée mensuellement et si une instance n'est utilisée que pendant une partie du mois, le taux d'utilisation est réparti au prorata.

Par exemple, si vous utilisez le plan ND, une instance équivaut à 1 UC virtuelle avec 2 Go de RAM et 12 Go HD. Donc, si vous choisissez de configurer votre cellule avec un noeud de contrôle et huit noeuds personnalisés, vous seriez facturé pour neuf noeuds (instances).

**Remarque **: La facturation minimum est de 0,25 instance heure par noeud Custom ou hôte Liberty. Dans l'exemple ci-dessus, un noeud de contrôle et un noeud personnalisé configuré pendant au moins 15 minutes entraînerait une facturation minimum de (0,25 * Nombre d'instances).

**Remarque** : du fait d'un volume spécifique de ressources de calcul, de mémoire et d'entrée/sortie, les clients sont facturés pour les instances accumulées dans l'état STOPPED à un taux réduit de 5 %. Les clients sont gérés par rapport à un nombre fixe d'instances STOPPED ne comportant pas plus de 10 adresses IP ou 64 Go de mémoire.

# Liens connexes
{: #rellinks}
## Généralités
{: #general}
* [WASdev](https://developer.ibm.com/wasdev/){: new_window}
* [Documentation de WebSphere Application Server V9](http://www.ibm.com/support/knowledgecenter/SSEQTP_9.0.0/as_ditamaps/was900_welcome_base.html){: new_window}
