---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Utilisation de chaînes d'outils sur {{site.data.keyword.Bluemix_notm}} dédié
{: #toolchains-using_dedicated}

Dernière mise à jour : 13 septembre 2016
{: .last-updated}

Vous pouvez utiliser une chaîne d'outils pour améliorer la productivité de votre travail quotidien de développement, de déploiement et de vos opérations. Après avoir configuré une chaîne d'outils, vous pouvez ajouter, supprimer ou configurer des intégrations d'outils et gérer l'accès à la chaîne d'outils.
{: shortdesc}

## Configuration d'une intégration d'outil
{: #configuring_a_tool_integration_dedicated}

Si vous avez différé la configuration d'une intégration d'outil lors de la création d'une chaîne d'outils, un bouton **Configurer** s'affiche sur sa vignette. Si vous avez configuré une intégration d'outil à la création d'une chaîne d'outils, vous pouvez mettre à jour les paramètres de configuration.

1. Dans le tableau de bord, onglet **DEVOPS**, cliquez sur la chaîne d'outils pour ouvrir la page d'intégration d'outil correspondante. Vous pouvez également, dans le coin supérieur droit de la page de présentation de l'application, cliquer sur **Afficher la chaîne d'outils**. Cliquez ensuite sur **Intégrations d'outils**.
1. Si vous devez configurer une intégration d'outil pour la première fois, depuis sa vignette, cliquez sur **Configurer**.

  ![Bouton Configurer](images/toolchain_tile_configure.png)

 Lorsque vous avez terminé la configuration de l'intégration d'outil, cliquez sur **Sauvegarder l'intégration**.
 
1. Si vous devez mettre à jour la configuration d'une intégration d'outil, depuis sa vignette, cliquez sur le menu pour accéder aux options de configuration.

  ![Menu Configuration](images/toolchain_tile_menu.png)
 
 Lorsque vous avez terminé la mis à jour des paramètres, cliquez sur **Sauvegarder l'intégration**.

## Ajout d'une intégration d'outil
{: #adding_a_tool_integration_dedicated}

Vous pouvez ajouter et configurer des intégrations d'outils pour votre chaîne d'outils.

1. Dans le tableau de bord, onglet **DEVOPS**, cliquez sur la chaîne d'outils pour ouvrir la page d'intégration d'outil correspondante. Vous pouvez également, dans le coin supérieur droit de la page de présentation de l'application, cliquer sur **Afficher la chaîne d'outils**. Cliquez ensuite sur **Intégrations d'outils**.
1. Pour afficher la liste des intégrations d'outils à ajouter, cliquez sur le bouton d'ajout (+).
1. Cliquez sur l'intégration d'outil à ajouter.
1. Entrez les informations requises pour configurer l'intégration d'outil. 
1. Cliquez sur **Créer une intégration** pour ajouter l'intégration d'outil à votre chaîne d'outils.

## Suppression d'une intégration d'outil
{: #deleting_a_tool_integration}

Si vous supprimez une intégration d'outil de votre chaîne d'outils, la suppression est irréversible. 

1. Dans le tableau de bord, onglet **DEVOPS**, cliquez sur la chaîne d'outils pour ouvrir la page d'intégration d'outil correspondante. Vous pouvez également, dans le coin supérieur droit de la page de présentation de l'application, cliquer sur **Afficher la chaîne d'outils**. Cliquez ensuite sur **Intégrations d'outils**.
1. Sur la vignette de l'intégration d'outil à supprimer, cliquez sur le menu pour accéder aux options de configuration.
1. Pour supprimer l'intégration d'outil de votre chaîne d'outils, cliquez sur **Supprimer**.
1. Confirmez en cliquant sur **Supprimer**. 

## Gestion des accès
{: #managing_access_dedicated}

Vous pouvez accorder l'accès à une chaîne d'outils à des utilisateurs en les ajoutant à l'organisation (org) à laquelle la chaîne d'outils est associée. Chaque chaîne d'outils est associée à une organisation spécifique, et tout membre de cette organisation peut accéder aux chaînes d'outils associées. Pour afficher l'organisation que vous utilisez actuellement, cliquez sur l'icône **{{site.data.keyword.avatar}}** ![Icône Avatar](../icons/i-avatar-icon.svg) dans la barre de menus. Pour accéder à un ensemble différent de chaînes d'outils, changez d'organisation.

Lorsque vous ajoutez des utilisateurs à votre organisation et vos espaces {{site.data.keyword.Bluemix}}, ces utilisateurs peuvent se connecter à GitHub Enterprise à l'aide de leurs ID et mot de passe {{site.data.keyword.Bluemix_notm}}. Lorsque les utilisateurs se connectent, les comptes correspondants sont créés. Lorsque vous ajoutez des utilisateurs à votre organisation et vos espaces {{site.data.keyword.Bluemix_notm}}, ils ne sont pas automatiquement ajoutés au référentiel GitHub Enterprise. Une personne dotée de privilèges d'administrateur pour le référentiel doit les ajouter. Pour plus d'informations, voir [Utilisation de Dedicated GitHub Enterprise (Lien s'ouvrant dans une nouvelle fenêtre)](../services/ghededicated/index.html){: new_window}.

Pour ajouter un utilisateur, procédez comme suit : 

1. Dans le tableau de bord, onglet **DEVOPS**, cliquez sur la chaîne d'outils pour ouvrir la page d'intégration d'outil correspondante. Cliquez ensuite sur **Gérer**. Vous pouvez également, dans le coin supérieur droit de la page de présentation de l'application, cliquer sur **Afficher la chaîne d'outils**. Cliquez ensuite sur **Gérer**.  
1. Cliquez sur le lien de votre organisation. 
1. Dans la page de gestion des organisations, cliquez sur **Inviter un utilisateur** et entrez l'adresse électronique de l'utilisateur.
1. Si vous souhaitez donner des droits avancés à des responsables {{site.data.keyword.Bluemix_notm}} d'organisations, sélectionnez une ou plusieurs des cases à cocher **Responsable**, **Responsable de la facturation** et **Auditeur**.
1. Cliquez sur **INVITER**.
1. Cliquez sur **SAUVEGARDER**.

## Suppression d'une chaîne d'outils
{: #deleting_a_toolchain_dedicated}

Vous pouvez supprimer une chaîne d'outils et spécifier les intégrations d'outils associées à supprimer. Lorsque vous supprimez une chaîne d'outils, la suppression est irréversible.

1. Dans le tableau de bord, onglet **DEVOPS**, cliquez sur la chaîne d'outils pour ouvrir la page d'intégration d'outil correspondante. Cliquez ensuite sur **Gérer**. Vous pouvez également, dans le coin supérieur droit de la page de présentation de l'application, cliquer sur **Afficher la chaîne d'outils**. Cliquez ensuite sur **Gérer**.
1. Cliquez sur **Supprimer la chaîne d'outils**, examinez et modifiez éventuellement la liste des intégrations d'outils à supprimer.
1. Confirmez la suppression en entrant le nom de la chaîne d'outils et en cliquant sur **Supprimer**.

 **Conseil** : Lorsque vous supprimez une intégration d'outil GitHub Enterprise, le référentiel GitHub Enterprise associé n'est pas supprimé de GitHub Enterprise. Vous devez supprimer manuellement le référentiel depuis GitHub Enterprise.
