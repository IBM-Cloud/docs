---

copyright:
  years: 2016, 2017
lastupdated: "2017-3-3"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Initiation à {{site.data.keyword.product-insights_short}}
{: #product-insights}

{{site.data.keyword.product-insights_full}} se connecte aux produits logiciels IBM sur site pour générer un inventaire de tous les produits et fournit des analyses sur les données d'utilisation de ces derniers. 

{:shortdesc}

Le service {{site.data.keyword.product-insights_short}} s'exécute dans IBM Bluemix et reçoit des informations provenant des produits logiciels IBM sur site activés. Ces informations sont ensuite affichées dans le tableau de bord de l'instance de service. Pour utiliser ce service, vous devez disposer d'un compte Bluemix et devez créer le service dans une organisation et un espace. Les informations sur les produits et l'utilisation des produits sur site activés sont stockées de manière sécurisée et peuvent être consultées dans la portée ou le contexte de ce service unique.  

Astuce : il est plus simple de n'utiliser qu'une seule instance de service pour commencer. 

Pour commencer à utiliser {{site.data.keyword.product-insights_short}}, procédez comme suit : 

1.  Dans l'onglet **Manage**, cliquez sur le bouton **Register a product** pour afficher la liste des produits pris en charge, ainsi que le niveau de version requis. Des instructions sont fournies pour chaque type de produit afin que vous puissiez connecter vos instances de produit sur site au service {{site.data.keyword.product-insights_short}}. Si nécessaire, mettez à jour vos produits logiciels IBM sur site activés vers le niveau prérequis minimum. S'il s'agit d'un produit nécessitant un niveau minimum pris en charge, installez le groupe de correctifs ou le correctif temporaire afin d'activer l'intégration avec {{site.data.keyword.product-insights_short}}. 
2.  Connectez vos produits logiciels IBM sur site activés à votre service {{site.data.keyword.product-insights_short}}. Dans le cadre du processus de configuration de chaque produit, vous avez besoin des données d'identification du service (c'est-à-dire apikey et apihost). Vous trouverez les données d'identification du service dans l'onglet **Service Credentials** du tableau de bord du service. 
3.  Après avoir activé et connecté chaque instance de produit, il se peut que vous deviez démarrer ou redémarrer les produits ou les instances de produit afin qu'ils fournissent les informations les concernant et sur leur utilisation au service {{site.data.keyword.product-insights_short}}. 

Pour plus de détails sur l'activation des produits, le niveau de prise en charge minimum de chaque produit et le mode d'activation de chaque produit en vue de son intégration avec {{site.data.keyword.product-insights_short}}, rejoignez la communauté {{site.data.keyword.product-insights_full}} [Technical Community](https://developer.ibm.com/product-insights/).

Vous pouvez consulter votre inventaire en sélectionnant l'onglet **Manage** dans le tableau de bord du service.  

* Dans le tableau de bord du service, les noms des produits connectés sont répertoriés dans le panneau **Products**. 
* Pour afficher toutes les instances de produit, sélectionnez **View all**. Pour afficher les instances de produit d'un produit, sélectionnez ce produit dans le panneau **Products** ; les instances apparaissent alors dans le panneau **Instances**.
* Pour afficher les détails d'une seule instance de produit, sélectionnez l'instance de produit dans le panneau **Instances**. Le panneau **Details** affiche alors les informations correspondantes. Le panneau **Details** indique les détails de chaque instance de produit, ainsi que les informations d'utilisation envoyées par l'instance. 
* L'onglet **Usage** affiche les informations d'utilisation du produit au format graphique. Selon le produit, vous pouvez indiquer le type d'informations que vous souhaitez visualiser ainsi que la période d'échantillonnage.
* L'onglet **Details** affiche les informations sur l'instance de produit, notamment les informations sur le produit, l'environnement et les composants. 
* L'onglet **Advisor**, dans l'onglet **Services**, fournit des détails sur les services supplémentaires dont vous pourriez tirer parti en plus de l'instance de produit en cours. L'onglet **Updates** fournit des informations sur le niveau de version de l'instance de produit et sa devise. 










