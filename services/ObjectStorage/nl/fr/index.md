---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-11"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}



# Initiation à {{site.data.keyword.objectstorageshort}} {: #getting-started-with-object-storage}


{{site.data.keyword.objectstoragefull}} fournit un stockage de données en cloud non structuré. Vous pouvez stocker du contenu et y accéder mais aussi composer interactivement des applications et des services et vous y connecter.
{: shortdesc}

Certains cas d'utilisation courants pour le service {{site.data.keyword.objectstorageshort}} sont présentés ci-dessous :

* Sauvegarde de données de volume depuis vos instances
* Utilisation d'un emplacement intermédiaire lors du transfert de volumes importants de données
* Transfert de données entre des environnements non directement connectés
* Rôle de référentiel central


{{site.data.keyword.Bluemix_notm}} Public {{site.data.keyword.objectstorageshort}} permet d'accéder à un compte Swift {{site.data.keyword.objectstorageshort}} complet pour gérer vos données. Aucun chiffrement côté fournisseur n'est fourni.


1.	Mettez à disposition votre instance depuis le catalogue {{site.data.keyword.Bluemix_notm}}. Configurez votre instance et cliquez sur **Créer**. Si vous avez choisi initialement l'option **Laisser non lié** pour la zone **Application**, vous
pourrez toujours lier l'instance de service à votre application {{site.data.keyword.Bluemix_notm}} ultérieurement.
2. Dans votre tableau de bord d'instance de service, créez un conteneur pour commencer à stocker des objets.
3. Ajoutez un fichier dans votre conteneur depuis le menu déroulant **Actions**.
4. Pour tester l'accès à vos objets, cliquez sur **Télécharger** et révisez le fichier.
5. Quand vous êtes prêt à connecter votre instance à une application, configurez vos données d'identification de service et [liez le service](/docs/services/reqnsi.html#add_service).



# Liens connexes
{: #rellinks}

## Référence API
{: #api}
* [OpenStack {{site.data.keyword.objectstorageshort}} (Swift) API v1](http://developer.openstack.org/api-ref-objectstorage-v1.html){: new_window}
* [OpenStack Identity (Keystone) API v3.0](http://developer.openstack.org/api-ref-identity-v3.html){: new_window}

## SDK
{: #sdk}
* [Kits de développement de logiciels (SDK) OpenStack](https://wiki.openstack.org/wiki/SDKs){: new_window}

## Tutoriels et exemples
{: #samples}
* [Connecting to IBM {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}} with Java](https://developer.ibm.com/recipes/tutorials/connecting-to-ibm-object-storage-for-bluemix-with-java/){: new_window}
* [Use Python to access your {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.objectstorageshort}}](https://developer.ibm.com/recipes/tutorials/use-python-to-access-your-bluemix-object-storage/){: new_window}
* [Use PHP to leverage {{site.data.keyword.objectstorageshort}}](https://developer.ibm.com/recipes/tutorials/use-php-to-leverage-object-storage-for-bluemix/){: new_window}
* [Use Node js to access Object Storage for
Bluemix](https://developer.ibm.com/recipes/tutorials/use-pkgcloud-to-access-ibm-object-storage-for-bluemix-with-node-js/){: new-window}

## Contextes d'exécution compatibles
{: #buildpacks}
* [Liberty for Java](https://www.ng.bluemix.net/docs/runtimes/liberty/index.html){: new_window}
* [SDK for Node.js](https://www.ng.bluemix.net/docs/runtimes/nodejs/index.html){: new_window}
* [Go](https://www.ng.bluemix.net/docs/runtimes/go/index.html){: new_window}
* [PHP](https://www.ng.bluemix.net/docs/runtimes/php/index.html){: new_window}
* [Python](https://www.ng.bluemix.net/docs/runtimes/python/index.html){: new_window}
* [Ruby](https://www.ng.bluemix.net/docs/runtimes/ruby/index.html){: new_window}
* [Packs de construction de la communauté](https://www.ng.bluemix.net/docs/starters/byob.html){: new_window}


## Liens connexes
{: #general}
* [IBM {{site.data.keyword.Bluemix_notm}} - Tarification](https://www.ng.bluemix.net/#/pricing){: new_window}
* [IBM {{site.data.keyword.Bluemix_notm}} Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
