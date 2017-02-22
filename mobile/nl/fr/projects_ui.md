---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Utilisation d'un module de démarrage d'interface utilisateur pour créer un projet
{: #projects_ui}

Vous pouvez utiliser un [module de démarrage pour l'interface utilisateur](starters.html#UI_Starter) dans le tableau de bord {{site.data.keyword.Bluemix}} Mobile afin de créer un projet dans l'environnement {{site.data.keyword.Bluemix_notm}}. Cette
procédure ne s'applique pas aux projets qui utilisent les modules de démarrage
pour le code. Pour obtenir les instructions relatives aux modules de démarrage
pour le code, voir [Création d'un projet avec
un module de démarrage pour le code](projects_code.html).
{:shortdesc}

Effectuez les étapes suivantes pour créer un projet avec un module
de démarrage pour l'interface utilisateur :

1. Créez un projet de tableau de bord Mobile dans {{site.data.keyword.Bluemix_notm}}.

 Après avoir sélectionné le catalogue Mobile, vous accédez à l'onglet
*Initiation*. Cet onglet décrit les modules de démarrage
sélectionnés que vous pouvez employer, ainsi que leurs différents modes
d'utilisation pour créer un projet en fonction du niveau d'assistance dont vous avez
besoin. Si vous souhaitez commencer avec un minimum d'aide, sélectionnez **Créer un projet**.

 Si vous disposez déjà de projets, vous pouvez sélectionner l'onglet
*Projets* dans l'onglet *Initiation*. Dans la vue
**Projets** du
tableau de bord {{site.data.keyword.Bluemix_notm}}
Mobile, vous pouvez sélectionner un projet à utiliser et employer des
*Actions* afin de supprimer un projet, télécharger son code ou
créer un nouveau projet. Si le projet a été créé à partir d'un module de
démarrage pour l'interface utilisateur, vous pouvez également l'ouvrir
directement dans le Générateur d'interface graphique à l'aide du menu *Actions*. 

	1. Dans la console {{site.data.keyword.Bluemix_notm}},
sélectionnez **Mobile** après avoir développé le menu et
affiché les trois lignes en regard du logo {{site.data.keyword.Bluemix_notm}}. 
	
	2. Sélectionnez **Créer un projet**. 

	  Vous pouvez aussi sélectionner l'onglet
**Projets** pour afficher les projets figurant déjà dans
votre environnement mobile et créer un nouveau projet en cliquant sur **Créer un projet**. 

	3. Sélectionnez le module de démarrage qui correspond le mieux au type
d'application que vous souhaitez créer, puis sélectionnez **Créer un projet**. Il
existe des **Modules de démarrage pour l'interface
utilisateur** et des **Modules de démarrage pour le code**. Pour
plus d'informations sur les modules de démarrage et leur utilisation, voir
[Modules de démarrage](starters.html). 
	
	4. Entrez le nom de votre projet et sélectionnez
**Créer**.
	
2. Effectuez vos sélections dans l'écran **Présentation du projet**.  L'écran **Présentation du projet** affiche des
informations sur votre projet et sur les fonctionnalités facultatives que vous pouvez lui ajouter, telles que {{site.data.keyword.mobilepushshort}}.  

	1. Facultatif : sélectionnez **Ajouter** pour
ajouter une des fonctions répertoriées à votre projet. Editez le **Nom
du service** et cliquez sur **Créer**. Lorsque vous ajoutez des services au projet, vous établissez une connexion avec la page {{site.data.keyword.Bluemix_notm}} pour ce service. Configurez le service en fournissant les informations requises pour le service.
	
	2. Facultatif : répétez l'étape *a* pour toute autre
fonction supplémentaire que vous souhaitez ajouter au projet. 

3. Concevez votre interface utilisateur à l'aide du Générateur
d'interface graphique.

   **Remarque :** Vu que l'interface utilisateur des modules de démarrage du code n'est pas personnalisable, l'onglet
*Conception*
n'est pas disponible.

    1. Sélectionnez **Générateur
d'interface graphique** dans le menu de navigation pour personnaliser
la conception de votre application. 
	
		**Astuce :** Pour afficher un aperçu rapide du Générateur d'interface graphique, sélectionnez **Me montrer comment cela fonctionne** dans la navigation après avoir sélectionné le Générateur d'interface graphique. 
	
	2. Personnalisez la présentation de votre application dans
l'onglet **Ecrans**.
	
	3. Ajoutez de nouveaux écrans en sélectionnant **Ajouter des écrans**. Attribuez un nom à vos nouveaux écrans pour vous y référer plus
facilement dans votre application. Vous pouvez sélectionnez les types d'écran suivants : 
		* Menu
		* Liste
		* Carte
		* Personnalisé 
		* Graphique
		
	4. Vous pouvez modifier le titre du menu de votre application en
sélectionnant la zone de texte *Menu* dans la section
**Présentation** de l'interface et en remplaçant son contenu
dans la zone **Données à afficher**. Visualisez vos mises à
jour dans la section du périphérique simulé.
	
		Mettez à jour les éléments de conception en sélectionnant chacun
d'entre eux et en mettant à jour leurs informations, si nécessaire. Ces
éléments s'affichent sous forme d'arborescence. Vous pouvez modifier l'ordre
d'affichage des éléments du menu en les faisant glisser vers un nouvel
emplacement. Tous les enfants de l'élément sont également déplacés avec leur parent. Les
informations textuelles des éléments d'arborescence qui s'affichent dans les
zones **Données à afficher** font référence au contenu de la
feuille de calcul des sources de données. *Ne modifiez pas ces
éléments dans la vue **Conception**, car ils sont
remplacés par le contenu des Sources de données identifiées dans la vue
**Données**.* 
		
		Un élément identifié dans l'arborescence comme un
*Formulaire* est indépendant et ne peut pas être modifié en ligne. Il
ne fait référence à aucune information issue d'une source de données.
	
	5. Sélectionnez **Données** dans la navigation pour afficher les données utilisées par l'application. Il existe des informations par défaut dans le modèle ; vous avez cependant la possibilité de modifier la source des données en sélectionnant **Création**. Vous
pouvez faire référence à plusieurs sources de données, il convient donc
d'indiquer un nom pour chacune d'entre elles. Vous pouvez sélectionner les
sources de données suivantes :
		* Cloud
		* Local
		* Cloudant
		* Google Sheets
		* Excel Online
		* Google Drive
	
		Vous pouvez également importer, exporter ou modifier le contenu du
tableau en le sélectionnant et en utilisant les différents boutons.
	     
		**Remarque :** Si vous importez des données qui ne correspondent pas à la structure des données par défaut,
activez le curseur *Remplacer le schéma*. Par exemple, dans le cas d'un fichier .csv qui
comporte moins de colonnes que les données fournies avec le module de démarrage.
		 
	6. Sélectionnez **Navigation** pour personnaliser les actions de navigation dans votre application. Cette action est facultative car les
actions de navigation pour beaucoup d'écrans sont créées automatiquement en fonction des relations entre les écrans. Vous pouvez changer l'écran cible en
sélectionnant d'abord l'écran ou la zone *depuis* lesquels vous désirez naviguer dans la liste des options de menu. Sélectionnez ensuite l'écran
*vers lequel vous désirez naviguer* dans la zone Ecran cible. 
		 
	7. Sélectionnez **Accès utilisateur** dans la
navigation afin de modifier les droits d'accès pour votre projet. Vous
pouvez activer et désactiver l'accès utilisateur à l'aide de l'interrupteur. Lorsque
l'accès utilisateur est activé, vous pouvez définir un délai d'expiration pour
les utilisateurs inactifs et les données d'identification des utilisateurs qui
peuvent accéder à l'application.
	
	8. Sélectionnez **Paramètres** dans le menu de
navigation pour modifier les informations générales relatives aux couleurs de
votre projet. Cet écran vous permet de saisir votre clé d'API Google, si elle
est requise pour les fonctions que vous avez ajoutées au projet. Il vous permet
aussi d'ajouter votre identificateur de bundle unique enregistré dans l'Apple
Store ou le Google Play Store.
	
		Si vous voulez ajouter le kit de développement de logiciels (SDK) IBM
MobileFirst Foundation au projet, placez l'interrupteur en position active.
		
	9. Si vous avez positionné l'interrupteur de manière à ajouter IBM MobileFirst Platform
Foundation à votre projet dans l'écran *Paramètres*, l'élément
**Foundation** apparaît dans la navigation. Sélectionnez
**Foundation** et indiquez les informations requises
spécifiques à IBM MobileFirst Platform Foundation.
	
	10. Sélectionnez **Publier** dans le menu de navigation afin d'entrer les informations finales permettant de créer votre application mobile. Vous pouvez entrer votre Identificateur du bundle pour iOS et l'identifiant d'application pour Android.
	
		Si vous créez une application iOS, vous devez vous procurer
votre Identificateur de bundle, votre certificat de distribution sous forme de
fichier `.p12` et votre Profil de mise à disposition sous forme de
fichier `.mobileprovision` auprès du portail de mise à disposition
Apple. Ces trois éléments doivent être créés en même temps et avec
le même ordinateur que celui que vous projetez d'utiliser pour publier votre
application mobile dans l'Apple Store. Le certificat de distribution et le
profil de mise à disposition doivent être basés sur l'identificateur de bundle. 	
4. Revenez à l'écran *Présentation du projet* pour
extraire le code de votre application et l'essayer ! Vous pouvez télécharger
le code directement pour les systèmes d'exploitation iOS et Android, ou scanner
un code QR pour Android. 


