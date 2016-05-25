---

 

copyright:

  years: 2015, 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:prereq: .prereq}
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

# Déploiement de votre application avec l'interface de ligne de commande
*Dernière mise à jour : 24 février 2016*

Vous pouvez utiliser l'interface de ligne de commande pour déployer et modifier des applications et des instances de service.
{:shortdesc}

Avant de commencer, installez les interfaces de ligne de commande {{site.data.keyword.Bluemix}} et Cloud Foundry.

<p>
<a class="xref" href="http://clis.ng.bluemix.net/ui/home.html" target="_blank" title="(Ouverture dans un nouvel onglet ou une nouvelle fenêtre)"><img class="image" src="images/btn_bx_commandline.svg" alt="Télécharger l'interface de ligne de commande {{site.data.keyword.Bluemix}}" /> </a> <a class="xref" href="https://github.com/cloudfoundry/cli/releases" target="_blank" title="(Ouverture dans un nouvel onglet ou une nouvelle fenêtre)"><img class="image" src="images/btn_cf_commandline.svg" alt="Télécharger l'interface de ligne de commande Cloud Foundry" /> </a> 
</p>

**Restriction :** les outils de ligne de commande ne sont pas pris en charge par Cygwin. Utilisez-les dans une fenêtre de ligne
de commande autre que Cygwin.
{:prereq}

Une fois les interfaces de ligne de commande installées, vous pouvez commencer :

  1. {: download} Téléchargez votre code de démarrage. 
      
    <a class="xref" href="http://bluemix.net" target="_blank" title="(Ouverture dans un nouvel onglet ou une nouvelle fenêtre)"><img class="image" src="images/btn_starter-code.svg" alt="Télécharger le code de démarrage" /> </a>
  
  2. Décompressez le package dans un nouveau répertoire pour configurer votre environnement de développement.
  3. Placez-vous dans le nouveau répertoire.
  
  <pre class="pre">cd <var class="keyword varname">votre_nouveau_répertoire</var></pre>
  
   4.  Modifiez le code de votre application si nécessaire. Il est recommandé d'exécuter l'application localement avant de la déployer dans {{site.data.keyword.Bluemix}}.<br><br>Remarquez
le fichier `manifest.yml`. Lorsque vous déployez à nouveau votre application dans {{site.data.keyword.Bluemix}}, il est
utilisé pour déterminer l'adresse URL de votre application, l'allocation de mémoire, le nombre d'instance et d'autres paramètres essentiels. Vous pouvez
[en apprendre plus sur le fichier manifeste](https://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html){: new_window} dans la
documentation Cloud Foundry.
  
  5. Connectez-vous à {{site.data.keyword.Bluemix}}.
  
  <pre class="pre">bluemix api https://api.<span class="keyword" data-hd-keyref="DomainName">nom_domaine</span></pre>
  
  6. Connectez-vous à {{site.data.keyword.Bluemix_notm}}.
 
  <pre class="pre">bluemix login -u <var class="keyword varname" data-hd-keyref="user_ID">nom_utilisateur</var> -o
<var class="keyword varname" data-hd-keyref="org_name">nom_org</var> -s <var class="keyword varname" data-hd-keyref="space_name">nom_espace</var></pre>
  
  7. Déployez votre application dans {{site.data.keyword.Bluemix_notm}}. Pour plus d'informations sur la commande cf push, voir
[Téléchargement de votre application](./upload_app.html).
  
  <pre class="pre">cf push <var class="keyword varname" data-hd-keyref="app_name">nom_app</var></pre>
  
  8. Accédez à votre application en entrant l'adresse URL suivante dans votre navigateur :
  
  <pre class="codeblock"><code><var class="keyword varname" data-hd-keyref="host">hôte</var>.<span class="keyword" data-hd-keyref="APPDomain">nom_domaine_app</span></code></pre>
