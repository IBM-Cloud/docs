---

 

copyright:

  years: 2014, 2017

lastupdated: "2017-01-10" 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Sécurité {{site.data.keyword.Bluemix_notm}}
{: #security}

Conçue selon les pratiques d'ingénierie sécurisée, la plateforme {{site.data.keyword.Bluemix}}
possède des contrôles de sécurité répartis dans des couches sur le réseau et dans l'infrastructure. {{site.data.keyword.Bluemix_notm}} fournit un
groupe de services de sécurité que les développeurs d'applications peuvent utiliser afin de sécuriser leurs applications mobiles et Web. La combinaison de ces éléments permet de faire d'{{site.data.keyword.Bluemix_notm}} une plateforme
proposant des choix clairs pour le développement d'applications sécurisé.
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} assure la sécurité en appliquant des règles de sécurité respectant les meilleurs pratiques d'IBM en matière de systèmes, de réseau et d'ingénierie
sécurisée. Ces règles incluent des pratiques telles que l'analyse du code source, l'analyse dynamique, la modélisation des menaces et des tests de pénétration. {{site.data.keyword.Bluemix_notm}} suit le processus IBM Product Security Incident Response Team (PSIRT) pour la gestion des incidents de sécurité. Pour plus d'informations, voir le site [IBM Security Vulnerability Management (PSIRT) ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](http://www-03.ibm.com/security/secure-engineering/process.html){: new_window}. 

Les environnements {{site.data.keyword.Bluemix_notm}} public et dédié utilisent les services cloud d'infrastructure sous forme de services
(IaaS) {{site.data.keyword.BluSoftlayer}} et profitent pleinement de son architecture sécurisée. L'infrastructure
sous forme de services {{site.data.keyword.BluSoftlayer}} fournit des niveaux de protection
multiples qui se chevauchent pour vos applications et vos données. Pour l'environnement {{site.data.keyword.Bluemix_notm}} local, vous êtes en charge de la sécurité physique et
fournissez l'infrastructure en hébergeant l'environnement {{site.data.keyword.Bluemix_notm}} local dans votre
propre centre de données situé derrière le pare-feu de la société. De plus,
{{site.data.keyword.Bluemix_notm}} ajoute des fonctions de sécurité au niveau de la couche plateforme sous forme de services (PaaS) dans différentes catégories : plateforme, données et application.

## Sécurité de la plateforme {{site.data.keyword.Bluemix_notm}}
{: #platform-security}

{{site.data.keyword.Bluemix_notm}} offre une sécurité fonctionnelle, d'infrastructure, opérationnelle et physique (via {{site.data.keyword.BluSoftlayer}}) pour la
plateforme de base. Toutefois, l'environnement
{{site.data.keyword.Bluemix_notm}} local est unique car le client fournit l'infrastructure et le centre de
données, et est en charge de la sécurité physique.

L'environnement {{site.data.keyword.Bluemix_notm}} sur {{site.data.keyword.BluSoftlayer}} est conforme aux normes IBM de sécurité en
matière de technologie de
l'information, qui satisfont et dépassent les valeurs standard de l'industrie. Ces normes incluent les éléments suivants : Réseau, chiffrement de données et contrôle d'accès
 * Listes de contrôle d'accès, droits et tests de pénétration
 * Identification, authentification et autorisation
 * Protection des informations et des données
 * Intégrité et disponibilité des services
 * Gestion des vulnérabilités et des correctifs
 * Détection d'attaques systématiques et par déni de service
 * Réponse aux incidents de sécurité

![Présentation de la sécurité de la plateforme Bluemix ](images/platform_sec.svg)

Figure 1. Présentation de la sécurité de la plateforme {{site.data.keyword.Bluemix_notm}}

Avec l'environnement {{site.data.keyword.Bluemix_notm}} local, vous hébergez {{site.data.keyword.Bluemix_notm}} derrière le pare-feu
de votre société et dans votre centre de données. Par conséquent, vous êtes responsable de certains aspects de la sécurité. L'image ci-dessous indique quelles sont les parties
de la sécurité qui appartiennent au client et quelles sont celles qui sont gérées et mises à jour par IBM.

![Présentation de la sécurité de la plateforme Bluemix locale](images/security_local_platform.svg){: #localplatformsecurity}

Figure 2. Présentation de la sécurité de la plateforme {{site.data.keyword.Bluemix_notm}} locale

IBM installe, surveille à distance et gère l'environnement {{site.data.keyword.Bluemix_notm}} local dans votre centre de données par le biais
d'un relais, une fonction de distribution incluse dans l'environnement {{site.data.keyword.Bluemix_notm}} local. Le relais se connecte de façon
sécurisée avec des certificats propres à chaque instance {{site.data.keyword.Bluemix_notm}} locale. Pour plus d'informations sur l'environnement
{{site.data.keyword.Bluemix_notm}} local et le relais, voir [Environnement Bluemix local](/docs/local/index.html).

### Sécurité fonctionnelle

{{site.data.keyword.Bluemix_notm}} dispose de plusieurs fonctions en matière de sécurité fonctionnelle, telles que l'authentification d'utilisateur, l'autorisation d'accès, les opérations critiques et de contrôle, et la protection de données.

<dl>
<dt>Authentification</dt>
<dd>Les développeurs d'applications sont authentifiés auprès de {{site.data.keyword.Bluemix_notm}} via l'identité Web IBM.

Pour
les environnements {{site.data.keyword.Bluemix_notm}} dédié et local, l'authentification via LDAP est
prise en charge par défaut. A la demande, l'authentification via l'identité Web IBM peut être configurée à la place pour
{{site.data.keyword.Bluemix_notm}}.
</dd>

<dt>Autorisation</dt>
<dd>{{site.data.keyword.Bluemix_notm}} utilise les mécanismes Cloud Foundry pour s'assurer que chaque développeur a accès uniquement aux applications et aux instances de service qu'il a créées. L'autorisation d'accès aux services {{site.data.keyword.Bluemix_notm}} est basée sur OAuth. L'accès à l'ensemble des noeuds finaux internes de la plateforme {{site.data.keyword.Bluemix_notm}} est restreint pour les utilisateurs externes.</dd>

<dt>Audit</dt>
<dd>Des journaux d'audit sont créés pour toutes les tentatives d'authentification, réussies ou non, des développeurs d'application. Des journaux d'audit
sont également créés pour les accès privilégiés aux systèmes Linux qui hébergent les conteneurs où sont exécutées les applications
{{site.data.keyword.Bluemix_notm}}.</dd>

<dt>Protection des données</dt>
<dd> L'ensemble du trafic {{site.data.keyword.Bluemix_notm}} passe par les produits IBM WebSphere® DataPower® SOA Appliances, qui offrent des fonctions de proxy inverse, de terminaison SSL et
d'équilibrage de charge.
Les méthodes HTTP suivantes sont autorisées :
<ul>
<li>DELETE</li>
<li>GET</li>
<li>HEAD</li>
<li>OPTIONS</li>
<li>POST</li>
<li>PUT</li>
<li>TRACE</li>
</ul>
 Le délai d'attente d'inactivité HTTP est de 2 minutes.</dd>
<dd>Les en-têtes suivants sont remplis par DataPower :
<dl>
<dt>$wsis</dt>
<dd>true si la connexion côté client est sécurisée (HTTPS) ; false dans le cas contraire.</dd>
<dt>$wssc</dt>
<dd>Un des schémas de connexion client suivants : https, http, ws ou wss.</dd>
<dt>$wssn</dt>
<dd>Nom d'hôte envoyé par le client.</dd>
<dt>$wssp</dt>
<dd>Port du serveur sur lequel le client se connecte.</dd>
<dt>x-client-ip</dt>
<dd>Adresse IP du client.</dd>
<dt>x-forwarded-proto</dt>
<dd>Un des schémas de connexion client suivants : https, http, ws ou wss.</dd>
</dl>
</dd>

<dt>Pratiques de développement sécurisé</dt>
<dd> Pour les environnements {{site.data.keyword.Bluemix_notm}} public et dédié, des analyses régulières permettant de détecter les vulnérabilités
en matière de sécurité sont effectuées sur divers composants {{site.data.keyword.Bluemix_notm}} avec IBM Security AppScan® Dynamic
Analyzer. La modélisation des
menaces et des tests de pénétration sont effectués pour détecter et traiter les vulnérabilités potentielles pour tous les types de déploiement
{{site.data.keyword.Bluemix_notm}}. De plus, les développeurs d'applications peuvent utiliser le service AppScan Dynamic Analyzer afin de sécuriser
leurs applications Web qui sont déployées dans {{site.data.keyword.Bluemix_notm}}.</dd>
</dl>

### Sécurité de l'infrastructure

{{site.data.keyword.Bluemix_notm}} s'appuie sur Cloud Foundry et fournit une base robuste pour l'exécution de vos applications. Dans cette architecture, plusieurs composants gèrent la sécurité et l'isolement. De
plus, la gestion des modifications ainsi que des procédures de sauvegarde et de restauration sont implémentées pour assurer l'intégrité et la disponibilité.

<dl>
<dt>Séparation des environnements</dt>
<dd> Pour l'environnement {{site.data.keyword.Bluemix_notm}} public, les environnements de développement et de production sont séparés afin d'améliorer la stabilité et la sécurité des applications.</dd>

<dt>Pare-feux</dt>
<dd> Des pare-feux sont en place pour restreindre l'accès au réseau {{site.data.keyword.Bluemix_notm}}. Pour l'environnement
{{site.data.keyword.Bluemix_notm}} local, le pare-feu de votre société sépare le reste de votre réseau de votre
instance {{site.data.keyword.Bluemix_notm}}.</dd>

<dt>Protection contre les intrusions</dt>
<dd>Les environnements {{site.data.keyword.Bluemix_notm}} public et dédié assurent la protection contre les intrusions pour détecter les menaces afin
qu'elles
puissent être traitées. Des règles de protection contre les intrusions sont activées dans les pare-feux.</dd>

<dt>Gestion des conteneurs d'applications sécurisée</dt>
<dd>Chaque application {{site.data.keyword.Bluemix_notm}} est isolée et s'exécute dans son propre conteneur, qui
possède des limites de ressources spécifiques pour le processeur, la mémoire et le disque.</dd>

<dt>Renforcement de la sécurité du système d'exploitation</dt>
<dd>Les administrateurs IBM renforcent le système d'exploitation et le réseau régulièrement à l'aide d'outils tels qu'IBM Endpoint Manager.</dd>
</dl>

### Sécurité opérationnelle

{{site.data.keyword.Bluemix_notm}} offre un environnement de sécurité opérationnelle robuste avec les contrôles suivants.

<dl>
<dt>Analyse de vulnérabilité</dt>
<dd>{{site.data.keyword.Bluemix_notm}} utilise Nessus, outil d'analyse de vulnérabilité de Tenable Network
Security, pour détecter les anomalies liées au réseau et aux configurations hôte.</dd>

<dt>Gestion des correctifs automatisés</dt>
<dd>Les administrateurs {{site.data.keyword.Bluemix_notm}} garantissent que les correctifs des
systèmes d'exploitation sont appliqués à une fréquence appropriée. Les correctifs automatisés sont activés avec IBM Endpoint Manager.</dd>

<dt>Analyse et consolidation des journaux d'audit</dt>
<dd>{{site.data.keyword.Bluemix_notm}} utilise les outils IBM Security QRadar® pour consolider les journaux Linux afin de surveiller l'accès privilégié sur les systèmes Linux. {{site.data.keyword.Bluemix_notm}} utilise également les outils SIEM (gestion des événements et des informations de sécurité) d'IBM QRadar pour surveiller les tentatives de connexion, réussies ou non, des développeurs d'applications.</dd>

<dt>Gestion de l'accès utilisateur</dt>
<dd>Dans {{site.data.keyword.Bluemix_notm}}, les instructions de répartition des tâches sont suivies pour affecter des privilèges d'accès
granulaire aux utilisateurs et pour assurer que les utilisateurs n'ont accès qu'aux éléments dont ils ont besoin pour accomplir leurs tâches selon le
principe du moindre privilège.

Dans les environnements {{site.data.keyword.Bluemix_notm}} dédié et local, les administrateurs désignés
peuvent
gérer les rôles et les droits pour les utilisateurs {{site.data.keyword.Bluemix_notm}} dans leur organisation dans la console d'administration. Voir
[Gestion de {{site.data.keyword.Bluemix_notm}}](/docs/admin/adminpublic.html#mng) pour des détails.
</dd>
</dl>

### Sécurité physique

Les environnements {{site.data.keyword.Bluemix_notm}} public et dédié s'appuient sur la topologie "un réseau dans le réseau" de {{site.data.keyword.BluSoftlayer}} en
matière de sécurité de réseau physique. Cette architecture permet de s'assurer que les systèmes sont accessibles uniquement au personnel autorisé. Pour l'environnement {{site.data.keyword.Bluemix_notm}} local, vous êtes en charge de la sécurité physique de
l'instance locale. Votre centre de données est sécurisé derrière le pare-feu de votre société.

Dans la topologie "un réseau dans le réseau" de {{site.data.keyword.BluSoftlayer}}, la couche réseau public gère le trafic public vers les sites Web hébergés ou les
ressources en
ligne. La
couche réseau privé permet une véritable gestion externe par un opérateur tiers autonome via des passerelles de réseau privé virtuel SSL, PPTP ou IPSec. La
couche réseau centre de données à centre de données offre une connectivité gratuite et sécurisée entre les serveurs hébergés dans des installations
{{site.data.keyword.BluSoftlayer}} distinctes.

Chaque centre de données {{site.data.keyword.BluSoftlayer}} est totalement sécurisé grâce à des contrôles qui répondent aux exigences standard de l'industrie et de la norme
SSAE 16, sans exception.

## Sécurité des données
{: #data-security}

Avec {{site.data.keyword.Bluemix_notm}},
la sécurisation des données contre l'accès non autorisé est le fruit d'une
collaboration entre {{site.data.keyword.Bluemix_notm}} et vous.

Les données qui sont associées à une application en cours d'exécution peuvent être dans l'un des trois états suivants : en transit, au repos et en cours d'utilisation.

<dl>
<dt>Données en transit</dt>
<dd>Il s'agit des données transférées entre des noeuds sur un réseau.</dd>

<dt>Données au repos</dt>
<dd>Il s'agit des données qui sont stockées.</dd>

<dt>Données en cours d'utilisation</dt>
<dd>Il s'agit des données qui ne sont pas stockées et qui sont utilisées sur un noeud final.</dd>
</dl>

Vous devez prendre en compte chaque type de données lorsque vous planifiez la sécurité des données.

La plateforme {{site.data.keyword.Bluemix_notm}} sécurise les données transférées en sécurisant l'accès de l'utilisateur final à
l'application via SSL sur le réseau, jusqu'à ce que les données atteignent IBM DataPower Gateway à la frontière du réseau interne de
{{site.data.keyword.Bluemix_notm}}. IBM DataPower Gateway sert de
proxy inverse et fournit la terminaison SSL. IPSEC est utilisé pour sécuriser les données qui transitent entre IBM DataPower Gateway et l'application.

La sécurité des données utilisées et des données au repos vous incombe lorsque vous développez votre application. Vous pouvez tirer profit de
plusieurs services liés aux données qui sont disponibles dans le catalogue {{site.data.keyword.Bluemix_notm}} pour traiter ces questions.

## Sécurité des applications {{site.data.keyword.Bluemix_notm}}
{: #application-security}

En tant que développeur, vous devez activer la configuration des paramètres de sécurité, y compris la protection des données d'application, pour vos applications exécutées sur {{site.data.keyword.Bluemix_notm}}.

Vous pouvez utiliser les fonctions de sécurité fournies par plusieurs services {{site.data.keyword.Bluemix_notm}} pour sécuriser vos applications. Tous les services {{site.data.keyword.Bluemix_notm}} qui sont produits par IBM suivent les pratiques de développement d'ingénierie sécurisée d'IBM.

**Remarque :** il se peut que certains services décrits ici ne soient pas applicables dans les instances
{{site.data.keyword.Bluemix_notm}} dédiées ou locales.

### Service SSO

IBM Single Sign On for {{site.data.keyword.Bluemix_notm}} est un service d'authentification reposant sur des règles qui fournit une fonction de connexion unique facile à intégrer pour les applications Node.js ou
Liberty for Java.. Pour permettre à
un développeur d'applications d'intégrer la fonction de connexion unique à une application, l'administrateur crée des instances de service et ajoute des
sources d'identité.

Le service Single Sign On prend en charge plusieurs sources d'identité dans lesquelles vos données d'identification utilisateur sont stockées :

<dl>
<dt>Entreprise SAML</dt>
<dd>Il s'agit d'un registre d'utilisateurs qui procède à un échange de jetons pour l'authentification.</dd>

<dt>Répertoire cloud</dt>
<dd>Il s'agit d'un registre d'utilisateurs qui est hébergé dans le cloud IBM.</dd>

<dt>Sources d'identité sociales</dt>
<dd> Il s'agit des registres d'utilisateurs qui sont gérés par Google, Facebook et LinkedIn.</dd>
</dl>

Pour plus d'informations, voir [Initiation à Single Sign On](/docs/services/SingleSignOn/index.html).

### Application Security on Cloud

Ce service fournit une analyse de sécurité des applications mobiles et Web et vous permet d'analyser le code source afin d'identifier d'éventuelles
vulnérabilités en matière de sécurité. Pour plus d'informations, voir [Initiation à Application Security on Cloud](/docs/services/ApplicationSecurityonCloud/index.html).

### Plug-in IBM UrbanCode pour le test de la sécurité des applications

Le plug-in IBM Application Security Testing for {{site.data.keyword.Bluemix_notm}} vous permet d'exécuter des analyses de sécurité pour vos
applications Web ou Android qui sont hébergées dans {{site.data.keyword.Bluemix_notm}}. Il est développé par la communauté IBM UrbanCode. Deploy Community, qui assure son support, sur la plateforme IBM Bluemix DevOps Services.

Pour plus d'informations, voir [IBM Application Security Testing for Bluemix ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://developer.ibm.com/urbancode/plugindoc/ibmucd/ibm-application-security-testing-bluemix/1-0/){: new_window}. 

### dashDB

Le service dashDB utilise un serveur LDAP imbriqué pour l'authentification d'utilisateur. La connexion entre les applications et la base de données est protégée par des certificats SSL. Ce service utilise la capacité de chiffrement native de DB2® pour chiffrer automatiquement votre base de données déployée et vos sauvegardes de base de
données. La rotation de clé principale automatique a lieu tous les 90 jours.

Pour plus d'informations, voir [Initiation à dashDB](/docs/services/dashDB/index.html).

### Secure Gateway

Le service Secure Gateway permet de connecter les applications {{site.data.keyword.Bluemix_notm}} de façon sécurisée à des emplacements
distants, sur site ou dans le cloud. Il assure la connectivité et établit un tunnel entre votre organisation {{site.data.keyword.Bluemix_notm}} et
l'emplacement distant auquel vous voulez vous connecter. Vous pouvez configurer et créer une passerelle sécurisée en utilisant l'interface utilisateur
{{site.data.keyword.Bluemix_notm}} ou un package d'API.

Pour plus d'informations, voir [Initiation à Secure Gateway](/docs/services/SecureGateway/secure_gateway.html).

### Gestion des événements et des informations de sécurité

Vous pouvez utiliser les outils SIEM (gestion des événements et informations de sécurité) pour analyser les alertes de sécurité dans les journaux d'application. L'un de ces outils est IBM Security QRadar&reg; SIEM, qui fournit la sécurité intérieure dans les environnements de cloud. Pour plus d'informations, voir [IBM QRadar Security Intelligence Platform ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](http://www-01.ibm.com/support/knowledgecenter/SS42VS/welcome?lang=en){: new_window}.
