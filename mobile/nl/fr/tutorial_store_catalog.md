---

copyright:
  years: 2016, 2017
lastupdated: "2016-12-15"

---
{:new_window: target="_blank"}

# Tutoriel - Module de démarrage pour l'interface utilisateur du
catalogue magasin
{: #tutorial_store_catalog}

Le module de démarrage pour l'interface utilisateur du catalogue
magasin {{site.data.keyword.Bluemix}} fournit une structure
d'applications de ventes de base que vous pouvez personnaliser, ainsi que des
points d'intégration pour chacun des services {{site.data.keyword.Bluemix_notm}} Mobile.


## Configuration requise
{: #tutorial_requirements}

* Un compte [Bluemix ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](http://bluemix.net "Icône de lien externe")


## Initiation
{: #tutorial_gs}

Pour être rapidement opérationnel avec le module de démarrage pour
l'interface utilisateur du catalogue magasin, procédez comme suit :

1. Créez un projet de tableau de bord Mobile dans
{{site.data.keyword.Bluemix_notm}}.

   1. Dans la page **Initiation** du tableau de bord
Mobile, cliquez sur **Créer un projet**.

      Vous pouvez également cliquer sur **Créer un
projet** dans la page **Projets**.

   2. Sélectionnez **Modules de démarrage pour l'interface
utilisateur**, si cette option n'est pas déjà sélectionnée.

   3. Sélectionnez **Catalogue magasin** et cliquez
sur **Créer un projet**.

   4. Entrez le nom de votre projet et cliquez sur
**Créer**.

2. Facultatif : Ajoutez la fonctionnalité {{site.data.keyword.mobilepushshort}}.

   1. Cliquez sur **Ajouter** pour **{{site.data.keyword.mobilepushshort}}** sur la page
**Présentation du projet**.

      Vous pouvez également cliquer sur **Créer** sur la page **{{site.data.keyword.mobilepushshort}}**.

   2. Entrez le nom de votre service et cliquez sur
**Créer**.

   3. Pour iOS, [configurez le service de notification push
d'Apple![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](/docs/services/mobilepush/t_push_provider_ios.html "Icône de lien externe"){: new_window}.

   4. Pour Android, [configurez Google Cloud Messaging
![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](/docs/services/mobilepush/t_push_provider_android.html "Icône de lien externe"){: new_window}.

3. Facultatif : ajoutez d'autres fonctionnalités.

   1. Cliquez sur **Ajouter** pour la fonctionnalité dans la page **Présentation du projet**.

   2. Entrez le nom de votre service et cliquez sur
**Créer**.

   3. Suivez les instructions fournies avec le service pour le configurer.

4. Concevez votre application.

   1. Sélectionnez **Générateur
d'interface graphique** dans le menu de navigation pour personnaliser
la conception de votre application.
   
		**Astuce :** Pour afficher un aperçu rapide du Générateur d'interface graphique, sélectionnez **Me montrer comment cela fonctionne** dans la navigation après avoir sélectionné le Générateur d'interface graphique.

   2. Sélectionnez l'onglet **Conception** dans la navigation.

      Il s'agit d'un espace de travail permettant de concevoir votre
application et de simuler son apparence.

   3. Si vous le souhaitez, ajoutez de nouveaux écrans en sélectionnant
**Ajouter des écrans**. Attribuez un nom à vos nouveaux écrans pour vous y référer plus
facilement dans votre application. De nouveaux écrans sont créés au même niveau que l'écran principal, quelle que soit votre sélection dans
l'arborescence. Vous pouvez sélectionnez les types d'écran suivants :
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
emplacement. Tous les enfants de l'élément sont également déplacés avec leur
parent. Les informations textuelles des éléments d'arborescence qui s'affichent
dans les zones **Données à afficher** font référence au
contenu de la feuille de calcul des sources de données. *Ne modifiez pas
ces éléments dans la vue **Conception**, car ils sont
remplacés par le contenu des Sources de données identifiées dans la vue
**Données**.*

		Un élément identifié dans l'arborescence comme un
*Formulaire* est indépendant et ne peut pas être modifié en ligne. Il ne fait référence à aucune information issue d'une source de données.

   5. Sélectionnez **Données** dans la navigation pour afficher les données utilisées par l'application. Il existe des informations par défaut dans le modèle ; vous avez cependant la possibilité de modifier la source des données en sélectionnant **Création**. Vous pouvez faire référence à plusieurs
sources de données, il convient donc d'indiquer un nom pour chacune d'entre
elles. Vous pouvez sélectionner les sources de données suivantes :
      * Cloud
      * Local
      * Cloudant
      * Google Sheets
      * Excel Online
      * Google Drive

      Vous pouvez également importer, exporter ou modifier le contenu
du tableau en le sélectionnant et en utilisant les différents boutons.

	  Remarque : Si vous importez des données qui ne correspondent pas à
la structure des données par défaut, activez le curseur de remplacement de
schéma. Par exemple, dans le cas d'un fichier .csv qui comporte moins de
colonnes que les données fournies avec le module de démarrage.
	  
   6. Sélectionnez **Navigation** pour personnaliser les actions de navigation dans votre application. Cette action est facultative car les
actions de navigation pour beaucoup d'écrans sont créées automatiquement en fonction des relations entre les écrans. Vous pouvez changer l'écran cible en
sélectionnant d'abord l'écran ou la zone *depuis* lesquels vous désirez naviguer dans la liste des options de menu. Sélectionnez ensuite l'écran
*vers lequel vous désirez naviguer* dans la zone Ecran cible. 

   7. Sélectionnez **Accès utilisateur** dans la
navigation afin de modifier les droits d'accès pour votre projet. Vous pouvez
activer et désactiver l'accès utilisateur à l'aide de l'interrupteur. Lorsque
l'accès utilisateur est activé, vous pouvez définir un délai d'expiration pour
les utilisateurs inactifs et les données d'identification des utilisateurs qui
peuvent accéder à l'application.

   8. Sélectionnez **Paramètres** dans le menu de
navigation pour modifier les informations générales relatives aux couleurs de
votre projet. Cet écran vous permet de saisir votre clé d'API Google, si elle
est requise pour les services que vous avez ajoutés au projet. Il vous permet
aussi d'ajouter votre identificateur de bundle unique enregistré dans l'Apple
Store ou le Google Play Store.

      Si vous voulez ajouter le kit de développement de logiciels (SDK)
IBM MobileFirst Foundation au projet, placez l'interrupteur en position active.

   9. Si vous avez positionné l'interrupteur de manière à ajouter IBM
MobileFirst Platform Foundation à votre projet dans l'écran
*Paramètres*, l'élément **Foundation** apparaît
dans la navigation. Sélectionnez **Foundation** et indiquez
les informations requises spécifiques à IBM MobileFirst Platform Foundation.

   10. Sélectionnez **Publier** dans le menu de navigation afin d'entrer les informations finales requises pour créer votre application mobile. Vous pouvez entrer votre Identificateur du bundle pour iOS et l'identifiant d'application pour Android.

       Si vous créez une application iOS, vous devez vous procurer
votre Identificateur de bundle, votre certificat de distribution sous forme de
fichier *.p12* et votre Profil de mise à disposition sous forme de
fichier *.mobileprovision* auprès du portail de mise à disposition
Apple. Ces trois éléments doivent être créés en même temps et avec le même
ordinateur que celui que vous projetez d'utiliser pour publier votre
application mobile dans l'Apple Store. Le certificat de distribution et le
profil de mise à disposition doivent être basés sur l'identificateur de bundle. 	

5. Téléchargez votre projet.

   1. Cliquez sur **Code** et sélectionnez votre
plateforme ou votre langage de programmation préféré.

   2. Pour Android, vous avez le choix parmi les options suivantes une
fois le code généré :

      * Télécharger le code

      * Télécharger le fichier APK

      * Télécharger avec le code QR

   3. Pour iOS, vous pouvez choisi l'option suivante une fois le code généré :

      * Télécharger le code

6. Exécutez votre application sur le périphérique ou sur le
simulateur.


## Etape suivante
{: #tutorial_next}

[Essayez-le ! ![Icône de lien externe](../icons/launch-glyph.svg "Icônede lien externe")](http://console.{DomainName}/mobile/create-project?starter=fb5e31a9-1186-4d46-939e-2f620f35b83b "Icône de lien externe"){: new_window}



### Tutoriels du module de démarrage pour l'interface utilisateur
{: #tutorials_UI}

* [Tutoriel - Catalogue magasin](tutorial_store_catalog.html)


### Tutoriels du module de démarrage pour le code
{: #tutorials_Code}

* [Tutoriel - Basic](tutorial.html)
* [Tutoriel - Cloudant Sync](tutorial_cloudant_synd.html)
* [Tutoriel - {{site.data.keyword.openwhisk_short}}](tutorial_openwhisk.html)
* [Tutoriel - {{site.data.keyword.visualrecognitionshort}}](tutorial_visual_recognition.html)
* [Tutoriel - Watson Language](tutorial_watson_language.html)
* [Tutoriel - Weather](tutorial_weather.html)

