---

copyright:
  years: 2016, 2017
lastupdated: "2016-12-16"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Utilisation d'un module de démarrage de code pour créer un projet
{: #projects_code}

Vous pouvez utiliser un [module de démarrage pour le code](starters.html#Code_Starter) dans le tableau de bord {{site.data.keyword.Bluemix}} Mobile afin de créer un projet dans l'environnement {{site.data.keyword.Bluemix_notm}}. Cette procédure ne s'applique pas
aux projets qui utilisent les modules de démarrage pour l'interface utilisateur. Pour obtenir les instructions relatives aux modules de démarrage pour l'interface utilisateur, voir [Création d'un projet avec un  module de démarrage pour l'interface utilisateur](projects_ui.html). 
{:shortdesc}

Effectuez les étapes suivantes pour créer un projet avec un module de démarrage pour le code :

1. Créez un projet de tableau de bord Mobile dans {{site.data.keyword.Bluemix_notm}}.

 Après avoir sélectionné le catalogue Mobile, vous accédez à l'onglet *Initiation*. Cet onglet décrit les modules de démarrage sélectionnés que vous pouvez employer, ainsi que leurs différents modes d'utilisation pour créer un projet en fonction du niveau d'assistance dont vous avez besoin. Si vous souhaitez commencer, sélectionnez **Créer un projet**.

 Si vous disposez déjà de projets, vous pouvez démarrer avec l'onglet *Projets* déjà sélectionné. Dans la vue **Projets** du tableau de bord {{site.data.keyword.Bluemix_notm}} Mobile, vous pouvez sélectionner un projet à utiliser et employer des *Actions* afin de supprimer un projet, télécharger son code ou créer un nouveau projet.

	1. Dans la console {{site.data.keyword.Bluemix_notm}}, sélectionnez **Mobile** après avoir développé le menu et affiché les trois lignes en regard du logo {{site.data.keyword.Bluemix_notm}}. 
	
	2. Sélectionnez **Créer un projet**. 

	  Vous pouvez aussi sélectionner l'onglet
**Projets** pour afficher les projets figurant déjà dans
votre environnement mobile et créer un nouveau projet en cliquant sur
**Créer un projet**.

	3. Cliquez sur **Modules de démarrage pour le code**.  

	4. Sélectionnez le module de démarrage qui correspond le mieux au type
d'application que vous souhaitez créer, puis sélectionnez **Créer un
projet**. Il existe des **Modules de démarrage pour
l'interface utilisateur** et des **Modules de démarrage pour
le code**. Pour plus d'informations sur les modules de démarrage et
leur utilisation, voir [Modules de démarrage](starters.html). 
	
	5. Entrez le nom de votre projet et sélectionnez
**Créer**.
	
2. Effectuez vos sélections dans l'écran **Présentation du projet**.  L'écran **Présentation du projet**
affiche des informations sur votre projet et sur les services facultatifs que vous pouvez lui ajouter, tels que {{site.data.keyword.mobilepushshort}} et
Authentication.  

	1. Facultatif : sélectionnez **Ajouter** pour
ajouter un des services répertoriés à votre projet. Editez le **Nom
du service** et cliquez sur **Créer**. Lorsque vous ajoutez des services au projet, vous établissez une connexion avec la page {{site.data.keyword.Bluemix_notm}} pour ce service. Configurez le service en fournissant les informations requises pour le service.
	
	2. Facultatif : répétez l'étape *a* pour toute autre
fonction supplémentaire que vous souhaitez ajouter au projet.

3. Facultatif : Sélectionnez **Données** pour connecter une base de données Cloudant NoSQL ou un service Object Storage.
	1. Cliquez sur **Créer** pour configurer une nouvelle base de données Cloudant NoSQL ou un service Object Storage.
	
	Remarque : Si vous créez une instance du service Object Storage, vous êtes dirigé hors du projet pour créer ce service et lui ajouter les données
d'identification
requises. Revenez au projet après avoir créé cette instance de service et sélectionnez **Ajouter un projet existant** pour connecter le
service au projet.
	
	Si vous disposez d'une instance existante qui n'est pas encore connectée à un autre projet et que vous désirez la connecter à celui-ci,
sélectionnez **Ajouter un  projet existant**. 
	
	2. Vérifiez que la vignette de la base de données Cloudant NoSQL ou du service Object Storage auquel vous vous êtes connecté est affichée sur l'onglet Données
de votre projet.

4.  Téléchargez votre projet et terminez la configuration.

    1. Cliquez sur **Télécharger le code** et
sélectionnez votre langage préféré.
   
    2. Procédez à l'extraction de l'archive et affichez le fichier
`README.md` dans un afficheur Markdown afin de terminer la
configuration.

5.  Essayez votre application ! 


