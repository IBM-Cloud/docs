---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Projets
{: #projects}

La console {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} combine l'interface utilisateur, les données et les services d'une application au sein d'un *projet* complet. Lorsque vous créez un projet, tous les composants requis de votre application, ainsi que les fonctions ajoutées sont gérées sur le serveur {{site.data.keyword.Bluemix_notm}}. Vous pouvez télécharger le code de votre application ainsi que les données d'identification et les initialiseurs requis si les services sont configurés dans votre projet. Vous pouvez afficher tous vos projets en sélectionnant **Projets**.  

Vous pouvez afficher des informations supplémentaires sur un projet unique en le sélectionnant dans la page **Projets**. La page relative à la présentation du projet qui s'affiche comprend les services configurés et disponibles pour le projet. Les services sont des fonctions distinctes qui étendent la fonctionnalité de votre application. Etant donné qu'il s'agit d'un ajout individuel, vous pouvez ajouter les services dont vous avez besoin, comme les services de notifications push, d'authentification, de données et de stockage ou d'autres services. Quand vous ajoutez un service à votre projet sur la page relative à la présentation du projet puis suivez les instructions pour le configurer, il est automatiquement associé à votre application. Pour plus d'informations sur la page de présentation du projet, voir la rubrique traitant de cette [page](project_overview_page.html).

Pour créer votre projet, vous devez sélectionner un [modèle](patterns.html) puis un [module de démarrage](starters.html).


## Page de présentation du projet
{: #project_overview}

Vous pouvez afficher et utiliser un seul projet {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} en sélectionnant ce projet sur la page **Projets**, ce qui ouvre la page relative à la présentation du projet.
{: shortdesc}

La page relative à la présentation du projet affiche une vignette pour chaque fonctionnalité qui est configurée ou disponible pour configuration avec le projet sélectionné. La vignette, qui indique le type de fonctionnalité, comporte un bouton *actions* avec trois boutons verticaux. Les fonctionnalités disponibles incluent, par exemple, les services {{site.data.keyword.mobilepushshort}}, Analytics ou Data et Storage. Les fonctionnalités compatibles dépendant du type de projet et des fonctionnalités disponibles dans la région concernée, il est possible que toutes les fonctionnalités ne soient pas disponibles avec tous les projets. 

Quand un type de fonctionnalité n'est pas encore associé au projet, un bouton **Créer**  est affiché sur la vignette. Les options du bouton
d'actions permettent de créer une instance du service ou d'ajouter une instance de service existante si la fonctionnalité n'est pas encore associée. La sélection de l'option d'ajout d'une instance de service existante fournit une liste des instances de service de ce type au sein de votre espace.

Si la fonctionnalité est déjà associée à ce projet, le nom de l'instance de service associée est affiché sur la vignette après le type de
fonctionnalité, ce qui facilite l'identification de l'instance de service associée à votre projet sur votre console {{site.data.keyword.dev_console}}. Les
actions disponibles sur le bouton d'action sont les suivantes : **Afficher** et **Retirer** quand la fonctionnalité est déjà associée au projet. Le retrait d'une instance de service efface seulement l'association à ce projet et ne supprime pas l'instance de service de votre console {{site.data.keyword.dev_console}}. Pour supprimer une instance de service, cliquez sur la page accessible en sélectionnant les options relatives aux services Web et mobiles pour afficher et supprimer les instances de service voulues.

Sélectionnez la commande relative à l'obtention du code sur la vignette **Code** pour télécharger le code pour votre projet. Pour plus d'informations sur le
téléchargement du code, voir [Obtention du code](get_code.html).


## Mise à jour de votre projet pour utiliser un nouveau module de démarrage
{: #update-starter}

1. Depuis la page relative aux projets ou à la présentation du projet, cliquez sur l'icône du menu déroulant dynamique et sélectionnez le module de démarrage de la mise à jour.

2. Choisissez un nouveau module de démarrage puis cliquez sur **Mettre à jour**.

3. Cliquez sur  la commande relative à l'obtention du code sur la page de présentation du projet pour sélectionner votre langue.

   Vous pouvez également cliquer sur la page **Code**.


## Mise à jour de votre projet pour générer un nouveau langage
{: #update-language}

1. Depuis la page relative au projet ou à la présentation du projet, cliquez sur l'icône du menu déroulant dynamique et sélectionnez le module de démarrage de la mise à jour.

2. Sélectionnez un nouveau langage et cliquez sur **Mettre à jour**.

3. Cliquez sur  la commande relative à l'obtention du code sur la page de présentation du projet pour sélectionner votre langue.
