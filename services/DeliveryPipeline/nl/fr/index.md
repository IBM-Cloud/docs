---



copyright :

  years: 2015, 2016



---


{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}

# Initiation à {{site.data.keyword.deliverypipeline}} {: #delivery-pipeline}  

Dernière mise à jour : 15 septembre 2016
{: .last-updated}

Pour automatiser vos générations et vos déploiements dans {{site.data.keyword.Bluemix}}, utilisez IBM Continuous {{site.data.keyword.deliverypipeline}} for {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

Ces informations s'appliquent à
{{site.data.keyword.deliverypipeline}} et à
{{site.data.keyword.deliverypipeline}} Next.

Avec le service {{site.data.keyword.deliverypipeline}}, vous pouvez choisir entre plusieurs types de génération. Vous fournissez le script de génération et {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}} l'exécute ; il n'est pas nécessaire de configurer des systèmes de génération. Ensuite, en un clic, vous pouvez déployer automatiquement votre application dans un ou plusieurs espaces {{site.data.keyword.Bluemix_notm}}, sur un ou plusieurs serveurs Cloud Foundry publics, ou dans un ou plusieurs
conteneurs Docker dans IBM Containers for {{site.data.keyword.Bluemix_notm}}.  

Les travaux de génération compilent et conditionnent le code source de votre application depuis des référentiels Git ou de gestion de contrôle de
source Jazz (SCM). Ils génèrent des artefacts pouvant être déployés,
tels que des fichiers WAR ou des conteneurs Docker pour IBM Containers. De plus, vous pouvez
exécuter des tests unitaires dans votre génération automatiquement. A chaque fois que le code source change, une génération est déclenchée.

Un travail de déploiement prend la sortie d'un travail de génération et la déploie sur des serveurs IBM Containers ou Cloud Foundry tels que {{site.data.keyword.Bluemix_notm}}.  

Vous pouvez effectuer le déploiement dans une ou plusieurs régions et dans un ou plusieurs services. Par exemple, vous pouvez configurer votre
service {{site.data.keyword.deliverypipeline}} de sorte que les artefacts de développement utilisent IBM Containers, soient testés dans une région, et soient déployés pour la production
dans plusieurs régions. Pour plus d'informations, voir
[Régions](../../overview/index.html#ov_intro__reg).

Il existe plusieurs manières de créer un pipeline,
comme l'ajout d'un pipeline à une application existante et la
création d'un pipeline sans aucune application existante. Si votre
organisation n'a pas déjà un service
{{site.data.keyword.deliverypipeline}}, vous pouvez accéder
au catalogue, cliquer sur
{{site.data.keyword.deliverypipeline}} ou
{{site.data.keyword.deliverypipeline}} Next, puis sur Créer.

Procédez comme suit pour configurer un
{{site.data.keyword.deliverypipeline}} pour une
application existante :    

1. Dans le tableau de bord des applications {{site.data.keyword.Bluemix_notm}}, sur l'onglet Présentation et sous **Distribution continue**, créez un projet hébergé par Git pour l'application en cliquant sur **Ajouter le référentiel et le pipeline Git** ou **Ajouter un référentiel Git**, selon le contexte.
1. Assurez-vous que la case à cocher **Remplir le référentiel avec le package d'applications du module de démarrage et activer le pipeline Build & Deploy** est sélectionnée, puis cliquez sur **Continuer**. Vous devrez peut-être vérifier votre adresse électronique avant de poursuivre.  
1. Une
fois votre référentiel Git créé, cliquez sur **Fermer**. Le bouton Ajouter un référentiel Git est remplacé par un bouton Editer le code et votre URL Git.  
1. Pour ouvrir le pipeline, cliquez sur **Editer le code**, puis sur **Build & Deploy**. Pour exécuter le pipeline pour la première fois, insérez une modification dans le référentiel Git via une commande push.

Après avoir
ajouté ce service, vous pouvez créer un pipeline de déploiement en plusieurs étapes dans vos espaces
{{site.data.keyword.Bluemix_notm}}, en configurant et en exécutant des étapes contenant des
travaux de génération, de test et de déploiement. Le tableau de bord {{site.data.keyword.deliverypipeline}} affiche vos projets {{site.data.keyword.jazzhub_short}}, ainsi que leur état. Vous pouvez vérifier le statut des générations, de
l'application déployée et des déploiements récents, ou consulter les journaux les plus récents et les détails de déploiement.  

<article class="topic reference nested1" aria-labelledby="d68e338" lang="en-us" id="rellinks" role="article">
<h2 class="topictitle2" id="d68e338">Liens connexes</h2>
<aside role="complementary" aria-labelledby="related_links">
<div class="linklist" id="general"><h3 class="linklistlabel" id="related_links">Liens connexes</h3>
<ul>
<li><img src="./sout.gif" alt=""><a href="https://developer.ibm.com/bluemix/support/#prereqs" rel="external" title="(S'ouvre dans un nouvel onglet ou une nouvelle fenêtre)">Configuration requise pour {{site.data.keyword.Bluemix_notm}}</a></li>
<li><img src="./sout.gif" alt=""><a href="https://www.ibm.com/devops/method/content/deliver/practice_delivery_pipeline/" rel="external" title="(S'ouvre dans un nouvel onglet ou une nouvelle fenêtre)">IBM Bluemix Garage Method: Delivery pipeline</a></li>
</ul>
</div>

<div class="linklist" id="samples">
<h3 class="linklistlabel">Tutoriels et exemples</h3>
<ul>

<!--
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/devopsweb/" rel="external" title="(Opens in a new tab or window)">Clone, edit, and deploy an app</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditor" rel="external" title="(Opens in a new tab or window)">Develop and deploy a Node.js app</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditorjava" rel="external" title="(Opens in a new tab or window)">Develop and deploy a Java app</a></li>
-->

<li><img src="./sout.gif" alt=""><a href="http://www.ibm.com/developerworks/topics/delivery%20pipeline%20service" rel="external" title="(S'ouvre dans un nouvel onglet ou une nouvelle fenêtre)">developerWorks : service {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.deliverypipeline}}</a></li>
</ul>
</div>
</aside>
</article>
