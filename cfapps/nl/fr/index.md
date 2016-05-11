---

 

copyright:

  2015，2016

 

---

{:shortdesc: .shortdesc} 
{:new_window: target="_blank"}

# Création d'applications Cloud Foundry
*Dernière mise à jour : 18 avril 2016*

Avec {{site.data.keyword.Bluemix}}, vous pouvez créer votre application dans l'interface utilisateur {{site.data.keyword.Bluemix_notm}}. Vous pouvez ensuite choisir de continuer à employer l'interface utilisateur,
l'interface de ligne de commande cf ou {{site.data.keyword.jazzhub_title}} pour développer, contrôler, planifier et déployer votre
application.
{:shortdesc}

Lorsque vous créez une application dans {{site.data.keyword.Bluemix_notm}}, vous devez commencer par le module de démarrage. Un *module de démarrage* est un modèle qui inclut des services prédéfinis et du code d'application configuré avec un pack de construction particulier. Il existe deux types de module de démarrage : les conteneurs boilerplate et les contextes d'exécution.

Un *conteneur boilerplate* regroupe une application, ainsi qu'un environnement d'exécution et des services prédéfinis qui lui sont associés pour un domaine particulier. Par exemple, le conteneur boilerplate Mobile Cloud inclut un contexte d'exécution Node.js, ainsi que les services Mobile Data, Mobile Application Security et Push. Il inclut également un logiciel SDK et des exemples d'application pour vous permettre de commencer à développer des applications mobiles qui accèdent à ces services.

Un *contexte d'exécution* est un ensemble de ressources utilisé pour exécuter une application. {{site.data.keyword.Bluemix_notm}} fournit des environnements d'exécution sous forme de conteneurs pour différents types d'application. Les environnements d'exécution sont intégrés sous forme de packs de construction dans {{site.data.keyword.Bluemix_notm}} ; ils sont configurés automatiquement et ne nécessitent pratiquement aucune maintenance.

Pour commencer à créer une application, procédez comme suit :
  1. Accédez au tableau de bord dans l'interface utilisateur {{site.data.keyword.Bluemix_notm}}.
  2. Cliquez sur **Créer une application**.
  3. Cliquez sur **Web** et suivez les instructions pour choisir un module de démarrage, spécifier un nom et sélectionner le mode de
codage.
  4. Une fois que vous avez terminé, cliquez sur **Afficher la vue d'ensemble de l'application**. La page Vue d'ensemble de votre
application s'affiche dans le tableau de bord.
  5. Vous pouvez ajouter un service à votre application en cliquant sur **AJOUTER UN SERVICE OU UNE API** dans la page
Vue d'ensemble de votre application
dans l'interface utilisateur Bluemix. Parcourez et sélectionnez des services dans le catalogue ou accédez à la fin du catalogue et cliquez sur
**Services expérimentaux {{site.data.keyword.Bluemix_notm}}** pour examiner ces services. Vous pouvez aussi
utiliser l'interface de
ligne de commande cf. Voir Options pour apprendre à utiliser les
applications.
  6. Dans la page Vue d'ensemble de l'application, cliquez sur Ajouter un référentiel Git pour sauvegarder la source de votre application
dans un
référentiel Git et créer un projet hébergé par Git. Vous pouvez également déployer l'application à partir d'{{site.data.keyword.jazzhub_title}}.

**Remarque :** si un service que vous liez à une application tombe en panne, il se peut que l'application s'arrête ou présente des
erreurs. {{site.data.keyword.Bluemix_notm}} ne redémarre pas automatiquement l'application pour assurer la
reprise suite à ces problèmes. Envisagez de coder votre application de sorte à identifier les indisponibilités, les exceptions et les pannes de connexion pour assurer
la reprise. Pour plus d'informations, voir la rubrique de traitement des incidents Les applications ne sont pas redémarrées automatiquement.

## Options pour la gestion des applications

Une fois que vous avez créé votre application, vous disposez de quelques options pour continuer à ajouter des services, construire l'application et la déployer :

<dl><dt>Interface de ligne de commande cf</dt>
<dd>Utilisez l'interface de ligne de commande cf pour mettre à jour votre application, créer une instance de service ou lier le service à votre application. Vous pouvez également utiliser l'interface de ligne de commande cloud-cli pour créer, mettre à jour et supprimer des offres de services.</dd>
<dt>Interface utilisateur {{site.data.keyword.Bluemix_notm}}</dt>
<dd>L'interface utilisateur {{site.data.keyword.Bluemix_notm}} permet de construire une application, et de choisir les services et les contextes d'exécution à combiner afin de résoudre vos problèmes métier.</dd>
<dt>{{site.data.keyword.jazzhub_title}}</dt>
<dd>Utilisez {{site.data.keyword.jazzhub_title}} pour créer une application dans le cloud et la déployer dans {{site.data.keyword.Bluemix_notm}}. Les services fournis par {{site.data.keyword.jazzhub_title}} incluent Track & Plan et Delivery Pipeline, qui sont proposés dans le
catalogue {{site.data.keyword.Bluemix_notm}} sous DevOps, mais également dans Web IDE et Git Hosting.</dd>
</dl>

## Conseils

Tenez compte des conseils suivants lorsque vous développez vos applications Web :

<dl><dt>Persistance</dt>
<dd>Ne spécifiez pas d'emplacement de stockage local pour vos applications. Même si une seule instance est en cours d'exécution, chaque instance de votre application peut être à tout moment redémarrée et déplacée vers une autre machine virtuelle, notamment pour des raisons d'équilibrage de charge. Tout
élément stocké en local est effacé lorsque l'application est déplacée ou supprimée. Utilisez l'un des services de magasin de données Bluemix pour la
persistance.</dd>
<dt>Limites de ressources</dt>
<dd>Prenez connaissance des limites relatives aux quantités de ressources qu'un compte d'essai peut utiliser. Ces limites sont les suivantes :
<table style="width:100%">
  <th>Type de ressource</th>	<th>Quantité maximale</th>
<tr><td>Nombre de services utilisés par toutes les applications</td> <td>10</td>
<tr><td>Mémoire utilisée dans toutes les applications</td> <td>	2 G</td>
<tr><td>Nombre de routes</td> <td>500</td>
</table>
</dd></dl>

*Tableau 1. Limites de ressources {{site.data.keyword.Bluemix_notm}} pour un compte d'essai*
