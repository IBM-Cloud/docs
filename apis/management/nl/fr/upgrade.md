---

copyright:
  years: 2017
lastupdated: "2017-04-11"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Accès à des fonctions de gestion d'API supplémentaires
{: #upgrade}

La gestion d'API vous permet de contrôler les fréquences d'appel, ainsi que le protocole d'autorisation OAuth, et d'afficher des analyses. Vous pouvez accroître votre contrôle sur la gestion des API en effectuant une mise à niveau vers le service {{site.data.keyword.apiconnect_full}}. Le service {{site.data.keyword.apiconnect_short}} offre plus de choix en matière de règles de sécurité, ainsi qu'un contrôle accru sur les limites de fréquence. Vous avez, de plus, la possibilité de configurer un portail de développeur entièrement personnalisable qui vous permet de diffuser vos API sur les réseaux sociaux et de vous engager auprès de la communauté des développeurs. Vous bénéficiez également d'autres avantages : 
* Gestion du cycle de vie
* API composites
* Intégration des services Web
* Médiation de protocole
* Génération d'API à partir de schéma
* Développement de microservices

La migration vers le service {{site.data.keyword.apiconnect_short}} est simple et vous n'avez pas à recréer les API que vous gérez grâce à la gestion d'API. 

## Migration des API vers {{site.data.keyword.apiconnect_short}}
{: #migrate_api}

Si vous décidez d'effectuer une mise à niveau vers {{site.data.keyword.apiconnect_full}}, vous devez migrer vos API depuis la gestion d'API vers le service {{site.data.keyword.apiconnect_short}} en procédant comme indiqué ci-après pour chacune de vos API : 

1. Téléchargez le document Swagger de l'API à partir de la gestion d'API. 
    1. Ouvrez votre application et sélectionnez **API Management**.
	2. Sélectionnez l'onglet **API Explorer**. La liste de vos API liées à ce projet s'affiche.
    2. Téléchargez le document Swagger de votre API en cliquant sur l'icône située en regard de l'API.
2. Créez et préparez l'instance {{site.data.keyword.apiconnect_short}}.  
    1. Créez une instance du service {{site.data.keyword.apiconnect_short}} à partir du catalogue {{site.data.keyword.Bluemix_notm}}.
	2. Sélectionnez votre plan.
	3. Sélectionnez **+Ajouter** pour créer un catalogue. 
	4. Entrez un nom d'affichage et un nom pour le catalogue, puis sélectionnez **Ajouter**.
	5. Sélectionnez le catalogue que vous avez créé.
3. Importez le document Swagger dans votre instance {{site.data.keyword.apiconnect_short}} en procédant comme suit : 
	1. Dans le tableau de bord du service
{{site.data.keyword.apiconnect_short}}, sélectionnez **Accéder à... (>>)** > **Brouillons** dans le menu.
	2. Sélectionnez l'onglet API.
	3. Sélectionnez **+Ajouter** > **Importer l'API à partir d'un fichier ou d'une URL**.
	4. Recherchez et sélectionnez le fichier Swagger que vous avez téléchargé depuis la gestion d'API. Sélectionnez **Ouvrir**.
	5. Sélectionnez **Importer** pour importer votre API dans le service {{site.data.keyword.apiconnect_short}}.
4. Indiquez les paramètres de votre API.
    1. Sélectionnez **Créer un produit**.
	2. Sélectionnez le produit que vous avez créé pour afficher ses paramètres. 
	3. Définissez la limite de fréquence de l'API.
	4. Définissez le niveau de l'API.
5. Ajoutez le noeud final de l'API, si nécessaire.
    1. Sélectionnez l'API.
	2. Sélectionnez l'onglet Assemblage.
	3. Ajoutez le noeud final, s'il n'est pas déjà spécifié. 
	
 Après avoir migré vos API, vous pouvez accéder à toutes les fonctions de gestion d'API en ouvrant la mosaïque de services {{site.data.keyword.apiconnect_short}}, ou à partir du tableau de bord {{site.data.keyword.Bluemix_notm}}.  

 
