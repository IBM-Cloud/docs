---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Utilisation de chaîne d'outils
{: #toolchains-using}

*Dernière mise à jour : 4 mai 2016*
{: .last-updated}

Vous pouvez utiliser une chaîne d'outils pour améliorer la productivité de votre travail quotidien de développement, de déploiement et de vos opérations. Après avoir configuré une chaîne d'outils, vous pouvez ajouter, supprimer ou configurer des intégrations d'outils et gérer l'accès à la chaîne d'outils.
{: shortdesc}

**Important **: Cette fonction est expérimentale. Les chaînes d'outils peuvent être instables et faire l'objet de modifications entraînant leur incompatibilité avec des versions antérieures. Elles ne sont pas recommandées pour une utilisation dans des environnements de production. Pour utiliser des chaînes d'outils, vous devez adresser une [demande d'accès](https://new-console.ng.bluemix.net/devops?cm_mmc=IBMBluemixGarageMethod-_-MethodSite-_-10-19-15::12-31-18-_-toolchains-welcome-page){: new_window} à usage unique.  Les chaînes d'outils sont disponibles uniquement dans la région sud des Etats-Unis. 

## Configuration d'une intégration d'outil
{: #configuring_a_tool_integration}

Vous pouvez configurer une intégration d'outil initiale ou mettre à jour les paramètres de configuration d'une intégration d'outil faisant déjà partie de votre chaîne d'outils. 

1. Dans le tableau de bord DevOps, onglet **Chaînes d'outils**, cliquez sur une chaîne d'outils pour ouvrir la page d'intégration d'outil correspondante. Vous pouvez également, depuis la page de présentation de l'application, vignette de distribution continue, cliquer sur **Afficher la chaîne d'outils** puis sur **Intégrations d'outils**.
1. Si vous devez configurer une intégration d'outil pour la première fois, depuis sa vignette, cliquez sur **Configurer**.

  ![Bouton Configurer](images/toolchain_tile_configure.png)

 Lorsque vous avez terminé la configuration de l'intégration d'outil, cliquez sur **Sauvegarder l'intégration**.
 
1. Si vous devez mettre à jour la configuration d'une intégration d'outil, depuis sa vignette, cliquez sur le menu pour accéder aux options de configuration.

  ![Menu Configuration](images/toolchain_tile_menu.png)
 
 Lorsque vous avez terminé la mis à jour des paramètres, cliquez sur **Sauvegarder l'intégration**.

 **Remarque **: Une fois que vous avez configuré le référentiel d'une intégration d'outil GitHub, l'URL du référentiel peut être mise à jour mais le référentiel ne peut plus être changé. Pour utiliser un référentiel différent, supprimez de votre chaîne d'outils l'intégration d'outil GitHub en cours, ajoutez une intégration d'outil GitHub à votre chaîne d'outils, puis configurez-la pour utiliser le nouveau référentiel.

## Ajout d'une intégration d'outil
{: #adding_a_tool_integration}

Vous pouvez ajouter et configurer des intégrations d'outils pour votre chaîne d'outils. 

1. Dans le tableau de bord DevOps, onglet **Chaînes d'outils**, cliquez sur une chaîne d'outils pour ouvrir la page d'intégration d'outil correspondante. Vous pouvez également, depuis la page de présentation de l'application, vignette de distribution continue, cliquer sur **Afficher la chaîne d'outils** puis sur **Intégrations d'outils**.
1. Pour afficher la liste des intégrations d'outils à ajouter, cliquez sur le bouton d'ajout (+).
1. Cliquez sur une intégration d'outil à ajouter.
1. Entrez les informations requises pour configurer l'intégration d'outil. 
1. Cliquez sur **Créer une intégration** pour ajouter l'intégration d'outil à votre chaîne d'outils.

## Suppression d'une intégration d'outil
{: #deleting_a_tool_integration}

Vous pouvez supprimer une intégration d'outil de votre chaîne d'outils. 

1. Dans le tableau de bord DevOps, onglet **Chaînes d'outils**, cliquez sur une chaîne d'outils pour ouvrir la page d'intégration d'outil correspondante. Vous pouvez également, depuis la page de présentation de l'application, vignette de distribution continue, cliquer sur **Afficher la chaîne d'outils** puis sur **Intégrations d'outils**.
1. Sur la vignette de l'intégration d'outil à supprimer, cliquez sur le menu pour accéder aux options de configuration. 
1. Pour supprimer l'intégration d'outil de votre chaîne d'outils, cliquez sur **Supprimer**.
1. Confirmez en cliquant sur **Supprimer**.

## Gestion des accès
{: #managing_access}

Vous pouvez accorder l'accès à une chaîne d'outils à des utilisateurs en les ajoutant à l'organisation (org) à laquelle la chaîne d'outils est associée. Chaque chaîne d'outils est associée à une organisation spécifique, et tout membre de cette organisation peut accéder aux chaînes d'outils associées. Si vous changez d'organisation, vous pouvez accéder à un ensemble différent de chaînes d'outils.

<!--CA: Commenting out the content on authentication for Interconnect since it applies to GitHub Enterprise. This content can be exposed again when GHE is supported for the Dedicated Beta 2.-->

<!--You have three authentication options for your Bluemix dedicated environment: LDAP, SAML, or Web ID. 

**Important:** For this beta, Web ID authentication requires additional user management on GitHub Enterprise.

If you use LDAP or SAML authentication in your Bluemix dedicated environment, when you add users to your Bluemix org and spaces, the users can log in to GitHub Enterprise by using their Bluemix ID and password, and accounts are created for them. When you add users to your Bluemix org and spaces, they are not automatically added to the GitHub Enterprise repo. Someone who has admin privileges for the repo must add them.  

If you use Web ID authentication, when you add users to your Bluemix org and spaces, a GitHub Enterprise site administrator must set up a GitHub Enterprise account for those users. Alternatively, new users can create a toolchain, in which case a GitHub Enterprise account is created for them. However, if those users want to access repos that are associated with toolchains besides their own, they must be granted access to those repos.

To add a user: -->

1. Dans l'onglet DevOps, onglet **Chaînes d'outils**, cliquez sur la chaîne d'outils à gérer puis cliquez sur **Gérer**. Vous pouvez également, depuis la page de présentation de l'application, vignette de distribution continue, cliquer sur **Afficher la chaîne d'outils** puis sur **Gérer**.  
1. Cliquez sur le lien de votre organisation.  
1. Dans la page de gestion des organisations, cliquez sur **Inviter un utilisateur** et entrez l'adresse électronique de l'utilisateur. 
1. Si vous souhaitez donner des droits avancés à l'utilisateur, sélectionnez une ou plusieurs des cases à cocher **Responsable**, **Responsable de la facturation** et **Auditeur**. 
1. Cliquez sur **INVITER**.
1. Cliquez sur **SAUVEGARDER**.

## Suppression d'une chaîne d'outils
{: #deleting_a_toolchain}

Vous pouvez supprimer une chaîne d'outils et spécifier les intégrations d'outils associées à supprimer. 

1. Dans l'onglet DevOps, onglet **Chaînes d'outils**, cliquez sur la chaîne d'outils à supprimer puis cliquez sur **Gérer**. Vous pouvez également, depuis la page de présentation de l'application, vignette de distribution continue, cliquer sur **Afficher la chaîne d'outils** puis sur **Gérer**.
1. Cliquez sur **Supprimer la chaîne d'outils** et passez en revue les intégrations d'outils que vous allez supprimer. 
1. Confirmez la suppression en entrant le nom de la chaîne d'outils et en cliquant sur **Supprimer**.

 **Conseil **: Lorsque vous supprimer une intégration d'outil GitHub, le référentiel GitHub associé n'est pas supprimé de GitHub. Vous devez supprimer manuellement le référentiel depuis GitHub.
