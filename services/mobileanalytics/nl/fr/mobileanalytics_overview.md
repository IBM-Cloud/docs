---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-13"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# A propos de {{site.data.keyword.mobileanalytics_short}}  
{: aboutmobileanalytics}

{: shortdesc}
Le service {{site.data.keyword.mobileanalytics_full}} fournit des connaissances essentielles en matière de performances et d'utilisation d'application pour les développeurs et les propriétaires d'applications mobiles. Avec {{site.data.keyword.mobileanalytics_short}}, les propriétaires et les développeurs d'applications peuvent mieux comprendre ce qu'il se passe côté utilisateur, et peuvent utiliser les connaissances ainsi acquises pour créer des applications orientées utilisateurs et d'une qualité exceptionnelle sur le marché des applications mobiles. 

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
	<dt>Collectez les données de votre choix</dt>
		<dd>Instrumenter les applications avec des événements personnalisés, découvrir comment les utilisateurs interagissent avec votre
application, suivre les achats, et surveiller l'activité de l'application.  
</dd>
<dt>Visualiser d'un seul coup d'oeil les mesures pour toutes vos applications</dt>
	<dd>La console {{site.data.keyword.mobileanalytics_short}} propose des graphiques <!-- both --> prêts à l'emploi
<!--and custom-->, et il n'est plus nécessaire d'écrire des requêtes.</dd>
<dt>Vous concentrer sur ce qui est important pour vous</dt>
	<dd>Filtrez les mesures par heure, adaptateur, application, version d'application, système d'exploitation, version de système d'exploitation ou modèle de périphérique.</dd>
<dt>Détecter rapidement des problèmes</dt>
	<dd>Surveillez l'état des pannes. Définissez des déclencheurs d'alerte sur des mesures critiques et dirigez les alertes vers n'importe quel noeud final REST. </dd>
<dt>Identifier et résoudre des causes premières</dt>
	<dd>Utilisez la journalisation personnalisée dans votre application, téléchargez automatiquement les journaux et effectuez des recherches dans ces derniers à partir de la console. Explorez en aval les événements de panne pour voir les traces de pile. </dd>
</dl>
 

## Utilisation de mesures et d'événements
{: #usingmetrics}

Les **mesures prédéfinies** vous permettent de répondre à des questions, telles que les suivantes :

* Quel est le nombre de nouveaux utilisateurs de mon application ?  
* Combien de personnes utilisent-elles activement mon application ?  
* A quelle fréquence les personnes utilisent-elles mon application ? 
* A quelle heure de la journée les personnes utilisent-elles mon application ?  
* Quels sont les modèles de périphérique préférés des utilisateurs de mon application ? 
* Quand cesser la prise en charge de systèmes d'exploitation surannés ? 
* Quelles sont les applications qui présentent des problèmes de performance ?  

En ajoutant vos propres **événements personnalisés**, vous pouvez répondre à des questions telles que : 

* Quelles sont les fonctions les plus utilisées, et celles les moins utilisées ?  
* A quel endroit les utilisateurs entrent-ils et quittent-ils mon application ?  
* Quelles sont les activités que visualisent le plus les utilisateurs ?  
* les utilisateurs suivent-ils jusqu'au bout les flux de travaux (par exemple, les entonnoirs de conversion) ?   

Les journaux et données d'utilisation côté client sont collectés automatiquement et envoyées à la demande au service Mobile Analytics. Les développeurs et les administrateurs peuvent utiliser le tableau de bord du service {{site.data.keyword.mobileanalytics_short}} pour afficher les données qui sont collectées par le logiciel SDK du client.

## Visualisation de données
{: data-visualization}

Toutes les données collectées par le service d'analyse peuvent être visualisées via le tableau de bord
{{site.data.keyword.mobileanalytics_short}} (accessible depuis votre tableau de bord
{{site.data.keyword.Bluemix_notm}} en cliquant sur la vignette de votre instance de service IBM {{site.data.keyword.mobileanalytics_short}}.
<!--You can also create custom charts, based on data that is collected by the analytics service in the dashboard.--> Outre la possibilité addition
d'examiner en un clin d'oeil les analyses de votre périphérique mobile, la fonction d'analyse permet d'effectuer une recherche sommaire dans les journaux
client, dans les captures des données de pannes et dans les données supplémentaires éventuelles que vous soumettez via des appels de fonction d'API
client qui alimentent le service {{site.data.keyword.mobileanalytics_short}}. 

## Foire aux questions {{site.data.keyword.mobileanalytics_short}} 
{: #faq}

<dl>
	<dt>Présentation d'{{site.data.keyword.mobileanalytics_full}}</dt>
		<dd>{{site.data.keyword.mobileanalytics_full}} est un service qui fournit des données d'historique et en temps réel. Ces dernières indiquent les performances de vos applications mobiles et comment les applications mobiles sont utilisées. Avec {{site.data.keyword.mobileanalytics_short}}, les développeurs et les propriétaires d'applications peuvent prendre des décisions en fonction des données en surveillant les tendances pour les utilisateurs actifs, les sessions, les plateformes mobiles et les pannes d'application. Vous pouvez aussi définir des alertes pour des mesures sélectionnées qui, une fois déclenchées, envoient des messages à un noeud final REST, comprenant un service push ou vos services de messagerie internes.</dd>
	<dt>Que puis-je faire avec {{site.data.keyword.mobileanalytics_short}} for {{site.data.keyword.Bluemix_notm}} ?</dt>
		<dd>En tant que gestionnaire de produits pour application mobile, vous pouvez voir combien de personnes utilisent votre application (mesures d'utilisateurs) et à quel moment elles l'utilisent (mesures de sessions). Ces informations sont présentées sous forme de séries temporelles et mises à jour en temps réel pour que vous puissiez constater l'effet des modifications que vous apportez à votre application. Vous pouvez procéder à un filtrage pour afficher des versions d'application ou des systèmes d'exploitation spécifiques afin de prendre des décisions relatives à la dépréciation ou à la hiérarchisation. </dd>
		<dd>En tant que spécialiste du marketing pour les applications mobiles, vous pouvez vous servir des mesures d'utilisateurs et de sessions pour surveiller l'engagement, gérer les résiliations et évaluer l'efficacité de l'effort de marketing pour vos applications mobiles en observant les changements au fil du temps et en établissant des corrélations avec vos dates d'événement.</dd>
		<dd>En tant que développeur d'applications mobiles, vous pouvez vous servir des mesures sur les pannes afin d'identifier et de résoudre les problèmes de performance des applications mobiles avant qu'ils ne gênent les utilisateurs et entachent la réputation de l'application. Vous pouvez surveiller le nombre de pannes et le taux de panne dans la console d'analyse et hiérarchiser les pannes affectant le plus d'utilisateurs. Vous pouvez définir des alertes pour envoyer des notifications ou effectuer des actions automatisées lorsque les pannes dépassent un seuil donné, et vous pouvez traiter les incidents en explorant les instances de panne afin d'afficher les journaux des périphériques et les traces de pile de l'application.</dd>
	<dt>Dois-je avoir des compétences d'analyste de données pour utiliser Mobile Analytics ?</dt>
		<dd>Non, {{site.data.keyword.mobileanalytics_short}} propose une console d'analyse prête à l'emploi conçue pour les parties prenantes et les développeurs d'applications. Aucune compétence dans le domaine des requêtes n'est nécessaire.</dd>
	<dt>Puis-je effectuer des requêtes personnalisées sur mes données d'analyse ?</dt>
		<dd>{{site.data.keyword.mobileanalytics_short}} ne permet pas d'effectuer des requêtes personnalisées, mais cette fonction est envisagée pour une version future.</dd>
	<dt>Comment puis-je connecter mon application à {{site.data.keyword.mobileanalytics_short}} ?</dt>
		<dd>[Téléchargez notre logiciel SDK open source pour iOS ou Android](install-client-sdk.html), ou utilisez l'[API REST](https://mobile-analytics-dashboard.{DomainName}/analytics-service/) de {{site.data.keyword.mobileanalytics_short}} pour les autres plateformes. </dd>
	<dt>Dans quelles régions Bluemix {{site.data.keyword.mobileanalytics_short}} est-il disponible ?</dt>
		<dd>Actuellement, Mobile Analytics est disponible dans le Sud des Etats-Unis et au Royaume-Uni. Il sera disponible dans d'autres régions, mais le planning de mise à disposition n'a pas encore été défini.</dd>
	<dt>Combien coûte ce service ?</dt>
		<dd>Les 100 premiers millions d'événements qui sont collectés chaque mois sont gratuits, ensuite les événements coûtent 1 $ par million d'événements.</dd>
	<dt>Qu'est-ce qu'un événement ?</dt>
		<dd>Les événements actuellement signalés incluent le début de session d'application, la fin de session d'application (y compris le blocage d'application), les notifications d'alerte et les entrées de journal.</dd>
	<dt>Comment puis-je estimer le coût mensuel du service ?</dt>
		<dd>Étant donné que le prix dépend du nombre d'événements envoyés au service par compte client, estimer les prix revient à estimer les événements.  
<p>
Le prix facturé est la somme des événements de toutes les applications que vous avez connectées à {{site.data.keyword.mobileanalytics_short}}. Pour une application donnée, le nombre d'événements dépend du degré d'instrumentation que vous avez implémenté dans l'application, du nombre d'utilisateurs et de l'activité des utilisateurs.   
</p>
<p>
Utilisez cette formule pour estimer l'utilisation :
événements par mois par application = (utilisateurs par jour) (sessions par utilisateur par jour) (jours par mois) (événements par session)
</p>
<p>
Les événements par session peuvent varier considérablement de 2 à plusieurs centaines, selon les appels réseau, les analyses personnalisées, les captures de journaux et les définitions d'alertes que le développeur a configurés dans l'application.
</p>
	<dt>Combien de temps mes données d'analyse sont-elles conservées ?</dt>
		<dd>Les données sont conservées au moins 30 jours.</dd>
	<dt>Au bout de combien de temps les données s'affichent-elles dans la console {{site.data.keyword.mobileanalytics_short}} ?</dt>
		<dd>Les données qui apparaissent dans la console {{site.data.keyword.mobileanalytics_short}} sont des données presque en temps réel, ce qui signifie qu'elles s'affichent quelques secondes à peine après les événements réels.</dd>
	<dt>Quelle est la différence entre {{site.data.keyword.mobileanalytics_full}} et l'analyse des applications mobiles disponible dans MobileFirst Platform Foundation ?</dt>
		<dd>Les concepts d'utilisateur et de session sont très similaires dans ces deux consoles, mais l'analyse proposée par MobileFirst Platform Foundation contient des mesures et des paramètres supplémentaires qui permettent aux clients de gérer leur propre cluster d'analyse sur site. De plus, la console d'analyse MobileFirst Platform Foundation décompose les métriques des adaptateurs et des procédures de l'adaptateur, alors que dans le service {{site.data.keyword.mobileanalytics_short}}, ces métriques sont intégrées dans les graphiques et les tableaux de demandes de réseau.</dd>
	<dt>J'utilise MobileFirst Platform Foundation sur site pour développer mes applications, mais je ne veux pas héberger mon propre cluster d'analyse. Puis-je utiliser {{site.data.keyword.mobileanalytics_full}} à la place ?</dt>
		<dd>Oui. Vous avez deux options : si vous utilisez MobileFirst Platform Foundation 7.x ou 8.0 et que vos applications sont instrumentées avec des logiciels SDK de MobileFirst Platform, vous pouvez configurer votre serveur MobileFirst afin d'afficher les données d'analyse dans {{site.data.keyword.mobileanalytics_short}} for {{site.data.keyword.Bluemix_notm}}. Lisez les articles du blogue [Configuring Mobile Analytics and Mobile Foundation Bluemix services ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://mobilefirstplatform.ibmcloud.com/blog/2016/07/11/analytics-bm-service/){: new_window} pour plus de détails. Vous pouvez aussi instrumenter vos applications avec le logiciel SDK de {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.mobileanalytics_short}} et afficher les données d'analyse directement dans le service {{site.data.keyword.mobileanalytics_short}}.</dd>
	<!-- <dt>My instance of  {{site.data.keyword.mobileanalytics_short}} does not look like the screen shots in the catalog. What's going on?</dt> -->
		<!-- <dd>Most likely you are using the Classic view interface for {{site.data.keyword.Bluemix_notm}}. Classic view is deprecated, so {{site.data.keyword.mobileanalytics_short}} runs best in the new {{site.data.keyword.Bluemix_notm}} interface. If you are in Classic view, you will see a link in the {{site.data.keyword.Bluemix_notm}} header that says <strong>Try the new {{site.data.keyword.Bluemix_notm}}</strong>. Click that link to use the new interface.</dd> -->
</dl>


# rellinks
 {:class="linklist"}

## Logiciel SDK
{: rellink-sdk}
<!-- Links to SDK download and SDK Developer Guide -->
* [Logiciel SDK Android ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window} 
* [Logiciel SDK iOS ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core){: new_window}

<!-- {:elementKind="article" id="rellinks"} -->
