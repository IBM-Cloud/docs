---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#Envoi par commande push de l'application de démarrage à {{site.data.keyword.Bluemix_short}}
{: #pushing_starter_app}


 
Déployez l'application de démarrage et apprenez rapidement à utiliser le service {{site.data.keyword.geospatialshort_Geospatial}} :
{:shortdesc}

1. Si ce n'est déjà fait, [installez l'outil de ligne de commande cf](docs/starters/install_cli.html).
2. [Procurez-vous le code](https://hub.jazz.net/project/streamscloud/geo-starter/overview) de l'application de démarrage {{site.data.keyword.geospatialshort_Geospatial}}. 
3. Renommez le répertoire contenant les fichiers d'application avec le nom que vous avez choisi pour votre application dans {{site.data.keyword.Bluemix_short}}. Par exemple, si votre application s'appelle myapp, renommez le répertoire en myapp.
4. Sur la ligne de commande, accédez au répertoire renommé.
<pre><code>cd myapp</code></pre>
5. Connectez-vous à {{site.data.keyword.Bluemix_short}} :
<pre><code>cf api https://api.DomainName</code></pre>
6. Connectez-vous à {{site.data.keyword.Bluemix_short}} et définissez votre organisation cible lorsque vous y êtes invité, puis déployez votre application.
<pre><code>
cf login
cf push myapp
</code></pre>

##Etape suivante

* Consultez la page de présentation de votre application, accessible depuis le tableau de bord {{site.data.keyword.Bluemix_short}} pour vérifier que l'application a démarré.
* Lancez votre application pour l'afficher dans votre navigateur. Vous trouverez l'adresse URL (ou "route") de votre application dans la page de présentation de l'application. La page Web du modèle d'application affiche des informations sur le statut des appels d'API REST dans le code de l'application et les événements que {{site.data.keyword.geospatialshort_Geospatial}} détecte.
