---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configuration d'un domaine personnalisé pour le serveur {{site.data.keyword.mobilefoundation_short}}
{: #configcustomdomain}

*Dernière mise à jour : 15 juin 2016*
{: .last-updated}

{{site.data.keyword.mobilefoundation_short}} fournit un
serveur {{site.data.keyword.mfserver_short_notm}} sur
{{site.data.keyword.containerlong}} comme groupe de conteneurs. Ce
groupe de conteneurs sera mappé à une URL dont les noms de domaine sont basés
sur la **Région** {{site.data.keyword.Bluemix_notm}}. Vous
pouvez également configurer votre propre domaine personnalisé.
{:shortdesc}

Un groupe de conteneurs est créé avec une URL ou une route dont les
noms de domaine par défaut sont basés sur la `Région` {{site.data.keyword.Bluemix_notm}}.

*Tableau 1. Noms de domaine de l'application basés sur la `Région`
dans {{site.data.keyword.Bluemix_notm}}*

  |Domaine |  Région  |    
  |:----- | :----- |    
  |`mybluemix.net` | Dallas, US  |    
  |`eu-gb.mybluemix.net` | London, UK  |    
  |`au-syd.mybluemix.net`  | Sydney, Australia |  

Pour pouvoir utiliser votre propre domaine, vous devez configurer un
domaine personnalisé en procédant comme suit : 

1.	Créez une instance {{site.data.keyword.mfserver_short_notm}}
en créant l'instance de service
{{site.data.keyword.mobilefoundation_short}} en sélectionnant
l'un des plans pris en charge. 

+ Ajoutez dans votre `Organisation`
{{site.data.keyword.Bluemix_notm}} le domaine personnalisé que vous
souhaitez utiliser. Accédez à **Gérer les organisations > Domaines >
Ajouter un domaine** pour ajouter votre propre domaine.

+ Configurez une route permettant à votre groupe de conteneurs
d'utiliser votre domaine personnalisé. 

+ Accédez au fournisseur DNS de votre domaine et ajoutez une entrée
CNAME, qui acheminera le trafic de votre domaine vers la route
{{site.data.keyword.Bluemix_notm}} par défaut, dans laquelle le
groupe de conteneurs est exécuté. 

+ Si vous voulez configurer `https` pour votre domaine
personnalisé, transférez le certificat SSL de votre domaine dans {{site.data.keyword.Bluemix_notm}}. Pour
ce faire, accédez à **Gérer les organisations > Domaines**,
sélectionnez le domaine personnalisé pour lequel le certificat SSL doit être
configuré et cliquez sur **Télécharger le certificat** pour
transférer le certificat SSL de votre domaine. Pour plus d'informations,
voir
[SSL Certificates and Bluemix Custom Domains](https://developer.ibm.com/bluemix/2014/09/28/ssl-certificates-bluemix-custom-domains/).
