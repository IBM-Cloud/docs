---



copyright:

  years: 2015, 2017

lastupdated: "2017-04-19"



---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Téléchargement de votre application

Une fois que vous êtes connecté à {{site.data.keyword.Bluemix}}, vous pouvez télécharger votre application à l'aide de la commande `bluemix app push`.
{:shortdesc}

Avant de commencer, effectuez les opérations suivantes :
  1. Installez l'interface de ligne de commande {{site.data.keyword.Bluemix}}. 

  <a class="xref" href="http://clis.ng.bluemix.net/ui/home.html" target="_blank" title="(Ouverture dans un nouvel onglet ou une nouvelle fenêtre)"><img class="image" src="images/btn_bx_commandline.svg" alt="Télécharger l'interface de ligne de commande {{site.data.keyword.Bluemix}}" /> </a> 

  2. Connectez-vous à {{site.data.keyword.Bluemix}}.

  <pre class="pre"><code class="hljs">bluemix api https://api.<span class="keyword" data-hd-keyref="DomainName">nom_domaine</span></code></pre>

  3. Connectez-vous à {{site.data.keyword.Bluemix_notm}}.

  <pre class="pre"><code class="hljs">bluemix login -u <var class="keyword varname" data-hd-keyref="user_ID">nom_utilisateur</var> -o <var class="keyword varname" data-hd-keyref="org_name">nom_org</var> -s <var class="keyword varname" data-hd-keyref="space_name">nom_espace</var></code></pre>

Lorsqu'une commande **bluemix app push** est émise, l'interface de ligne de commande met le répertoire de travail à disposition de l'environnement {{site.data.keyword.Bluemix_notm}}, qui utilise un pack de construction pour construire et exécuter l'application. 

  1. Depuis le répertoire de votre application, entrez la commande **bluemix app push** avec le nom de l'application. Le nom de l'application doit être unique dans l'environnement {{site.data.keyword.Bluemix_notm}}.

  <pre class="pre"><code class="hljs">bluemix app push <var class="keyword varname" data-hd-keyref="app_name">nom_application</var> -m 512m</code></pre>

  {{site.data.keyword.Bluemix_notm}} inclut des packs de construction intégrés. Dans certains cas, même pour les packs de construction intégrés, vous devez indiquer l'option -c afin de spécifier la commande qui est utilisée pour démarrer votre application. Par exemple, vous devez utiliser l'option -c pour envoyer votre application Node.js par commande push :

  <pre class="pre"><code class="hljs">bluemix app push <var class="keyword varname" data-hd-keyref="app_name">nom_application</var> -c start_command</code></pre>

  De plus, l'application Node.js doit contenir un fichier package.json valide.

  Tous les autres packs de construction externes doivent être envoyés par commande push avec l'option -b. Par exemple :

  <pre class="pre"><code class="hljs">bluemix app push <var class="keyword varname" data-hd-keyref="app_name">nom_application</var> -b buildpack_URL</code></pre>

  **Astuce :** Lorsque vous utilisez la commande **bluemix app push**, elle copie tous les fichiers et répertoires depuis votre répertoire de travail vers Bluemix. Assurez-vous que votre répertoire de travail contient uniquement les fichiers requis.

  
  2. Si vous modifiez votre application, vous pouvez télécharger ces modifications en entrant à nouveau la commande `bluemix app push`. La commande utilise vos options précédentes et vos réponses aux invites pour mettre à jour n'importe quelle instance en cours d'exécution de votre application avec les nouvelles parties de code.

L'interface de ligne de commande {{site.data.keyword.Bluemix}} regroupe une interface de ligne de commande cf dans son installation. En réalité, la commande `bluemix app push` appelle `cf push` pour télécharger et déployer votre application sur {{site.data.keyword.Bluemix_notm}}. Voir [Commandes cf](/docs/cli/reference/cfcommands/index.html) pour plus d'informations sur cf push. Voir [Utilisation de packs de construction de communauté](/docs/cfapps/byob.html) pour des informations sur les packs de construction.


**Astuce :** vous pouvez également télécharger ou déployer une application à partir de DevOps Services. Voir [Developing a {{site.data.keyword.Bluemix_notm}} application in Node.js with the Web IDE](https://hub.jazz.net/tutorials/devopsweb/){: new_window}.
