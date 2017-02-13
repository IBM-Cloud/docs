---

copyright:
  years: 2015, 2017
lastupdated: "2016-10-19"

---

# Création d'applications mobiles depuis le conteneur boilerplate {{site.data.keyword.mobilefirstbp}} Starter
{: #try_mobile}

Vous pouvez utiliser chacun des services {{site.data.keyword.Bluemix}} Mobile indépendamment. Il vous est aussi possible de les utiliser ensemble, avec le conteneur boilerplate {{site.data.keyword.mobilefirstbp}} Starter, pour en tirer le meilleur
profit.

Pour commencer, utilisez {{site.data.keyword.mobilefirstbp}} Starter afin de créer votre application. Le conteneur boilerplate vous permet de réaliser les actions suivantes :

* Création d'un contexte d'exécution Node.js avec un modèle d'application. Vous pouvez utiliser cette application pour fournir des fonctions côté serveur,
comme des API RESTful et des fichiers statiques.<!-- You can read more about operating this application in the Developing Mobile Backend section.-->
* Mise à disposition d'une instance de chaque service {{site.data.keyword.Bluemix_notm}} Mobile et liaison du service à l'application Node.js.

<!--
<img src="images/mf_boiler_icon.png" alt="Bluemix mobile services" width="500"> {{site.data.keyword.mobilefirstbp}} Starter boilerplate
-->

Après avoir utilisé le conteneur boilerplate {{site.data.keyword.mobilefirstbp}} Starter pour créer votre application, vous pouvez vous
procurer les exemples Hello Bluemix pour chaque service ou commencer à instrumenter votre application existante pour l'utilisation des services {{site.data.keyword.Bluemix_notm}}.


## Présentation des services
{: #services-overview}
Vous pouvez utiliser tous les services {{site.data.keyword.Bluemix_notm}} Mobile ensemble en vous servant du conteneur boilerplate {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.mobilefirstbp}} Starter ou utiliser chaque service individuellement depuis le catalogue {{site.data.keyword.Bluemix_notm}}. Le diagramme ci-après met en évidence les composants des services {{site.data.keyword.Bluemix_notm}} Mobile.

![Architecture des services mobiles {{site.data.keyword.Bluemix_notm}}](images/bms_architecture.jpg)

<table summary="Ce tableau décrit les services {{site.data.keyword.Bluemix_notm}} Mobile">
<caption>Tableau 1. {{site.data.keyword.Bluemix_notm}} et les systèmes d'entreprise</caption>
<th>{{site.data.keyword.Bluemix_notm}}</th>
<th>Systèmes d'entreprise</th>
<tr>
<td> <img src="images/i_js_64.png" alt="Icône de contexte d'exécution Node.js"><b>Node.js</b> <br/> Un contexte d'exécution Node.js qui héberge un
modèle d'application est fourni dans le conteneur boilerplate {{site.data.keyword.mobilefirstbp}} Starter. Vous pouvez utiliser le modèle d'application afin de mettre à
disposition des fonctions côté serveur, comme des API RESTful et des fichiers statiques. <br/>Par exemple, vous pouvez étendre l'application Node.js
pour un traitement logique personnalisé ou pour la connexion à des API REST dans l'infrastructure existante de votre société. Chaque application que vous
créez dans {{site.data.keyword.Bluemix_notm}} possède un ID d'application unique. Votre application mobile utilise cet ID avec le logiciel SDK afin d'accéder aux services qui
lui sont associés. L'ID d'application est utilisé par la plateforme comme contexte pour les fonctions communes, telles que la mesure et la
journalisation.
<!--You can read more about operating this application in the "Developing Mobile Backend" section.--></td>
<td valign="top"><b>Fournisseur d'informations</b> <br/>Vous pouvez utiliser un contexte d'exécution Node.js hébergé dans {{site.data.keyword.Bluemix_notm}} pour vous connecter
à tout type de fournisseur d'informations :
<ul>
	<li>Un système de back end d'entreprise</li>
	<li>Une base de données </li>
	<li>Un autre service tiers hébergé</li>
</ul>
</td>
</tr>
<tr>
<td><img src="images/authentication_icon.png" alt="{{site.data.keyword.amashort}} - icône du service"> <b>{{site.data.keyword.amashort}}</b><br/>Utilisez le service {{site.data.keyword.amafull}} pour protéger les applications Node.js et Java for Liberty applications hébergées sur {{site.data.keyword.Bluemix_notm}}. En instrumentant votre application mobile avec le logiciel SDK {{site.data.keyword.amashort}}, vous pouvez demander aux utilisateurs qu'ils se connectent pour accéder à Node.js ou aux services {{site.data.keyword.Bluemix_notm}} Mobile. <!-- In addition to security capabilities, {{site.data.keyword.amashort}} also gathers analytics data, so that you can monitor your mobile application performance and collect client logs and usage statistics.--> </td>
<td valign="top"><b>Fournisseurs d'identité d'utilisateur</b> <br/>Vous pouvez utiliser les fournisseurs d'identité suivants : <ul><li>Facebook</li><li>Google</li><li> Personnalisé </li></ul></td>
</tr>
<tr>
<td>Icône du service <img src="images/push_icon.png" alt="{{site.data.keyword.mobilepushshort}}">
<b>{{site.data.keyword.mobilepushshort}}</b><br/>Le service {{site.data.keyword.mobilepushfull}} fournit une plateforme unifiée permettant
d'envoyer et de gérer des notifications push ciblant les plateformes mobiles (iOS et Android), ainsi que les applications de navigateur Web. Ce
service gère le mappage des utilisateurs de votre application à leurs
périphériques, ainsi qu'à la plateforme des périphériques et aux navigateurs,
et traite la distribution des notifications push aux abonnés. Avec ce service,
vous pouvez envoyer des diffusions, des monodiffusions (en fonction de l'ID
utilisateur ou de l'ID de périphérique) et des notifications en fonction
d'étiquettes (ou de rubriques) à vos clients.</td>
<td valign="top"><b>Fournisseurs de service Push</b><ul><li>Apple Push Notifications Service</li><li>Firebase Cloud Messaging</li></ul></td>
</tr>
<tr>
<td><img src="images/cloudant64.png" alt="Icône du service Cloudant"><b>Cloudant NoSQLDB</b><br/> Cloudant est une base de données NoSQL sous forme
de service (DBaaS). Elle a été conçue pour la mise à l'échelle mondiale, l'exécution continue et le
traitement d'un large éventail de types de données tels que JSON, en texte intégral et géospatiales. </td>
<td>Cloudant.com</td>
</tr>
</table>
