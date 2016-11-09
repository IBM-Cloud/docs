---

copyright:
  years: 2015, 2016

---
{:shortdesc: .shortdesc}

# A propos de {{site.data.keyword.mobileanalytics_short}}  
{: aboutmobileanalytics}
Dernière mise à jour : 29 août 2016
{: .last-updated}

{: shortdesc}
Le service {{site.data.keyword.mobileanalytics_full}} fournit des connaissances essentielles en matière de performances et d'utilisation d'application pour les développeurs et les propriétaires d'applications mobiles. Avec {{site.data.keyword.mobileanalytics_short}}, les propriétaires et les développeurs d'applications peuvent mieux comprendre ce
qu'il se passe côté utilisateur, et peuvent utiliser les connaissances ainsi acquises pour créer des applications orientées utilisateurs et d'une
qualité exceptionnelle sur le marché des applications mobiles. 

{: #overview}  
Le service inclut la console {{site.data.keyword.mobileanalytics_short}} qui permet aux propriétaires et aux développeurs d'applications de surveiller les performances des applications mobiles, de consulter les statistiques d'utilisateur et d'effectuer des recherches dans les journaux de périphériques.  {{site.data.keyword.mobileanalytics_short}} fournit les logiciels SDK client pour iOS 8+ (Swift uniquement) et Android 4+.

<!-- Mobile Analytics Server SDKs - set of server SDKs to protect resources that are-->
<!--hosted on {{site.data.keyword.Bluemix_notm}}. Currently supported runtimes are-->
<!--Node.js and Java for Liberty.-->

Grâce au service {{site.data.keyword.mobileanalytics_short}}, vous pouvez :
<!-- and includes the following capabilities: -->
<!-- * Near real-time analytics for client activity. Exp -->
<!--* Network latency analytics. GA only -->
<!-- * Client log search and download. Exp -->
<!--* Server log search and download. GA only -->
<!-- Crash and stack trace search. Exp -->

<dl>
	<dt>Obtenir immédiatement des connaissances</dt>
		<dd>Vous pouvez afficher des mesures de performances et d'utilisation en temps réel.</dd>
	<dt>Effectuer une implémentation en quelques minutes</dt>
		<dd>Créez une instance de service dans {{site.data.keyword.Bluemix}}, ajoutez le logiciel SDK à votre projet et collez deux lignes de code dans votre application. Après cela, vous êtes prêt à collecter des douzaines de mesures prédéfinies.</dd>
	<!--<dt>Collect any data you want</dt>-->
		<!--<dd>Instrument apps with custom events, discover how users are interacting with your app, track purchases, and monitor app activity.  
</dd>-->
<dt>Visualiser d'un seul coup d'oeil les mesures pour toutes vos applications</dt>
	<dd>La console {{site.data.keyword.mobileanalytics_short}} propose des graphiques <!-- both --> prêts à l'emploi
<!--and custom-->, et il n'est plus nécessaire d'écrire des requêtes.</dd>
<dt>Vous concentrer sur ce qui est important pour vous</dt>
	<dd>Filtrez les mesures par heure, adaptateur, application, version d'application, système d'exploitation, version de système d'exploitation ou modèle de périphérique.</dd>
<dt>Détecter rapidement des problèmes</dt>
	<dd>Surveillez l'état des pannes. Définissez des déclencheurs d'alerte sur des mesures critiques et dirigez les alertes vers n'importe quel noeud final REST. </dd>
<dt>Identifier et résoudre des causes premières</dt>
	<dd>Utilisez la journalisation personnalisée dans votre application, téléchargez automatiquement les journaux et effectuez des recherches dans
ces derniers à partir de la console. Explorez en aval les événements de panne pour voir les traces de pile. </dd>
</dl>
 

## Utilisation de mesures et d'événements
{: #usingmetrics}

Les **mesures prédéfinies** vous permettent de répondre à des questions, telles que les suivantes :

* Quel est le nombre de nouveaux utilisateurs de mon application ?  
* Combien de personnes utilisent-elles activement mon application ?  
* A quelle fréquence les personnes utilisent-elles mon application ? 
* A quelle heure de la journée les personnes utilisent-elles mon application ?  
* Quels sont les modèles de périphérique préférés des utilisateurs de mon application ? 
* A quel moment dois-je déprécier le support des systèmes d'exploitation existants ? 
* Quelles sont les applications qui présentent des problèmes de performance ?  

<!--By adding your own **custom events** you can answer questions like:--> 

<!--* What features are used most and least?-->  
<!--* Where are users entering and leaving my app?-->  
<!--* What activities are users viewing most? --> 
<!--* Are users completing workflows in the app (for example, conversion funnels)? -->  

<!--Client-side logs and usage data are gathered automatically and sent to the Mobile Analytics -->
<!-- service on demand. Developers and -->
<!-- administrators can use the {{site.data.keyword.mobileanalytics_short}} service dashboard to view data that -->
<!-- is gathered by the client SDK. -->

<!--## Data visualization
{: data-visualization}

All data that is collected by the analytics service can be visualized through the {{site.data.keyword.mobileanalytics_short}} dashboard which is accessible from your {{site.data.keyword.Bluemix_notm}} dashboard by clicking your IBM {{site.data.keyword.mobileanalytics_short}} service tile instance. You can also create custom charts, based on data that is collected by the analytics service in the dashboard. In addition to an at-a-glance view of your mobile analytics, the analytics feature includes the capability to perform a raw search against client logs, captured client crash data, and any extra data that you explicitly provide through client API function calls that feed into the {{site.data.keyword.mobileanalytics_short}} service. -->

## Foire aux questions {{site.data.keyword.mobileanalytics_short}} 
{: #faq}

<dl>
	<dt>Présentation d'{{site.data.keyword.mobileanalytics_full}}</dt>
		<dd>{{site.data.keyword.mobileanalytics_full}} est un service qui fournit des données d'historique et en temps réel. Ces dernières indiquent les performances de vos applications mobiles et comment les applications mobiles sont utilisées.  Avec {{site.data.keyword.mobileanalytics_short}}, les développeurs et les propriétaires d'applications peuvent prendre des décisions en fonction des données en surveillant les tendances pour les utilisateurs actifs, les sessions, les plateformes mobiles et les pannes d'application. Vous pouvez aussi définir des alertes pour des mesures sélectionnées qui, une fois déclenchées, envoient des messages à un noeud final REST, comprenant un service push ou vos services de messagerie internes.</dd>
	<dt>Que puis-je faire avec {{site.data.keyword.mobileanalytics_short}} for {{site.data.keyword.Bluemix_notm}} bêta ?</dt>
		<dd>En tant que gestionnaire de produits pour application mobile, vous pouvez voir combien de personnes utilisent votre application (mesures d'utilisateurs) et à quel moment elles l'utilisent (mesures de sessions).  Ces informations sont présentées sous forme de séries temporelles et mises à jour en temps réel pour que vous puissiez constater l'effet des modifications que vous apportez à votre application.  Vous pouvez procéder à un filtrage pour afficher des versions d'application ou des systèmes d'exploitation spécifiques afin de prendre des décisions relatives à la dépréciation ou à la hiérarchisation. </dd>
		<dd>En tant que spécialiste du marketing pour les applications mobiles, vous pouvez vous servir des mesures d'utilisateurs et de sessions pour surveiller l'engagement, gérer les résiliations et évaluer l'efficacité de l'effort de marketing pour vos applications mobiles en observant les changements au fil du temps et en établissant des corrélations avec vos dates d'événement.</dd>
		<dd>En tant que développeur d'applications mobiles, vous pouvez vous servir des mesures sur les pannes afin d'identifier et de résoudre les problèmes de performance des applications mobiles avant qu'ils ne gênent les utilisateurs et entachent la réputation de l'application. Vous pouvez surveiller le nombre de pannes et le taux de panne dans la console d'analyse et hiérarchiser les pannes affectant le plus d'utilisateurs. Vous pouvez définir des alertes pour envoyer des notifications ou effectuer des actions automatisées lorsque les pannes dépassent un seuil donné, et vous pouvez traiter les incidents en explorant les instances de panne afin d'afficher les journaux des périphériques et les traces de pile de l'application.</dd>
	<dt>Dois-je avoir des compétences d'analyste de données pour utiliser Mobile Analytics ?</dt>
		<dd>Non, {{site.data.keyword.mobileanalytics_short}} propose une console d'analyse prête à l'emploi conçue pour les parties prenantes et les développeurs d'applications. Aucune compétence dans le domaine des requêtes n'est nécessaire.</dd>
	<dt>Puis-je effectuer des requêtes personnalisées sur mes données d'analyse ?</dt>
		<dd>{{site.data.keyword.mobileanalytics_short}} bêta ne permet pas d'effectuer des requêtes personnalisées, mais cette fonction est envisagée pour une version future.</dd>
	<dt>Comment puis-je connecter mon application à {{site.data.keyword.mobileanalytics_short}} ?</dt>
		<dd>[Téléchargez notre logiciel SDK open source pour iOS ou Android](install-client-sdk.html), ou utilisez l'[API REST](https://mobile-analytics-dashboard.stage1.ng.bluemix.net/analytics-service/) de {{site.data.keyword.mobileanalytics_short}} pour les autres plateformes. </dd>
	<dt>Dans quelles régions Bluemix {{site.data.keyword.mobileanalytics_short}} est-il disponible ?</dt>
		<dd>Au moment de la rédaction de ce document, Mobile Analytics était disponible dans les régions Sud des Etats-Unis et Royaume-Uni. Il sera disponible dans d'autres régions, mais le planning de mise à disposition n'a pas encore été défini.</dd>
	<dt>Combien coûte ce service ?</dt>
		<dd>Le service bêta est gratuit.</dd>
	<dt>Combien de temps mes données d'analyse sont-elles conservées ?</dt>
		<dd>Pour la version bêta, les données sont conservées au moins 30 jours.</dd>
	<dt>Au bout de combien de temps les données s'affichent-elles dans la console {{site.data.keyword.mobileanalytics_short}} ?</dt>
		<dd>Les données qui apparaissent dans la console {{site.data.keyword.mobileanalytics_short}} sont des données presque en temps réel, ce qui signifie qu'elles s'affichent quelques secondes à peine après les événements réels.</dd>
	<dt>Quelle est la différence entre {{site.data.keyword.mobileanalytics_full}} et l'analyse des applications mobiles disponible dans MobileFirst Platform Foundation ?</dt>
		<dd>Les concepts d'utilisateur et de session sont très similaires dans ces deux consoles, mais l'analyse proposée par MobileFirst Platform Foundation contient des mesures et des paramètres supplémentaires qui permettent aux clients de gérer leur propre cluster d'analyse sur site. De plus, la console d'analyse MobileFirst Platform Foundation présente des mesures pour les adaptateurs et les procédures d'adaptateur, alors que dans le service {{site.data.keyword.mobileanalytics_short}}, nous prévoyons d'intégrer ces mesures dans des tables et des graphiques de demandes réseau dans la version post bêta du service {{site.data.keyword.mobileanalytics_short}}.</dd>
	<dt>J'utilise MobileFirst Platform Foundation sur site pour développer mes applications, mais je ne veux pas héberger mon propre cluster d'analyse. Puis-je utiliser {{site.data.keyword.mobileanalytics_full}} à la place ?</dt>
		<dd>Oui. Vous avez deux options : si vous utilisez MobileFirst Platform Foundation 7.x ou 8.0 et que vos applications sont instrumentées avec des logiciels SDK de MobileFirst Platform, vous pouvez configurer votre serveur MobileFirst afin d'afficher les données d'analyse dans {{site.data.keyword.mobileanalytics_short}} for {{site.data.keyword.Bluemix_notm}}. Lisez l'article de blogue [Configuring Mobile Analytics and Mobile Foundation Bluemix services](https://mobilefirstplatform.ibmcloud.com/blog/2016/07/11/analytics-bm-service/) pour des détails. Vous pouvez aussi instrumenter vos applications avec le logiciel SDK de {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.mobileanalytics_short}} et afficher les données d'analyse directement dans le service {{site.data.keyword.mobileanalytics_short}}.</dd>
	<dt>J'essaye d'utiliser {{site.data.keyword.mobileanalytics_short}} et une zone blanche est affichée à la place de mes graphiques. Que se passe-t-il ?</dt>
		<dd>Vous utilisez probablement l'interface d'affichage classique pour {{site.data.keyword.Bluemix_notm}}. Celle-ci est dépréciée ; {{site.data.keyword.mobileanalytics_short}} bêta s'exécute dans la nouvelle interface {{site.data.keyword.Bluemix_notm}}. Si vous utilisez l'interface classique, l'en-tête {{site.data.keyword.Bluemix_notm}} comporte un lien permettant d'essayer la nouvelle interface {{site.data.keyword.Bluemix_notm}}. Cliquez dessus pour utiliser la nouvelle interface.</dd>
</dl>


# rellinks
 {:class="linklist"}

## Logiciel SDK
{: rellink-sdk}
<!-- Links to SDK download and SDK Developer Guide -->
* [Logiciel SDK Android](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)  
* [Logiciel SDK iOS](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core)  

<!-- {:elementKind="article" id="rellinks"} -->
