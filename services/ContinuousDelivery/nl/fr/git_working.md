---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-11"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:screen:.screen}
{:codeblock:.codeblock}

# Utilisation de Git Repos and Issue Tracking (expérimental)
{: #git_working}

Collaborez avec votre équipe et gérez votre code source avec un référentiel Git et le dispositif de suivi des problèmes qui est hébergé par IBM et basé sur [GitLab Community Edition ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://about.gitlab.com/){:new_window}.
{: shortdesc}

L'intégration de l'outil Git Repos and Issue Tracking aide les équipes à gérer le code et à collaborer de diverses manières : 
   * Gestion de référentiels Git via des contrôles d'accès à granularité fine qui permettent de sécuriser le code
   * Révision du code et amélioration de la collaboration via des demandes de fusion
   * Suivi des problèmes et partage d'idées via le dispositif de suivi de problème
   * Documentation de projets sur le système wiki

**Remarque :** Cette intégration d'outils étant basée sur GitLab Community Edition et hébergée par IBM sur Bluemix, certaines options GitLab ne sont pas disponibles. Par exemple, Delivery Pipeline fournit une intégration et une distribution continues pour Bluemix ; par conséquent, les fonctions d'intégration continue dans GitLab ne sont pas prises en charge. En outre, les fonctions d'administration ne sont pas disponibles car elles sont gérées par IBM. 

## Limites de taille de fichier et de référentiel
{: #git_limits}

La taille des fichiers est strictement limitée à 100 Mo. La limite de taille suggérée pour les référentiels est 1 Go. Si votre référentiel dépasse 1 Go, vous risquez de recevoir un courrier électronique vous demandant de réduire sa taille. 

## Création d'un jeton d'accès personnel ou d'une clé SSH pour l'authentification    
{: #git_authentication}

Pour effectuer des opérations Git distantes, telles que `clone` ou `push`, à partir de votre référentiel Git local, vous devez utiliser un jeton d'accès personnel ou une clé SSH pour vous authentifier auprès de GitLab.

* Pour configurer un jeton d'accès personnel, voir [Jetons d'accès personnels ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://git.ng.bluemix.net/help/api/README.html#personal-access-tokens){:new_window}.
* Pour configurer une clé SSH, voir [SSH ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://git.ng.bluemix.net/help/ssh/README){:new_window} ou [Création de clés SSH ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://git.ng.bluemix.net/help/gitlab-basics/create-your-ssh-keys){:new_window}. L'accès à vos référentiels à l'aide d'une authentification SSH peut nécessiter une configuration supplémentaire pour les proxy et les pare-feux. 

**Remarque :** Pour utiliser un jeton d'accès personnel ou une clé SSH pour l'authentification, vous devez configurer Git localement. Pour obtenir des instructions, voir [Initiation à l'utilisation de Git sur la ligne de commande ![Icône de lien externe](../../icons/launch-glyph.svg "External link icon")](https://git.ng.bluemix.net/help/gitlab-basics/start-using-git){:new_window}.
