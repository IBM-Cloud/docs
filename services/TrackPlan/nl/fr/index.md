{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#Initiation au service {{site.data.keyword.trackplan}}{: #track-plan}  

*Dernière mise à jour : 21 janvier 2016*

Pour afficher, éditer et planifier des tâches, utilisez {{site.data.keyword.trackplanlong}} (le
service {{site.data.keyword.trackplan}}). Vous pouvez effectuer le suivi de votre travail et du travail de votre
équipe, créer des incidents, consulter le travail entrant, gérer votre journal des éléments en attente et planifier le travail pour des sprints futurs.
{: shortdesc}

Le service {{site.data.keyword.trackplan}} lie les plans et le code pour que les plans restent
synchronisés avec la progression de l'équipe de développement. Grâce à ce service, vous pouvez créer des cas d'utilisation, des tâches et des incidents
afin de décrire le travail du projet et d'en effectuer le suivi. Vous pouvez aussi planifier et gérer le journal des éléments en attente du produit, des
éditions et des sprints.

1. Connectez-vous à {{site.data.keyword.Bluemix_notm}} et sélectionnez une organisation et un espace pour
votre application.
1. Dans le tableau de bord {{site.data.keyword.Bluemix_notm}}, cliquez sur **Créer une application**.
1. Sélectionnez un modèle d'application Web ou mobile, sélectionnez un module de démarrage et cliquez sur **Continuer**. Donnez un
nom à votre application, puis cliquez sur **Terminer**.
1. Faites défiler la page Commencer le codage et cliquez sur **Afficher la présentation de l'application**.
1. Dans le tableau de bord des applications {{site.data.keyword.Bluemix_notm}}, créez un projet hébergé par
Git pour l'application en cliquant sur **Ajouter un référentiel Git**. Veillez à ce que la case **Remplir le référentiel avec le package d'applications du module de démarrage et activer Delivery Pipeline (Build & Deploy)** soit cochée, puis cliquez sur **Continuer**. Une
fois votre référentiel Git créé, cliquez sur **Fermer**. Le lien Ajouter un référentiel Git est remplacé par le
lien Editer le code et l'adresse URL de votre référentiel Git.
1. Ajoutez le service {{site.data.keyword.trackplan}} à l'espace pour pouvoir gérer le travail de votre
équipe.
    1. Dans le tableau de bord des applications {{site.data.keyword.Bluemix_notm}}, cliquez sur **Ajouter un service ou une API**. Pour la catégorie, sélectionnez **DevOps** et dans le catalogue, cliquez sur **Track & Plan**.
    2. Dans la page {{site.data.keyword.trackplan}}, sélectionnez un plan et cliquez sur
**Créer**.    
1. Dans la liste des applications, dans la colonne Etat, changez l'état du service
{{site.data.keyword.trackplan}} en cliquant sur l'état en cours, qui dans ce cas est **OFF**. La page des paramètrs du projet s'ouvre dans {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}}.
    1. Sélectionnez l'option permettant d'activer le service {{site.data.keyword.trackplan}}. Si nécessaire,
mettez à jour votre région, votre organisation ou votre espace.
    2. Cliquez sur **Sauvegarder**.  
1. Revenez au tableau de bord {{site.data.keyword.Bluemix_notm}} et cliquez sur le service {{site.data.keyword.trackplan}}. L'état du service {{site.data.keyword.trackplan}} est devenu
**ON** pour votre application.
1. Dans la liste des applications, dans la colonne Elément de travail, cliquez sur **Créer** pour commencer à utiliser
le service {{site.data.keyword.trackplan}}.  

Dans le tableau de bord {{site.data.keyword.Bluemix_notm}}, vous pouvez voir vos projets {{site.data.keyword.jazzhub_short}}, ainsi que le nombre de leurs membres, leur visibilité et si le service {{site.data.keyword.trackplan}} est activé pour chacun d'eux. Vous pouvez créer des éléments de travail pour n'importe lequel
de vos projets {{site.data.keyword.jazzhub_short}} ou accéder à vos outils de planification.  

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
<li><img src="./sout.gif" alt=""><a href="http://www.ibm.com/developerworks/topics/track%20and%20plan%20service" rel="external" title="(S'ouvre dans un nouvel onglet ou une nouvelle fenêtre)">developerWorks : service {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.trackplan}}</a></li>
</ul>
</div>
</aside>
</article>
