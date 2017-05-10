---

copyright:
  years: 2017
lastupdated: "2017-04-13"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Mes API
{: #manage_api}

L'onglet **View Managed APIs** permet de visualiser le statut global des API que vous gérez et de celles que vous avez précédemment gérées mais qui ne sont pas exposées à ce moment. L'onglet **Shared APIs** permet d'afficher toutes les API qui ont été partagées avec votre organisation {{site.data.keyword.Bluemix_notm}} via la gestion d'API ou via le service {{site.data.keyword.apiconnect_short}}.

Vous pouvez afficher toutes les API que vous gérez grâce à la gestion d'API dans le tableau de bord des API. 

## Affichage des API gérées
{: #view_api}

Vous pouvez afficher les API créées pour les actions {{site.data.keyword.openwhisk_short}} et d'autres sources externes.

1. Dans le tableau de bord {{site.data.keyword.Bluemix_notm}}, cliquez sur l'icône **Menu** > **Services** > **API**.
2. Pour sélectionner votre source, cliquez sur **Manage APIs**. La liste des API actuellement gérées s'affiche. Les types d'API sont les suivants :
    * User Defined Endpoints (Noeuds finaux définis par l'utilisateur) : ces entrées sont des API qui ne font pas partie de l'environnement {{site.data.keyword.Bluemix_notm}} et dont le suivi est assuré par le noeud final de leur URL. 
    * {{site.data.keyword.openwhisk_short}} Apps (Applications OpenWhisk) : ces entrées sont des actions {{site.data.keyword.openwhisk_short}} encapsulées dans une API.

Sélectionnez le nom d'une API pour afficher plus de détails à son sujet.

## Création d'API gérées
{: #create_mgd_api}

Vous pouvez ajouter une API à la liste sans quitter la liste des API gérées en sélectionnant **Create Managed API**.

Après avoir indiqué si vous souhaitez créer une API {{site.data.keyword.openwhisk_short}} ou un proxy d'API (API externe), saisissez les informations concernant votre nouvelle API.  

Il s'agit du seul endroit permettant d'ajouter un proxy d'API, ou API externe. Une API externe est une API qui n'est ni créée, ni stockée dans l'espace de l'organisation {{site.data.keyword.Bluemix_notm}}. Pour gérer une telle API, indiquez l'URL de son noeud final externe. Cela s'avère utile lorsque vous essayez la gestion d'API et vous voulez savoir si cette fonction correspond à vos attentes, ou lorsque vous disposez déjà d'API qui s'exécutent avec ces URL existantes et que vous ne souhaitez pas interrompre. 

Pour plus d'informations sur les paramètres obligatoires lors de la création des API, voir [Gestion des API](manage_apis.html).

## Utilisation des API partagées
{: #share_api}

L'onglet **Explore Shared APIs** affiche les API créées par d'autres et partagées avec vous. Vous pouvez également créer des clés d'API pour les API associées aux actions {{site.data.keyword.openwhisk_short}} et au service {{site.data.keyword.appconserviceshort}}.

1. A partir du tableau de bord {{site.data.keyword.Bluemix_notm}}, cliquez sur l'icône **Menu** > **Services** > **API**.
2. Sélectionnez **Explore Shared APIs** dans la navigation. Toutes les API que vous pouvez consommer s'affichent ici.
3. Pour consommer une API, sélectionnez-la pour ouvrir le portail de développeur associé qui vous permet de vous abonner à un plan afin de l'utiliser. 
4. Après avoir sélectionné une API à gérer, reportez-vous à [Gestion des API](manage_apis.html) pour avoir plus d'informations sur les tâches suivantes : 
    * Afficher l'utilisation d'une API
    * Créer des clés d'API
    * Utiliser l'explorateur d'API pour afficher la documentation et tester l'API.
