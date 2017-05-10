---

copyright:
  years: 2015, 2017
lastupdated: "2016-10-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Gestion des traductions
{: #globalizationpipeline_managingtranslations}

Une fois que vous avez créé des bundles et commencé à générer des traductions pour votre application, le contenu généré automatiquement peut être utilisé tel quel ou être modifié. Vous pouvez également utiliser une traduction automatique autre que celle par défaut. Cette section explique comment modifier le moteur de traduction automatique qui effectue les traductions pour vos bundles, comment effectuer des tâches d'édition humaine après traduction et comment affecter des rôles utilisateur et des restrictions d'accès aux personnes qui auront besoin d'accéder à vos traductions.
{:shortdesc}

## Configuration de la traduction automatique
{: #globalizationpipeline_service_to_service}

{{site.data.keyword.GlobalizationPipeline_full}} prend en charge la possibilité d'intégrer d'autres services de traduction automatique afin d'effectuer la traduction automatique pour vos bundles. Il est pratique de pouvoir ajouter un autre service si le moteur utilisé par défaut par {{site.data.keyword.GlobalizationPipeline_short}} ne propose pas une langue dont vous avez besoin ou si vous préférez les traductions automatiques qui sont générées par un autre moteur. L'utilisation et les frais relatifs aux autres services sont traités dans la section sur les conditions d'utilisation de ces services.

Pour ajouter et configurer un autre service de traduction automatique pour {{site.data.keyword.GlobalizationPipeline_short}}, sélectionnez l'onglet **Machine Translation Configuration** du tableau de bord {{site.data.keyword.GlobalizationPipeline_short}}.

* Pour pouvoir ajouter un service de traduction automatique figurant dans le catalogue {{site.data.keyword.Bluemix_notm}} (**Watson Language Translator**), vous devez d'abord l'ajouter à votre espace {{site.data.keyword.Bluemix_notm}}.

* Pour ajouter un service tiers, sélectionnez le bouton correspondant à ce service sur l'onglet **Machine Translation Configuration** et indiquez les données d'identification de l'utilisateur requises pour accéder au service.

Après avoir ajouté un service de traduction automatique à {{site.data.keyword.GlobalizationPipeline_short}}, exécutez les étapes restantes pour finaliser l'intégration de ce service.

1. Cliquez sur **Enable** pour activer l'intégration à ce service.

2. Cliquez sur **Update Languages** pour visualiser la liste mise à jour des langues cible prises en charge.

3. Dans la liste des langues cible, sélectionnez le moteur de traduction automatique qui doit effectuer la traduction.

4. Cliquez sur **Save** pour revenir à l'onglet **Machine Translation Configuration**.

Une fois qu'un autre service a été configuré avec {{site.data.keyword.GlobalizationPipeline_short}}, toutes les langues cible qui ont été affectées à ce moteur commencent à être générées à l'aide de ce moteur. 

Pour cesser d'utiliser un autre moteur de traduction automatique :

1. Sur l'onglet **Machine Translation Configuration**, cliquez sur le bouton **Disable** pour le service que vous souhaitez cesser d'utiliser.

Une fois qu'un autre service de traduction est désactivé, toutes les traductions qu'il a générées sont conservées dans vos bundles. En revanche, il se peut que la traduction dans une langue cible donnée ne soit pas disponible pour des mises à jour ultérieures si cette langue cible n'est plus prise en charge par le moteur de traduction automatique qui est actuellement activé.

<!-- Review comment: When you disable an engine, do you need to go back and reconfigure the languages?? Does it go back to the default engine? What happens? -->

## Affichage et édition de traductions
{: #globalizationpipeline_translations}

Le service {{site.data.keyword.GlobalizationPipeline_short}} offre des fonctions d'édition humaine après traduction. Un traducteur professionnel ou quelqu'un ayant une bonne connaissance des langues cible peut éditer les traductions générées. L'édition permet d'améliorer la qualité ou la cohérence de la traduction ou d'effectuer des changements terminologiques. Par exemple, vous souhaiterez peut-être remplacer la traduction d'un nom de produit.

Pour afficher et éditer les traductions pour une langue cible :

1. Sur la page **Bundle details**, sélectionnez une langue cible ou cliquez sur l'icône d'**affichage des traductions**![. Sélectionnez l'icône d'affichage des traductions pour afficher les traductions d'une langue cible](images/viewProjectDetailIcon.png) dans la colonne Actions.
2. Les traductions sont présentées dans un tableau qui contient les informations de clé, de source et de traduction.
 * **Key :** Représente un attribut dans le fichier de ressources auquel une valeur est associée.
 * **Source :** Représente une chaîne susceptible d'être traduite qui a été incluse dans le fichier de ressources téléchargé.
 * **Translation :** Représente la version traduite d'une valeur source.
3. Dans la colonne Actions, cliquez sur l'icône de **modification de la traduction** ![. Sélectionnez l'icône de modification de la traduction pour éditer les traductions d'une paire clé/valeur donnée](images/editIcon.png) pour éditer une valeur traduite automatiquement.
4. Editez la traduction et cliquez sur **Update** pour mettre à jour la valeur traduite initialement avec votre modification.

![La boîte de dialogue de modification des traductions permet d'éditer facilement les traductions.](images/editTranslation.png) 

***Astuce :*** Lorsque vous gérez des bundles de grande taille comportant un grand nombre de clés susceptibles d'être traduites, il peut s'avérer difficile de trouver une valeur spécifique. Sur la page de traduction de langue cible, vous pouvez utiliser la zone **Search for...** pour effectuer une recherche rapide portant sur toutes les clés, toutes les données source et toutes les traductions.

![Utilisez la zone de recherche fournie sur la page de traduction de langue cible pour effectuer une recherche dans les clés, les données source, les traductions ou dans les trois à la fois pour une langue cible. ](images/search.png) 


## Ajout d'utilisateur d'API
{: #globalizationpipeline_users}

A mesure que vous gérez vos traductions, vous souhaiterez peut-être octroyer un accès à d'autres utilisateurs d'API en fonction des tâches qu'ils doivent effectuer. Par exemple, vous souhaiterez peut-être permettre à un traducteur d'éditer la traduction, sans l'autoriser à modifier les informations de bundle.

| Type de rôle | Afficher les traductions ? | Editer les traductions ? | Modifier les informations de bundle ? |
|-----------|--------------------|--------------------|----------------------------|
| Lecteur | Oui | Non | Non |
| Traducteur | Oui | Oui | Non |
| Administrateur | Oui | Oui | Oui |

Si vous créez d'autres utilisateurs d'API, vous pouvez limiter leur accès à un ou plusieurs bundles donnés ou leur accorder un accès à tous les bundles disponibles.

Pour autoriser un utilisateur d'API à accéder aux bundles d'une instance de service {{site.data.keyword.GlobalizationPipeline_short}} :

1. Sur le tableau de bord {{site.data.keyword.GlobalizationPipeline_short}}, cliquez sur l'onglet **API Users**.
2. Cliquez sur **New API User**.
3. Saisissez un **nom d'affichage** et un **commentaire** pour décrire le nouvel utilisateur d'API.
4. Choisissez un **type** pour le nouvel utilisateur d'API.
5. Choisissez d'accorder un accès utilisateur à tous les bundles ou à certains bundles uniquement.
6. Cliquez sur **Save**.

![Prenez part au forum afin de créer un nouvel utilisateur d'API.](images/newUser.png)

Un ID et un mot de passe pour l'utilisateur d'API sont générés et affichés. Copiez et sauvegardez ces données d'identification, car agrès avoir fermé la fenêtre, vous n'aurez plus accès à ces informations. les données d'identification peuvent être utilisées pour le service RESTful via des [SDK](https://github.com/IBM-Bluemix/gp-common). 

Pour réinitialiser le mot de passe de l'utilisateur d'API :

1. Sur le tableau de bord {{site.data.keyword.GlobalizationPipeline_short}}, cliquez sur l'onglet **API Users**.
2. Cliquez sur l'icône **Reset Password** ![Sélectionnez cette icône pour réinitialiser le mot de passe de l'utilisateur d'API](images/resetPW.png) pour réinitialiser un mot de passe pour un ID utilisateur spécifique. 
3. Cliquez sur **Yes**. 
