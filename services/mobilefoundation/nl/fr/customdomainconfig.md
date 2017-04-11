---

copyright:
  years: 2016, 2017
lastupdated:  "2017-02-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configuration d'un domaine personnalisé pour le serveur Mobile Foundation
{: #configcustomdomain}

{{site.data.keyword.mobilefoundation_short}} met à disposition un serveur {{site.data.keyword.mfserver_short_notm}}, qui est<!--on {{site.data.keyword.containerlong}} as a container group. The container group will be mapped to--> accessible en utilisant une URL dont les noms de domaine reposent sur la **région** {{site.data.keyword.Bluemix_notm}} . Vous
pouvez également configurer votre propre domaine personnalisé.
{:shortdesc}

L'<!--container group is created with a-->URL ou la route est créée avec les noms de domaine par défaut basés sur la `région` {{site.data.keyword.Bluemix_notm}}.

  |Domaine |  Région  |    
  |:----- | :----- |    
  |`mybluemix.net` | Sud des Etats-Unis |    
  |`eu-gb.mybluemix.net` | Royaume-Uni  |
  |`au-syd.mybluemix.net` | Sydney  |      
  {: caption="Table 1. Application domain names based on Region in {{site.data.keyword.Bluemix_notm}}" caption-side="top"}

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

+ Configurez une route permettant au serveur <!--container group--> d'utiliser votre domaine personnalisé.

+ Accédez au fournisseur DNS de votre domaine et ajoutez une entrée CNAME, qui acheminera le trafic de votre domaine vers la route {{site.data.keyword.Bluemix_notm}} par défaut, dans laquelle le serveur <!--container group--> s'exécute.

+ Si vous voulez configurer `https` pour votre domaine
personnalisé, transférez le certificat SSL de votre domaine dans {{site.data.keyword.Bluemix_notm}}. Pour
ce faire, accédez à **Gérer les organisations > Domaines**,
sélectionnez le domaine personnalisé pour lequel le certificat SSL doit être
configuré et cliquez sur **Télécharger le certificat** pour
transférer le certificat SSL de votre domaine. Pour plus d'informations, voir [SSL Certificates and Bluemix Custom Domains ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://developer.ibm.com/bluemix/2014/09/28/ssl-certificates-bluemix-custom-domains/){: new_window}.
