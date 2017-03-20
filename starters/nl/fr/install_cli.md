---



copyright:

  years: 2015，2017

lastupdated: "2017-01-12"


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

# Téléchargement, modification et redéploiement de votre application Cloud Foundry à l'aide de l'interface de ligne de commande

Utilisez l'interface de ligne de commande Cloud Foundry pour télécharger, modifier et redéployer vos instances de service et applications Cloud Foundry.
{:shortdesc}

Avant de commencer, téléchargez et installez l'interface de ligne de commande Cloud Foundry. 

<p>
<a class="xref" href="https://github.com/cloudfoundry/cli/releases" target="_blank" title="(Ouverture dans un nouvel onglet ou une nouvelle fenêtre)"><img class="image" src="images/btn_cf_commandline.svg" alt="Télécharger l'interface de ligne de commande Cloud Foundry" /> </a>
</p>

**Restriction :** l'outil de ligne de commande n'est pas pris en charge par Cygwin. Utilisez-le dans une fenêtre de ligne de commande autre que Cygwin.
{:prereq}

Une fois l'interface de ligne de commande installée, vous pouvez commencer :

  1. {: download} Téléchargez le code de votre application dans un nouveau répertoire afin de configurer votre environnement de développement.
  
    <a class="xref" href="http://bluemix.net" target="_blank" title="(Ouverture dans un nouvel onglet ou une nouvelle fenêtre)"><img class="image" src="images/btn_starter-code.svg" alt="Télécharger le code de l'application" /> </a>

  2. Placez-vous dans le répertoire dans lequel se trouve votre code.

  <pre class="pre">cd <var class="keyword varname">votre_nouveau_répertoire</var></pre>

  3.  Modifiez le code de votre application si nécessaire. Par exemple, si vous utilisez une application exemple {{site.data.keyword.Bluemix}} et qu'elle contient le fichier `src/main/webapp/index.html`, vous pouvez le modifier et éditer "Thanks for creating ..." pour indiquer un nouveau contenu. Vérifiez que l'application s'exécute en local avant de la déployer à nouveau dans {{site.data.keyword.Bluemix_notm}}.

    Tenez compte du fichier `manifest.yml`. Lorsque vous déployez à nouveau votre application dans {{site.data.keyword.Bluemix_notm}}, il est utilisé pour déterminer l'adresse URL de votre application, l'allocation de mémoire, le nombre d'instance et d'autres paramètres essentiels. Vous pouvez [en apprendre davantage sur le fichier manifeste ![](../icons/launch-glyph.svg "")](https://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html){: new_window} dans la documentation Cloud Foundry. 

    Prêtez également attention au fichier `README.md`, qui contient des détails tels que les instructions de génération, le cas échéant.

    Remarque : Si votre application est une application Liberty, vous devez la générer avant de la redéployer.

  4. Connectez-vous à {{site.data.keyword.Bluemix_notm}}.

  <pre class="pre">cf api https://api.<span class="keyword" data-hd-keyref="DomainName">nom_domaine</span></pre>

  <pre class="pre">cf login -u <var class="keyword varname" data-hd-keyref="user_ID">nom_utilisateur</var> -o
<var class="keyword varname" data-hd-keyref="org_name">nom_organisation</var> -s <var class="keyword varname" data-hd-keyref="space_name">nom_espace</var></pre>

  Si vous vous servez d'un ID fédéré, utilisez l'option `-sso`.

  <pre class="pre">cf login -u <var class="keyword varname" data-hd-keyref="user_ID">nom_utilisateur</var> -o <var class="keyword varname" data-hd-keyref="org_name">nom_organisation</var> -s <var class="keyword varname" data-hd-keyref="space_name">nom_espace</var> -sso</pre>

  5. A partir de <var class="keyword varname">votre_nouveau_répertoire</var>, redéployez votre application dans {{site.data.keyword.Bluemix_notm}} à l'aide de la commande `cf push`. Pour plus d'informations sur la commande `cf push`, voir [Téléchargement de votre application](/docs/starters/upload_app.html).

  <pre class="pre">cf push <var class="keyword varname" data-hd-keyref="app_name">nom_app</var></pre>

  6. Accédez à votre application via https://<var class="keyword varname" data-hd-keyref="app_name">nom_app</var>.<span class="keyword" data-hd-keyref="APPDomain">NomDomaineApp</span>.
