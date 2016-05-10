# Création d'applications mobiles
{: #mobile}
*Dernière mise à jour : 28 janvier 2016* 

Avec les services mobiles {{site.data.keyword.Bluemix}}, vous pouvez intégrer des services de cloud prégénérés, gérés et
évolutifs dans vos applications
mobiles sans recourir aux technologies de l'information. Ainsi, vous pouvez vous consacrer à la construction de vos applications mobiles au lieu de vous préoccuper des complexités liées à la gestion de
l'infrastructure de back end.

<table><caption>Tableau 1. Conteneur boilerplate MobileFirst&trade; Services Starter</caption>
<tr>
	<td>Chaque service mobile peut être utilisé indépendamment. Vous pouvez aussi utiliser les services ensemble pour en tirer le meilleur
profit. Pour commencer, utilisez {{site.data.keyword.mobilefirstbp}} Starter afin de créer votre application. Ce conteneur boilerplate :
		<ul>
			<li>Crée un contexte d'exécution Node.js avec un modèle d'application. Vous pouvez utiliser cette application pour fournir des fonctions côté serveur,
comme des API RESTful et des fichiers statiques. <!-- You can read more about operating this application in the Developing Mobile Backend section.--> </li>
			<li>
Met à disposition une instance de chaque service mobile {{site.data.keyword.Bluemix_notm}} et lie le service à l'application Node.js. </li>
		</ul>
	</td>
	<td> <img src="images/mf_boiler_icon.png" alt="Services mobiles Bluemix" width="500"> Conteneur boilerplate {{site.data.keyword.mobilefirstbp}} Starter </td>
</tr>
</table>

Après avoir utilisé le conteneur boilerplate {{site.data.keyword.mobilefirstbp}} Starter pour créer votre application, vous pouvez vous
procurer les exemples
HelloWorld pour chaque service ou commencer à instrumenter votre application existante pour l'utilisation des services
{{site.data.keyword.Bluemix_notm}}.


## Présentation des services
{: #services-overview}
Vous pouvez utiliser tous les services mobiles {{site.data.keyword.Bluemix_notm}} ensemble en vous servant du conteneur boilerplate {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.mobilefirstbp}} Starter ou utiliser chaque
service individuellement depuis le catalogue {{site.data.keyword.Bluemix_notm}}. Le diagramme ci-après met en évidence les composants des services
mobiles {{site.data.keyword.Bluemix_notm}}.

![Architecture des services mobiles {{site.data.keyword.Bluemix_notm}}](images/bms_architecture.jpg)

<table>
<caption>Tableau 2. {{site.data.keyword.Bluemix_notm}} et les systèmes d'entreprise</caption>
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
La section sur le développement des applications de back end mobiles présente l'exploitation de cette application plus en détail.</td>
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
<td><img src="images/catalog_icons-05.png" alt="{{site.data.keyword.amashort}} - icône du service"> <b>{{site.data.keyword.amashort}}</b><br/>Utilisez le service {{site.data.keyword.amafull}} pour protéger les applications Node.js et Java for Liberty applications hébergées sur {{site.data.keyword.Bluemix_notm}}. En instrumentant votre application mobile avec le logiciel SDK de
{{site.data.keyword.amashort}}, vous pouvez exiger des utilisateurs qu'ils se connectent pour accéder à Node.js ou aux services mobiles
{{site.data.keyword.Bluemix_notm}}. En plus de proposer des fonctions de sécurité, {{site.data.keyword.amashort}} recueille également des données d'analyse
pour que vous puissiez surveiller les performances de vos applications mobiles et collecter les journaux de client et les statistiques d'utilisation. </td>
<td valign="top"><b>Fournisseurs d'identité d'utilisateur</b> <br/>Vous pouvez utiliser les fournisseurs d'identité suivants : <ul><li>Facebook</li><li>Google</li></ul></td>
</tr>
<tr>
<td><img src="images/catalog_icons-09.png" alt="Icône du service Push Notifications">
<b>{{site.data.keyword.mobilepushshort}}</b><br/>Le service
{{site.data.keyword.mobilepushfull}} fournit une plateforme unifiée permettant d'envoyer et de gérer des notifications push ciblant les plateformes iOS et Android. Il gère le
mappage des utilisateurs de votre application à leurs périphériques ainsi que la plateforme des périphériques, et traite la distribution des
notifications
push aux périphériques. Avec ce service, vous pouvez envoyer des diffusions, des monodiffusions (en fonction de l'ID utilisateur ou de l'ID de
périphérique) et des notifications en fonction d'étiquettes (ou de rubriques) aux utilisateurs de votre application
mobile.</td>
<td valign="top"><b>Fournisseurs de service Push</b><ul><li>Apple Push Notifications Service</li><li>Google Cloud Messaging</li></ul></td>
</tr>
<tr>
<td><img src="images/cloudant64.png" alt="Icône du service Cloudant"><b>Cloudant NoSQLDB</b><br/> Cloudant est une base de données NoSQL sous forme
de service (DBaaS). Elle a été conçue pour la mise à l'échelle mondiale, l'exécution continue et le
traitement d'un large éventail de types de données tels que JSON, en texte intégral et géospatiales. </td>
<td>Cloudant.com</td>
</tr>
</table>
