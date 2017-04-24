---

copyright:
  years: 2015, 2017
lastupdated: "2017-3-21"

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Mise à niveau de votre projet {{site.data.keyword.jazzhub_short}} vers une chaîne d'outils
{: #upgrade_projects}

{{site.data.keyword.jazzhub}} évolue vers {{site.data.keyword.contdelivery_full}}. Dans le cadre de cette modification, les projets sont mis à niveau vers des chaînes d'outils. 

Vous pouvez mettre à niveau votre projet ou attendre qu'il soit automatiquement mis à niveau. Pour une meilleure expérience, mettez à niveau votre projet dès que possible afin de pouvoir contrôler le nom de votre chaîne d'outils et l'organisation dans laquelle elle est créée.   
{: shortdesc}

## Chaînes d'outils
{: #compare_toolchains}

Les chaînes d'outils sont semblables à des projets, à quelques différences importantes près :

- Les projets ne peuvent avoir qu'un seul référentiel et qu'un seul pipeline. Les chaînes d'outils peuvent avoir autant de référentiels et de pipelines que nécessaire.
- Les chaînes d'outils peuvent inclure des outils qui ne sont pas disponibles dans des projets, tels que Slack, Sauce Labs, PagerDuty et {{site.data.keyword.DRA_full}}.
- L'accès aux chaînes d'outils est géré via des organisations Bluemix standard. L'appartenance est gérée au niveau de l'organisation, contrairement aux projets, où elle est gérée au niveau du projet.

Pour en savoir plus sur les chaînes d'outils, consultez [YouTube![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://youtu.be/2SIPE1e7NJ4){: new_window} ou la section [Initiation à {{site.data.keyword.contdelivery_short}}](/docs/services/ContinuousDelivery/index.html).
[![Lien externe vers YouTube](images/CD_video.png)](https://youtu.be/2SIPE1e7NJ4){: new_window}    

## Conditions préalables requises
{: #upgrade_prereqs}    

- Pour accéder à la chaîne d'outils de votre projet mis à niveau, vous avez besoin d'un ID Bluemix. Avant la mise à niveau, vous devez vérifier que vous disposez d'un ID Bluemix actif. Si vous n'en possédez pas, [enregistrez-vous](https://console.ng.bluemix.net/registration/) pour en obtenir un.
- Vérifiez que le propriétaire de votre projet DevOps Services est correct. La chaîne d'outils créée à partir de votre projet fera partie de l'organisation Bluemix de ce propriétaire. 

**Important :** L'interface Eclipse Orion {{site.data.keyword.webide}} dans la chaîne d'outils est distincte de l'interface {{site.data.keyword.webide}} qui est associée à votre projet. Si vous utilisez l'interface {{site.data.keyword.webide}} et que certaines modifications ne sont pas validées, validez-les avant la mise à niveau.   


## Mise à niveau d'un projet vers une chaîne d'outils
{: #project_to_toolchain}

Lorsque votre projet est prêt pour la mise à niveau, un message s'affiche sur la carte du projet et la page de présentation.

![Image d'une carte portant le libellé Ready To Upgrade](images/card-project-to-upgrade.png)

![Message Time to Upgrade](images/banner-ready-to-upgrade.png)

**Astuce :** Les projets prêts pour la mise à niveau se trouvent dans le menu de la page Mes projets : 

![Image de l'élément de menu Projects To Upgrade](images/menu-projects-to-upgrade.png)

## Démarrage du processus de mise à niveau
{: #start_upgrade}

Avant de débuter le processus de mise à niveau, vous pouvez l'observer en action sur [YouTube![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://youtu.be/oaZVGveVxBg){: new_window}.
[![Lien externe vers YouTube](images/migration-video2.png)](https://youtu.be/oaZVGveVxBg){: new_window}    
Pour mettre à niveau votre projet vers une chaîne d'outils, procédez comme suit :

1. Pour démarrer le processus de mise à niveau, dans le message de la bannière, cliquez sur **upgrade now**. La page "Project upgrade toolchain" s'ouvre.  

   ![Exemple de page de mise à niveau](images/project-upgrade-toolchain.png)

   Pour une présentation du processus de mise à niveau, lisez la description sur cette page. Dans ce cas, le projet utilisant un référentiel sur GitHub.com, la chaîne d'outils est connectée au même référentiel GitHub. La chaîne d'outils inclut un nouveau pipeline qui contient les mêmes étapes et travaux que le pipeline du projet. En outre, la chaîne d'outils contient un pointeur vers l'interface Eclipse Orion {{site.data.keyword.webide}} qui s'exécute dans {{site.data.keyword.contdelivery_short}}.

2. Pour personnaliser la chaîne d'outils, vous pouvez configurer quelques paramètres :

   - Pour changer le nom de la chaîne d'outils, modifiez la zone **Nom**.

      ![Zone Nom](images/name-change.png)

   - Pour modifier l'organisation {{site.data.keyword.Bluemix_notm}} dans laquelle créer la chaîne d'outils, sélectionnez l'organisation dans le menu de votre compte :

      ![Choix de l'organisation Bluemix](images/bluemix-organization-chooser.png)

   Les chaînes d'outils étant gérées au niveau de l'organisation, veillez à sélectionner une organisation où les membres du projet qui ont besoin d'accéder à la chaîne d'outils existent déjà ou peuvent être ajoutés.  
  
3. Cliquez sur **Créer**. La chaîne d'outils est créée et sa page de présentation s'affiche.

   ![Présentation de la chaîne d'outils mise à niveau](images/new-toolchain-page.png)

   - Pour accéder à votre référentiel GitHub ou au suivi de problème associé, cliquez sur **GitHub** ou **Problèmes**.
   
   - Pour accéder à votre pipeline, cliquez sur **Delivery Pipeline**.  
   
   - Pour accéder à l'interface {{site.data.keyword.webide}}, qui inclut le contenu de votre référentiel qui a été réservé dans l'espace de travail, cliquez sur l'interface **Eclipse Orion {{site.data.keyword.webide}}**. 

## Révision de votre projet
{: #revisit_projects}

Vous êtes prêt à utiliser votre nouvelle chaîne d'outils. Votre projet s'intitule maintenant "Upgraded" et un message de confirmation s'affiche sur la page de présentation. 

![Image de la carte du projet avec le libellé Upgraded](images/card-upgraded-project.png)

![Projet mis à niveau](images/banner-upgraded.png)

Vous pouvez voir quels projets sont mis à niveau en sélectionnant **Upgraded Projects** dans le menu de la page Mes projets. 

![Image de l'élément de menu Upgraded Projects](images/menu-upgraded-projects.png)

Pour annuler la mise à niveau, supprimez votre chaîne d'outils. Ensuite, lorsque vous retournez sur la page de présentation du projet, le message de mise à niveau s'affiche à nouveau et vous pouvez effectuer une nouvelle mise à niveau lorsque vous êtes prêt. 

## Etapes suivantes
{: #upgrade_next_steps}   

1. Confirmez que la mise à niveau est terminée en recherchant le message sur la page de présentation du projet :    

   ![Projet mis à niveau](images/banner-upgraded.png)    

2. Accordez l'accès à la chaîne d'outils aux membres de votre équipe.     
    - Chaque membre de l'équipe doit disposer d'un compte Bluemix valide. Les membres de l'équipe qui ne possèdent pas de comptes doivent [s'enregistrer![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/registration){:new_window}.
    - Ajoutez des membres de l'équipe à l'organisation (org) à laquelle appartient la chaîne d'outils. 
3. Utilisez les outils de votre chaîne d'outils au lieu des outils de votre projet {{site.data.keyword.jazzhub_short}}. Par exemple, pour modifier le code à partir d'un navigateur, utilisez l'interface IDE Web de votre chaîne d'outils.    

## Traitement des incidents
{: #upgrade_troubleshoot}    

En cas de questions ou de problèmes, envoyez un courrier électronique à l'adresse [hub@jazz.net](mailto:hub@jazz.net). Dans votre courrier électronique, incluez les URL vers votre projet {{site.data.keyword.jazzhub_short}} et votre chaîne d'outils {{site.data.keyword.contdelivery_short}}. 

