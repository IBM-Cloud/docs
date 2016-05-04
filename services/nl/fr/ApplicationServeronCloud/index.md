---

copyright:
  années : 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Initiation à IBM WebSphere Application Server for Bluemix
{: #getting_started}

*Dernière mise à jour : 8 avril 2016*

{{site.data.keyword.IBM}} WebSphere Application Server for {{site.data.keyword.Bluemix}} est un service permettant une configuration rapide
sur une instance WebSphere Application Server Liberty, Network Deployment, ou Traditional, pré-configurée dans un environnement de cloud hébergé sur
Bluemix.
{: shortdesc}

## Présentation de WebSphere Application Server for Bluemix
{: #overview}

WebSphere Application Server for Bluemix fournit aux consommateurs des serveurs WebSphere traditionnels et Liberty Profile
préconfigurés. Il est hébergé sur des invités de machine virtuelle avec les droits d'accès de l'utilisateur root au système d'exploitation invité. Lorsque vous
créez votre service, choisissez entre *Liberty*, *ND* ou *WebSphere traditionnel*.

Vous êtes initié à l'administration WebSphere et disposez d'un accès complet au système d'exploitation sous-jacent. Vous pouvez réutiliser vos scripts existants et apporter de petites personnalisations au système afin de travailler avec vos propres infrastructures ou des
infrastructures tierces. Le centre d'administration et la console d'administration vous permettent d'administrer votre service WebSphere Application Server Liberty,
ND, ou Traditional, de la même façon que vos configurations WebSphere sur site.


**Remarque **: Le plan WebSphere Application Server for Bluemix Network Deployment propose à présent davantage de fonctions. Il se compose
d'un environnement de cellule WebSphere Application Server Network Deployment avec deux machines virtuelles, ou plus.
La première machine virtuelle contient le gestionnaire de déploiement et IBM
HTTP Server ; les autres machines virtuelles contiennent les noeuds personnalisés (agents de noeud) fédérés dans le gestionnaire de déploiement. Utilisez les scripts wsadmin existants pour créer votre configuration WebSphere ou servez-vous de la console d'administration WebSphere pour configurer
manuellement l'environnement. Ces nouvelles fonctions permettent aux utilisateurs de configurer un environnement en cluster pour la haute disponibilité, la
reprise en ligne et l'évolutivité. La mise en cluster est un aspect essentiel de toute application d'entreprise middleware, et les clients peuvent désormais choisir de mettre en cluster une
topologie afin d'équilibrer la charge des demandes entre deux instances, ou plus.

Le plan WebSphere Application Server for Bluemix Liberty Core propose lui aussi désormais davantage de fonctions. Il inclut l'utilisation d'une collectivité Liberty, qui est un domaine d'administration pour un groupe de profils Liberty (serveurs) et qui se
compose de deux machines virtuelles, ou plus. La première machine virtuelle contient le serveur Liberty du contrôleur de collectivité, qui constitue un point de contrôle pour la collectivité Liberty. En plus de la collectivité Liberty, cette machine virtuelle contient également le serveur IBM HTTP Server, qui permet l'accès à vos applications depuis un
navigateur Web. Les autres machines virtuelles sont les hôtes de la collectivité sur lesquels résident les membres de la collectivité (serveurs de profil
Liberty). Le centre d'administration Liberty est également activé sur le serveur du contrôleur Liberty.

Le diagramme suivant présente l'architecture des environnements de cellule WebSphere Application Server for Bluemix Network Deployment et de collectivité
Liberty.

![Figure 1. Architecture de cellule Network deployment et de collectivité Liberty](images/CellCollectiveDiagram.gif)

## Environnement d'exploitation
{: #operational_environment}

IBM WebSphere Application Server for Bluemix est un service qui renvoie des invités (machines virtuelles) dans un environnement partagé
sur lesquels les consommateurs peuvent déployer des applications. Un réseau privé virtuel protège le service public des analyses de port générique et d'autres attaques indésirables via le réseau. Toutefois,
il est important que vous vous rappeliez que le réseau privé virtuel du service que vous utilisez pour accéder à votre instance de service
peut être partagé par plusieurs organisations et utilisateurs Bluemix. Les machines virtuelles fournissent des ressources de traitement, de mémoire
et d'E-S provenant d'un pool partagé de ressources IaaS. Si vous désirez exécuter vos applications dans un environnement privé, prenez contact avec votre
ingénieur commercial IBM qui pourra vous présenter notre offre IBM WebSphere Application Server for Bluemix dédiée.

Etant donné que les ressources de traitement,
de mémoire et d'E-S sont exécutées par des machines virtuelles dans un environnement partagé, les configurations de service peuvent varier. Vous pouvez
examiner la configuration de chaque instance de service spécifique dans les portails et les tableaux de bord des services IBM
WebSphere Application Server for
Bluemix.

**Remarque **: IBM WebSphere Application Server for Bluemix propose à présent aux clients avec des applications gourmandes en mémoire
une option leur permettant de redimensionner leur environnement avec des machines virtuelles plus grandes. Les clients peuvent sélectionner
la taille de ressource spécifique d'un composant WebSphere Application Server en place ou d'un seul système en leur allouant des machines virtuelles dotés de
jusqu'à 32 Go de mémoire RAM.

## Stratégie de tarification
{: #pricing_strategy}

IBM WebSphere Application Server for Bluemix fournit des instances de machine virtuelle. Avec ces instances, les clients utilisent un simple portail pour
créer et gérer les déploiements WebSphere Application Server en entreprise de manière cohérente et reproductible, tout en bénéficiant d'une souplesse substantielle
pour paramétrer leurs applications. Les utilisateurs peuvent exploiter des machines virtuelles WebSphere Application Server Liberty,
ND, ou Traditional préconfigurées, dans un environnement de cloud hébergé. Les utilisateurs peuvent faire migrer les applications
WebSphere Application Server existantes vers Bluemix et contrôler complètement le système d'exploitation et le middleware sous-jacents.

IBM WebSphere Application Server for Bluemix est proposé avec le paramètre de calcul de redevance suivant :

*  *Instance-Heure* : Une instance est définie comme un accès à une configuration spécifique du service
IBM WebSphere Application Server for Bluemix. Les clients sont facturés pour chaque heure complète ou partielle d'utilisation du service déployé
sur la période de facturation. Chaque instance-heure est facturée mensuellement et si une instance n'est utilisée que pendant une partie du mois,
le taux d'utilisation est réparti au prorata.

Par exemple, si vous utilisez le plan ND, une instance équivaut à 1 UC virtuelle avec 2 Go de RAM et 12 Go HD. Donc, si vous choisissez de
configurer votre cellule avec un noeud de contrôle et huit noeuds personnalisés, vous seriez facturé pour neuf noeuds
(instances).

**Remarque **: La facturation minimum est de 0,25 instance heure par noeud Custom ou hôte Liberty. Dans l'exemple ci-dessus, un noeud de
contrôle et un noeud personnalisé configuré pendant au moins 15 minutes entraînerait une facturation minimum de (0,25 * Nombre d'instances).

# rellinks
## général
* [WASdev](https://developer.ibm.com/wasdev/){: new_window}
* [Documentation de WebSphere Application Server](http://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/as_ditamaps/was855_welcome_ndmp.html){: new_window}
* [Documentation de WebSphere Application Server
traditional v9 Beta](http://www.ibm.com/support/knowledgecenter/SSEQTP_9.0.0/as_ditamaps/was900_welcome_base.html){: new_window}
