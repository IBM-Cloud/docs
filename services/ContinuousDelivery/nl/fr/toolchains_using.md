---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Utilisation de chaînes d'outils sur {{site.data.keyword.Bluemix_notm}} public
{: #toolchains-using}

Dernière mise à jour : 9 novembre 2016
{: .last-updated}

Vous pouvez utiliser une chaîne d'outils pour améliorer la productivité de votre travail quotidien de développement, de déploiement et de vos opérations. Après avoir configuré une chaîne d'outils, vous pouvez ajouter, supprimer ou configurer des intégrations d'outils et gérer l'accès à la chaîne d'outils. Les chaînes d'outils sont disponibles uniquement dans la région sud des Etats-Unis.
{: shortdesc}

## Configuration d'une intégration d'outil
{: #configuring_a_tool_integration}

Si vous avez différé la configuration d'une intégration d'outil lors de la création d'une chaîne d'outils, un bouton **Configurer** s'affiche sur sa vignette. Si vous avez configuré une intégration d'outil à la création d'une chaîne d'outils, vous pouvez mettre à jour les paramètres de configuration.

1. Dans le tableau de bord DevOps, dans la page **Chaînes d'outils**, cliquez sur une chaîne d'outils afin d'ouvrir la page Vue
d'ensemble correspondante. Vous pouvez également cliquer sur
**Afficher la chaîne d'outils**, puis sur **Vue d'ensemble**, depuis la page Vue d'ensemble de l'application, sur la
vignette Continuous Delivery.
1. Si vous devez configurer une intégration d'outil pour la première fois, depuis sa vignette, cliquez sur **Configurer**.

  ![Bouton Configurer](images/toolchain_tile_configure.png)

 Lorsque vous avez terminé la configuration de l'intégration d'outil, cliquez sur **Sauvegarder l'intégration**.
 
1. Si vous devez mettre à jour la configuration d'une intégration d'outil, depuis sa vignette, cliquez sur le menu pour accéder aux options de configuration.

  ![Menu Configuration](images/toolchain_tile_menu.png)
 
 Lorsque vous avez terminé la mis à jour des paramètres, cliquez sur **Sauvegarder l'intégration**.

## Ajout d'une intégration d'outil
{: #adding_a_tool_integration}

Vous pouvez ajouter et configurer des intégrations d'outils pour votre chaîne d'outils.

1. Dans le tableau de bord DevOps, dans la page **Chaînes d'outils**, cliquez sur une chaîne d'outils afin d'ouvrir la page Vue
d'ensemble correspondante. Vous pouvez également cliquer sur
**Afficher la chaîne d'outils**, puis sur **Vue d'ensemble**, depuis la page Vue d'ensemble de l'application, sur la
vignette Continuous Delivery.
1. Pour afficher la liste des intégrations d'outils à ajouter, cliquez sur **Ajouter un outil**.
1. Cliquez sur une intégration d'outil à ajouter.
1. Entrez les informations requises pour configurer l'intégration d'outil. 
1. Cliquez sur **Créer une intégration** pour ajouter l'intégration d'outil à votre chaîne d'outils.

## Suppression d'une intégration d'outil
{: #deleting_a_tool_integration}

Si vous supprimez une intégration d'outil de votre chaîne d'outils, la suppression est irréversible. 

1. Dans le tableau de bord DevOps, dans la page **Chaînes d'outils**, cliquez sur une chaîne d'outils afin d'ouvrir la page Vue
d'ensemble correspondante. Vous pouvez également cliquer sur
**Afficher la chaîne d'outils**, puis sur **Vue d'ensemble**, depuis la page Vue d'ensemble de l'application, sur la
vignette Distribution continue.
1. Sur la vignette de l'intégration d'outil à supprimer, cliquez sur le menu pour accéder aux options de configuration.
1. Pour supprimer l'intégration d'outil de votre chaîne d'outils, cliquez sur **Supprimer**.
1. Confirmez en cliquant sur **Supprimer**.  

## Gestion des accès
{: #managing_access}

Vous pouvez accorder l'accès à une chaîne d'outils à des utilisateurs en les ajoutant à l'organisation (org) à laquelle la chaîne d'outils est associée. Chaque chaîne d'outils est associée à une organisation spécifique, et tout membre de cette organisation peut accéder aux chaînes d'outils associées. L'organisation au sein de laquelle vous travaillez actuellement s'affiche dans la barre de menus. Cliquez sur l'organisation et changez d'organisation pour accéder
à un ensemble différent de chaînes d'outils.

1. Dans le tableau de bord DevOps, sur la page **Chaînes d'outils**, cliquez sur la chaîne d'outils à gérer puis cliquez sur **Gérer**. Vous pouvez également, depuis la page de présentation de l'application, sur la vignette Continuous Delivery, cliquer sur **Afficher la chaîne d'outils** puis sur **Gérer**.  
1. Cliquez sur le lien de votre organisation. 
1. Dans la page de gestion des organisations, cliquez sur **Inviter un utilisateur** et entrez l'adresse électronique de l'utilisateur.
1. Si vous souhaitez donner des droits avancés à des responsables {{site.data.keyword.Bluemix_notm}} d'organisations, sélectionnez une ou plusieurs des cases à cocher **Responsable**, **Responsable de la facturation** et **Auditeur**.
1. Cliquez sur **INVITER**.
1. Cliquez sur **SAUVEGARDER**.

## Suppression d'une chaîne d'outils
{: #deleting_a_toolchain}

Vous pouvez supprimer une chaîne d'outils et spécifier les intégrations d'outils associées à supprimer. Lorsque vous supprimez une chaîne d'outils, la suppression est irréversible.

1. Dans le tableau de bord DevOps, sur la page **Chaînes d'outils**, cliquez sur la chaîne d'outils à supprimer puis cliquez sur **Gérer**. Vous pouvez également, depuis la page de présentation de l'application, sur la vignette Continuous Delivery, cliquer sur **Afficher la chaîne d'outils** puis sur **Gérer**.
1. Cliquez sur **Supprimer la chaîne d'outils**, examinez et modifiez éventuellement la liste des intégrations d'outils à supprimer.
1. Confirmez la suppression en entrant le nom de la chaîne d'outils et en cliquant sur **Supprimer**.  

 **Conseil **: Lorsque vous supprimer une intégration d'outil GitHub, le référentiel GitHub associé n'est pas supprimé de GitHub. Vous devez supprimer manuellement le référentiel depuis GitHub.


# Liens connexes
{: #rellinks}

## Tutoriels et exemples
{: #samples}

* [Créer et utiliser votre première chaîne d'outils (ce lien ouvre une
nouvelle fenêtre)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_flow){:new_window}
* [Créer une chaîne d'outils personnalisée (ce lien ouvre une nouvelle
fenêtre)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_custom){:new_window}
* [Créer une application avec trois microservices (ce lien ouvre une
nouvelle fenêtre)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_microservices){:new_window}
* [Create a toolchain from a template on {{site.data.keyword.Bluemix_notm}} Dedicated (Beta) (Lien s'ouvrant dans une nouvelle fenêtre)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_template_flow){:new_window}
* [Create a toolchain from an app on {{site.data.keyword.Bluemix_notm}} Dedicated (Beta) (Lien s'ouvrant dans une nouvelle fenêtre)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_app_flow){:new_window}

## Liens connexes
{: #general}

* [Chaîne d'outils de microservices (ce lien ouvre une nouvelle
fenêtre)](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [Chaîne d'outils simple (ce lien ouvre une nouvelle
fenêtre)](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM Bluemix Garage Method (Lien s'ouvrant dans une nouvelle fenêtre)](https://www.ibm.com/devops/method){:new_window}
