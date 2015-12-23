{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:download: .download}
{:pre: .pre}
{:app_name: data-hd-keyref="app_name"}
{:app_key: data-hd-keyref="app_key"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:host: data-hd-keyref="host"}
{:org_name: data-hd-keyref="org_name"}
{:route: data-hd-keyref="route"}
{:space_name: data-hd-keyref="space_name"}
{:service_name: data-hd-keyref="service_name"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:user_ID: data-hd-keyref="user_ID"}

# Déploiement de votre application avec l'interface de ligne de commande Cloud Foundry
*Dernière mise à jour : 11 novembre 2015*

Vous pouvez utiliser l'interface de ligne de commande Cloud Foundry pour déployer et modifier des applications et des instances de service.
{:shortdesc}

Avant de commencer, installez l'interface de ligne de commande cf.

<p>
<a class="xref" href="https://github.com/cloudfoundry/cli/releases" target="_blank" title="(Ouverture dans un nouvel onglet ou une nouvelle fenêtre)"><img class="image" src="images/btn_cf_commandline.svg" alt="Télécharger l'interface de ligne de commande Cloud Foundry" /> </a> </p>

**Restriction :** l'interface de ligne de commande Cloud Foundry n'est pas prise en charge par Cygwin. Utilisez-la dans une fenêtre de ligne de commande autre que Cygwin.

Une fois l'interface de ligne de commande cf installée, vous pouvez commencer :

  1. Téléchargez votre code de démarrage.
  
    <p>
    <a class="xref" href="http://bluemix.net" target="_blank" title="(Ouverture dans un nouvel onglet ou une nouvelle fenêtre)"><img class="image" src="images/btn_starter-code.svg" alt="Télécharger le code du module de démarrage" /> </a> </p>
  
  {:download}
  2. Décompressez le package dans un nouveau répertoire pour configurer votre environnement de développement.
  3. Placez-vous dans le nouveau répertoire.
  
  <pre class="pre">cd <var class="keyword varname">votre_nouveau_répertoire</var></pre>
  
  4. Connectez-vous à {{site.data.keyword.Bluemix}}.
  
  <pre class="pre">cf api https://api.<span class="keyword" data-hd-keyref="DomainName">nom_domaine</span></pre>
  
  5. Connectez-vous à {{site.data.keyword.Bluemix_notm}}.
 
  <pre class="pre">cf login -u <var class="keyword varname" data-hd-keyref="user_ID">nom_utilisateur</var> -o
<var class="keyword varname" data-hd-keyref="org_name">nom_organisation</var> -s <var class="keyword varname" data-hd-keyref="space_name">nom_espace</var></pre>
  
  6. Déployez votre application dans {{site.data.keyword.Bluemix_notm}}. Pour plus d'informations sur la commande cf push, voir
[Téléchargement de votre application](upload_app.html#upload_app__push).
  
  <pre class="pre">cf push <var class="keyword varname" data-hd-keyref="app_name">nom_app</var></pre>
  
  7. Accédez à votre application en entrant l'adresse URL suivante dans votre navigateur :
  
  <pre class="codeblock"><code><var class="keyword varname" data-hd-keyref="host">hôte</var>.<span class="keyword" data-hd-keyref="APPDomain">nom_domaine_app</span></code></pre>
