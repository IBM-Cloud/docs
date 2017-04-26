---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Analyse de journaux depuis l'interface CLI
{: #analyzing_logs_cli}

Dans {{site.data.keyword.Bluemix}}, vous pouvez visualiser, filtrer et analyser des journaux depuis l'interface de ligne de commande. Utilisez la ligne de commande pour gérer des journaux à l'aide d'un programme. 
{:shortdesc}

Pour analyser des journaux d'application Cloud Foundry (CF), utilisez les commandes suivantes : `cf logs`.
Pour plus d'informations, voir [Analyse de journaux d'application CF depuis l'interface CLI](logging_view_cli.html#analyzing_cf_logs_cli).

Pour analyser des journaux de conteneur Docker, utilisez la commande suivante : `cf ic logs`.
Pour plus d'informations, voir [Analyse de journaux de conteneur Docker depuis l'interface CLI](logging_view_cli.html#analyzing_container_logs_cli).


## Analyse des journaux d'application CF depuis l'interface de ligne de commande
{: #analyzing_cf_logs_cli}

Utilisez la commande **cf logs** pour afficher des journaux depuis une application Cloud Foundry et depuis les composants système qui interagissent avec lui lorsque vous déployez l'application dans {{site.data.keyword.Bluemix_notm}}. La commande **cf logs** affiche les flux de journalisation de sortie standard et d'erreur standard d'une application Cloud Foundry.

Pour afficher les journaux qui vous intéressent ou exclure le contenu que vous ne voulez pas afficher, vous pouvez utiliser la commande **cf logs** avec des options de filtrage telles que **cut** et **grep** dans l'interface de ligne de commande cf :

* Pour afficher les journaux d'une application Cloud Foundry, voir [Affichage du journal d'une application Cloud Foundry](logging_view_cli.html#full_log_cli).
* Pour afficher les derniers enregistrements de journal d'une application Cloud Foundry, voir [Affichage des dernières entrées de journal d'une application Cloud Foundry](logging_view_cli.html#tailing_log_cli).
* Pour afficher les enregistrements de journal d'une application Cloud Foundry pour une période donnée, voir [Affichage d'une section d'un journal](logging_view_cli.html#partial_log_cli).
* Pour afficher les entrées des journaux d'une application Cloud Foundry qui contiennent des mots clés spécifiques, voir [Affichage d'entrées de journal contenant certains mots clés](logging_view_cli.html#partial_by_keyword_log_cli).


## Analyse de journaux de conteneur Docker depuis l'interface CLI
{: #analyzing_container_logs_cli}

Utilisez la commande `cf ic logs` pour afficher les journaux d'un conteneur dans {{site.data.keyword.Bluemix_notm}}. Vous pouvez, par exemple, utiliser les journaux pour comprendre pourquoi un conteneur s'est arrêté ou pour examiner la sortie du conteneur. 

Pour examiner les erreurs d'application de l'application s'exécutant dans un conteneur via la commande `cf ic logs`, l'application doit consigner ses journaux dans les flux de sortie standard (STDOUT) et d'erreur standard (STDERR). Si vous concevez votre application pour consignation dans ces flux de sortie standard, vous pouvez consulter les journaux via la ligne de commande même si le conteneur est arrêté ou en panne.

Pour plus d'informations sur la commande `cf ic logs`, voir [Commande cf ic logs](/docs/containers/container_cli_reference_cfic.html#container_cli_reference_cfic__logs).


## Affichage du journal d'une application Cloud Foundry
{: #full_log_cli}

Pour afficher tous les journaux disponibles pour une application Cloud Foundry, procédez comme suit :

1. Ouvrez un terminal et connectez-vous à {{site.data.keyword.Bluemix}}.

2. En ligne de commande, exécutez la commande suivante pour afficher tous les journaux :

   <pre class="pre screen"><code>cf logs <var class="keyword varname">nom_app</var></code></pre>
   
   
## Affichage des dernières entrées de journal d'une application Cloud Foundry
{: #tailing_log_cli}

Pour afficher les derniers journaux disponibles pour une application Cloud Foundry, procédez comme suit :

1. Ouvrez un terminal et connectez-vous à {{site.data.keyword.Bluemix}}.

2. En ligne de commande, exécutez la commande suivante pour afficher tous les journaux :

     <pre class="pre screen"><code>cf logs <var class="keyword varname">nom_app</var> --recent</code></pre>

<div class="note tip"><span class="tiptitle">Astuce :</span> lorsque vous exécutez la commande <span class="keyword cmdname">cf push</span> ou <span class="keyword cmdname">cf start</span> dans une seule fenêtre de ligne de commande, vous pouvez entrer <samp class="ph codeph">cf logs nom_app --recent</samp> dans une autre fenêtre de ligne de commande pour afficher les journaux en temps réel. </div>


## Affichage d'une section d'un journal Cloud Foundry
{: #partial_log_cli}

Pour afficher une partie des journaux disponibles pour une application Cloud Foundry pour une période donnée, procédez comme suit :

1. Ouvrez un terminal et connectez-vous à {{site.data.keyword.Bluemix}}.

2. En ligne de commande, exécutez la commande suivante pour afficher tous les journaux :

    <pre class="pre screen"><code>cf logs <var class="keyword varname">nom_app</var> --recent  | cut -c 29-40,46-</code></pre>
    
    Pour plus d'informations sur l'option **cut**, entrez **cut --help**.


## Affichage d'entrées de journal contenant certains mots clés
{: #partial_by_keyword_log_cli}

Pour afficher les entrées de journal contenant certains mots clés pour une application Cloud Foundry, procédez comme suit :

1. Ouvrez un terminal et connectez-vous à {{site.data.keyword.Bluemix}}.

2. En ligne de commande, exécutez la commande suivante pour afficher tous les journaux :

    <pre class="pre screen"><code>cf logs <var class="keyword varname">nom_app</var> --recent | grep '<var class="keyword varname">mot clé</var>'</code></pre>
    

Par exemple, pour afficher les entrées de journal contenant le mot clé **APP**, utilisez la commande suivante :

<pre class="pre screen"><code>cf logs nom_app --recent | grep '\[App' </code></pre>

Pour plus d'informations sur l'option **grep**, entrez **grep --help**.


## Journaux des applications Cloud Foundry
{: #cf_app_logs_cli}

Les journaux suivants sont disponibles pour une application Cloud Foundry après que vous l'avez déployée dans {{site.data.keyword.Bluemix}} :

**buildpack.log**

Ce fichier journal enregistre des événements d'information à granularité fine pour le débogage. Vous pouvez l'utiliser pour identifier les problèmes liés à l'exécution du pack de construction.

Pour générer des données dans le fichier *buildpack.log*, vous devez activer le traçage de pack de construction via la commande : `cf set-env nom_application JBP_LOG_LEVEL DEBUG`
   
Pour consulter ce journal, entrez la commande suivante : `cf files nom_application app/.buildpack-diagnostics/buildpack.log`


**staging_task.log**

Ce fichier journal enregistre des messages après les étapes principales de la tâche de constitution. Vous pouvez l'utiliser pour identifier les problèmes liés à la constitution.

Pour consulter ce journal, entrez la commande suivante : `cf files nom_application logs/staging_task.log`


**Remarque :** pour des informations sur l'activation de la journalisation des applications, voir [Débogage d'erreurs d'exécution](/docs/debug/index.html#debugging-runtime-errors).



