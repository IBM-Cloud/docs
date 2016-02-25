{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}

#Initiation à {{site.data.keyword.deliverypipeline}} {: #delivery-pipeline}  

*Dernière mise à jour : 21 janvier 2016*

Pour automatiser vos générations et vos déploiements dans {{site.data.keyword.Bluemix}}, utilisez IBM Continuous {{site.data.keyword.deliverypipeline}} for {{site.data.keyword.Bluemix_notm}} (le service {{site.data.keyword.deliverypipeline}}).
{: shortdesc} 

Lorsque vous développez une application dans le cloud, vous avez le choix entre plusieurs types de génération. Vous fournissez le script de génération et {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}} l'exécute ; il n'est pas nécessaire de configurer des systèmes de génération. Ensuite, en un clic, vous pouvez déployer automatiquement votre application dans un ou plusieurs espaces {{site.data.keyword.Bluemix_notm}}, sur un ou plusieurs serveurs Cloud Foundry publics, ou dans un ou plusieurs
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

1. Connectez-vous à {{site.data.keyword.Bluemix_notm}} et sélectionnez une organisation et un espace pour
votre application.
1. Dans le tableau de bord {{site.data.keyword.Bluemix_notm}}, cliquez sur **Créer une application**.
1. Sélectionnez un modèle d'application Web ou mobile, sélectionnez un module de démarrage, et cliquez sur **Continuer**. Donnez un
nom à votre application, puis cliquez sur **Terminer**.  
1. Faites défiler la page Commencer le codage et cliquez sur **Afficher la présentation de l'application**.  
1. Dans le tableau de bord des applications {{site.data.keyword.Bluemix_notm}}, créez un projet hébergé par
Git pour l'application en cliquant sur **Ajouter un référentiel Git**. Veillez à ce que la case **Remplir le référentiel avec le package d'applications du module de démarrage et activer {{site.data.keyword.deliverypipeline}} (Build & Deploy)** soit cochée, puis cliquez sur **Continuer**.   
1. Une
fois votre référentiel Git créé, cliquez sur **Fermer**. Le lien Ajouter un référentiel Git est remplacé par le
lien Editer le code et l'adresse URL de votre référentiel Git.  
1. Ajoutez le service {{site.data.keyword.deliverypipeline}} à l'espace ou aux espaces associés. Après avoir
ajouté ce service, vous pouvez créer un pipeline de déploiement en plusieurs étapes dans vos espaces
{{site.data.keyword.Bluemix_notm}}, en configurant et en exécutant des étapes contenant des
travaux de génération, de test et de déploiement.
    1. Dans le tableau de bord des applications {{site.data.keyword.Bluemix_notm}}, cliquez sur **Ajouter un service ou une API**. Pour la catégorie, cochez la case **DevOps** et, dans le catalogue, cliquez sur **Delivery Pipeline**.
    2. Sélectionnez un plan et cliquez sur **Créer**. Le tableau de bord {{site.data.keyword.deliverypipeline}} s'ouvre et affiche l'application que vous avez créée précédemment.     
  
Le tableau de bord {{site.data.keyword.deliverypipeline}} affiche vos projets {{site.data.keyword.jazzhub_short}}, ainsi que leur état. Vous pouvez vérifier le statut des générations, de
l'application déployée et des déploiements récents, ou consulter les journaux les plus récents et les détails de déploiement.  

<article class="topic reference nested1" aria-labelledby="d68e338" lang="en-us" id="rellinks">
<h2 class="topictitle2" id="d68e338">Liens connexes</h2>
<aside>
<div class="linklist" id="general"><h3 class="linklistlabel">Liens connexes</h3>
<ul>
<li><img src="./sout.gif" alt=""><a href="https://developer.ibm.com/bluemix/support/#prereqs" rel="external" title="(S'ouvre dans un nouvel onglet ou une nouvelle fenêtre)">Configuration requise pour {{site.data.keyword.Bluemix_notm}}</a></li>
</ul>
</div>

<div class="linklist" id="samples">
<h3 class="linklistlabel">Tutoriels et exemples</h3>
<ul>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/devopsweb/" rel="external" title="(S'ouvre dans un nouvel onglet ou une nouvelle fenêtre)">Clonez, éditez et déployez une application</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditor" rel="external" title="(S'ouvre dans un nouvel onglet ou une nouvelle fenêtre)">Développez et déployez une appli Node.js</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditorjava" rel="external" title="(S'ouvre dans un nouvel onglet ou une nouvelle fenêtre)">Développez et déployez une appli Java</a></li>
<li><img src="./sout.gif" alt=""><a href="http://www.ibm.com/developerworks/topics/delivery%20pipeline%20service" rel="external" title="(S'ouvre dans un nouvel onglet ou une nouvelle fenêtre)">developerWorks : service {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.deliverypipeline}}</a></li>
</ul>
</div>
</aside>
</article>
