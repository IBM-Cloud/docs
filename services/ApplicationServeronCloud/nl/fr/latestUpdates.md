---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-08"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Dernières mises à jour
{: #latest_updates}

Liste des dernières mises à jour du service.

## 8 novembre 2016 : Mise à jour de WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}

* Ajout d'une capacité pour les clients de demander une adresse [IP publique](networkEnvironment.html#networkEnvironment) pour leur serveur WebSphere Application Server pour la machine virtuelle {{site.data.keyword.Bluemix_notm}}
* Correction de [plusieurs vulnérabilités de sécurité](http://www-01.ibm.com/support/docview.wss?uid=swg21993842){: new_window} affectant WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}, incluant :
  * Une vulnérabilité dans IBM WebSphere Application Server qui peut permettre aux attaquants distants d'exécuter du code Java arbitraire avec un objet sérialisé à partir de sources non fiables.
  * Une vulnérabilité de déni de service due à une lecture hors limites de la fonction TS_OBJ_print_bio. Un attaquant distant peut exploiter cette vulnérabilité en utilisant un fichier d'horodatage spécialement conçu pour provoquer l'arrêt de l'application.
  * Une vulnérabilité potentielle dans OpenSSL qui peut permettre à un agresseur à distance d'obtenir des informations sensibles, causées par une erreur dans le Triple-DES sur le chiffrement par bloc de 64 bits, utilisé dans le cadre du protocole SSL/TLS. En capturant de grandes quantités de trafic chiffré entre le serveur SSL/TLS et le client, un agresseur à distance capable de mener une attaque d'interposition (man in the middle) peut exploiter cette vulnérabilité pour récupérer les données en clair et obtenir des informations confidentielles. Cette vulnérabilité est connue sous le nom d'attaque SWEET32 Birthday.
  * OpenSSL est vulnérable à un déni de service. En demandant à plusieurs reprises la renégociation, un agresseur à distance authentifié peut envoyer une extension de demande d'état OCSP trop grande pour consommer toutes les ressources de mémoire disponibles.
  * OpenSSL est vulnérable à un déni de service, causé par un dépassement d'entier dans la fonction MDC2_Update. En utilisant des vecteurs d'attaque inconnus, un agresseur à distance peut exploiter cette vulnérabilité pour déclencher une écriture hors limites et provoquer l'arrêt de l'application.
  * Une vulnérabilité potentielle dans OpenSSL qui permet à un agresseur à distance d'obtenir des informations sensibles, provoquée par une erreur dans l'implémentation DSA qui permet le suivi d'un chemin de code temporel non constant pour certaines opérations. Un agresseur peut exploiter cette vulnérabilité en utilisant une attaque de synchronisation de cache pour récupérer la clé DSA privée.
  * OpenSSL est vulnérable à un déni de service, causé par des vérifications de longueur de message manquantes lors de l'analyse des certificats. Un agresseur à distance authentifié peut exploiter cette vulnérabilité pour déclencher une lecture hors limites et provoquer un déni de service. 

## 19 septembre 2016 : Mise à jour de WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}

* Mise à niveau des fichiers binaires de WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} de façon à ce que le groupe de correctifs 16.0.0.3 soit installé sur les nouvelles instances de WebSphere Application Server Liberty (plans Core et ND). 
* Correction de [plusieurs vulnérabilités de sécurité](http://www-01.ibm.com/support/docview.wss?uid=swg21990236){: new_window} affectant WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}, incluant :
  * Une vulnérabilité dans IBM WebSphere Application Server Liberty qui peut permettre à un agresseur à distance de mener des attaques de phishing.
  * Une vulnérabilité dans IBM WebSphere Application Server Liberty sur le cross-site scripting dans les clients OpenID Connect.
  * Une vulnérabilité potentielle dans IBM WebSphere Application Server Liberty qui peut permettre à un agresseur à distance d'obtenir des informations sensibles, causée par une mauvaise gestion des exceptions lorsqu'une page d'erreur par défaut n'existe pas.
  * Une vulnérabilité dans Apache Tomcat à un déni de service, provoquée par une erreur dans le composant Apache Commons FileUpload.
  * Une vulnérabilité dans IBM WebSphere Application Server et IBM WebSphere Application Server Liberty qui peut permettre à un agresseur à distance d'obtenir des informations sensibles, causée par le traitement inapproprié des réponses sous certaines conditions.
  * Une vulnérabilité non spécifiée liée au composant Networking qui n'a pas d'impact sur la confidentialité, un impact faible sur l'intégrité et aucune disponibilité.

## 17 août 2016 : Mise à jour de WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}

* Mise à niveau des fichiers binaires de WebSphere Application Server for Bluemix de la version 8.5.5.9 à la version 8.5.5.10
* Correction de [plusieurs vulnérabilités de sécurité](http://www-01.ibm.com/support/docview.wss?uid=swg21988710){: new_window} affectant WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}, incluant :
  * Vulnérabilités Apache Struts impactant la console d'administration WebSphere Application Server et WebSphere Application Server Hypervisor Edition.
  * Déni potentiel de la vulnérabilité du service avec IBM WebSphere Application Server lors de l'utilisation de services SIP.
  * Plusieurs vulnérabilités pouvant impacter IBM HTTP Server utilisé par WebSphere Application Server.
  * Vulnérabilité permettant le réacheminement du trafic HTTP avec les applications CGI, pouvant impacter IBM HTTP Server (IHS). Cette vulnérabilité est connue comme étant "HTTPOXY".
  * Vulnérabilité de divulgation d'informations dans IBM WebSphere Application Server.
  * Vulnérabilité potentielle de contournement de la sécurité dans IBM WebSphere Application Server qui ne se produit que dans les environnements dans lesquels la propriété personnalisée webcontainer HttpSessionIdReuse est activée.


## 24 juin 2016 : Mise à jour de WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}

* Nouvelle possibilité pour les clients de choisir entre V8.5 et V9.0 lors de la création d'une nouvelle instance *Traditional ND* ou *Traditional WebSphere*.
* Mise à niveau des fichiers binaires de WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} de façon à ce que le groupe de correctifs 16.0.0.2 soit installé sur les nouvelles instances de WebSphere Application Server Liberty (plans Core et ND). 16.0.0.2 est le groupe de correctifs qui suit 8.5.5.9. En ce qui concerne 16.0.0.2, toutes les fonctions facultatives Liberty autorisées prises en charge pour ces plans sont installées par défaut.
* Correction de [plusieurs vulnérabilités de sécurité](http://www-01.ibm.com/support/docview.wss?uid=swg21984977){: new_window} affectant WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}, incluant :
  * Vulnérabilité XML External Entity Injection (XXE) dans Apache Standard Taglibs qui affecte IBM WebSphere Application Server.
  * Possibilité d'une faiblesse de sécurité lors de l'utilisation de la fonction API Discovery appliquée au profil WebSphere Application Server Liberty et des documents Swagger.
  * Vulnérabilité potentielle de divulgation d'informations dans le centre d'administration pour IBM WebSphere Application Server Liberty.
  * Vulnérabilité potentielle de fractionnement des réponses HTTP dans IBM WebSphere Application Server.
  * Vulnérabilités OpenSSL révélées le 3 mai 2016 par OpenSSL Project.

## 13 juin 2016 : Mise à jour de WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}

* Nouvelle possibilité pour les clients de générer, provisionner, gérer et supprimer des instances de machine virtuelle via la création d'une application ou d'un script qui utilise des API WebSphere Application Server for Bluemix RESTful.
* Nouvelle fonction qui permet à un client d'avoir un nombre fixe d'instances STOPPED ne comportant pas plus de 10 adresses IP ou 64 Go de mémoire. Les clients sont désormais facturés pour les instances accumulées à l'état STOPPED à un taux réduit de 5 %.

## 26 avril 26 : Mise à jour de WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}

* Correction des [vulnérabilités potentielles en matière de sécurité](http://www-01.ibm.com/support/docview.wss?uid=swg21982128){: new_window} dans WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} si FIPS 140-2 est activé, ce qui inclut plusieurs vulnérabilités dans Samba - dont Badlock.
* Diverses maintenances de service ont été intégrées.

## 15 avril 2016 : Mise à jour de WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}

* Mise à niveau des fichiers binaires de WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} de la version 8.5.5.8 à la version 8.5.5.9
* Correction d'une vulnérabilité à une attaque [Cross-site scripting](http://www-01.ibm.com/support/docview.wss?uid=swg21981221){: new_window} dans Liberty for Java for IBM {{site.data.keyword.Bluemix_notm}} affectant les consommateurs utilisant le client OpenID Connect (OIDC).
* Diverses maintenances de service ont été intégrées.

## 19 février 2016 : Mise à jour de WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}
* Ajout d'une option pour les clients avec des applications gourmandes en mémoire leur permettant de redimensionner leur environnement avec des machines
virtuelles
plus grandes. Les clients peuvent sélectionner la taille de ressource spécifique d'un composant WebSphere Application Server ou d'un seul système en leur
allouant des machines virtuelles dotés de jusqu'à 32 Go de mémoire RAM.
* Mise à niveau des fichiers binaires de {{site.data.keyword.Bluemix_notm}} de la version 8.5.5.7 à 8.5.5.8
* Correction de plusieurs vulnérabilités dans IBM SDK Java Technology Edition affectant WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}, désignées par l'acronyme [SLOTH](http://www-01.ibm.com/support/docview.wss?uid=swg21977244){: new_window}.
* Correction d'une vulnérabilité à une attaque par [Cross-site
scripting](http://www-01.ibm.com/support/docview.wss?uid=swg21976337){: new_window} affectant les consommateurs de la sortie du fournisseur OAuth.
* Diverses maintenances de service ont été intégrées.

## 11 décembre 2015 : Mise à jour de WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}
* Le nom officiel du produit IBM Application Server on Cloud for {{site.data.keyword.Bluemix_notm}} a été remplacé par IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}
* Ajout de nouvelles fonctions au plan WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} Network Deployment. Le plan se compose d'un environnement de cellule
WebSphere  Application Server Network Deployment avec deux machines virtuelles, ou plus. Ces nouvelles fonctions permettent aux utilisateurs de configurer un environnement en cluster pour la haute disponibilité, la reprise en ligne et
l'évolutivité.
* Ajout de nouvelles fonctions au plan WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} Liberty Core. Le plan inclut l'utilisation d'une collectivité Liberty, qui est un domaine d'administration pour un groupe de profils Liberty (serveurs) et qui se
compose de deux machines virtuelles, ou plus.
* Mise à niveau des fichiers binaires de WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} de la version 8.5.5.6 à 8.5.5.7
* Une [vulnérabilité d'Apache Commons
Collections](https://www.us-cert.gov/ncas/current-activity/2015/11/13/Apache-Commons-Collections-Java-Library-Vulnerability){: new_window} a été traitée pour la désérialisation des objets Java.
* Une vulnérabilité permettant une [attaque
par séparation de réponse HTTP](http://www-01.ibm.com/support/docview.wss?uid=swg21972254){: new_window} a été traitée.
* Diverses maintenances de service ont été intégrées.

## 15 octobre 2015 : Mise à jour d'Application Server on Cloud
* Ajout des deux nouveaux plans suivants :
  * [WebSphere Application Server Traditional V9 Beta](https://www-01.ibm.com/marketing/iwm/iwmdocs/web/cc/earlyprograms/websphere.shtml){: new_window}
  * WebSphere Application Server ND
* Diverses maintenances de service
