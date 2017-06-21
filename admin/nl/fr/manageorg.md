---

copyright:

  years: 2015, 2017
lastupdated: "2017-04-11"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Gestion des organisations
En tant que propriétaire de compte ou responsable de l'organisation, vous pouvez effectuer des tâches de gestion de l'organisation, notamment renommer votre organisation, supprimer une organisation ou un espace, mettre à jour les rôles d'organisation ou d'espace et gérer le quota et les domaines.
{:shortdesc}

Dans la barre de menu de la console, sélectionnez **Gérer > Compte > Organisations** pour gérer vos organisations.  

**Remarque :** vous pouvez afficher les ressources d'une seule organisation à la fois. Si vous êtes membre de plusieurs organisations, vous pouvez passer d'une organisation à l'autre depuis le lien des préférences du compte utilisateur dans la barre de menu de la console. 

## Modification du nom d'une organisation 
{: #orgrename}

Procédez comme suit pour renommer votre organisation :
1. Cliquez sur **Gérer** > **Compte** > **Organisations**.
2. Identifiez l'organisation à renommer et cliquez sur **Afficher les détails**.
3. Cliquez sur **Editer l'organisation**.
4. Cliquez sur **Editer** à côté du nom de l'organisation. 
5. Entrez le nouveau nom d'organisation et cliquez sur **Sauvegarder**.

## Suppression d'organisations et d'espaces 
{: #deleteorgs}

En tant que propriétaire de compte, prenez contact avec le [support {{site.data.keyword.Bluemix_notm}} ![Icône de lien externe](../icons/launch-glyph.svg)](http://ibm.biz/bluemixsupport){: new_window} pour supprimer une organisation. 

**Remarque** : les opérations de suppression sont irréversibles. Vous perdez toutes vos applis et tous les services qui sont associés à l'organisation.

Procédez comme suit pour supprimer une organisation ou un espace : 
1. Cliquez sur **Gérer** > **Compte** > **Organisations**.
2. Identifiez l'organisation à éditer et cliquez sur **Afficher les détails**.
3. Identifiez l'espace à supprimer et cliquez sur **Editer l'espace**.
4. Cliquez sur **Supprimer l'espace**.

## Edition des rôles utilisateur 
{: #listmembers}

Procédez comme suit afin d'éditer les rôles utilisateur pour une organisation spécifique :
1. Cliquez sur **Gérer** &gt; **Compte** &gt; **Organisations**.
2. Identifiez l'organisation dont vous voulez afficher les membres, puis cliquez sur **Afficher les détails**.
3. Cliquez sur **Editer l'organisation**.
4. Les membres de votre organisation et leurs rôles s'affichent dans l'onglet **UTILISATEURS**.

Procédez comme suit afin d'éditer les rôles utilisateur pour un espace spécifique : 
1. Cliquez sur **Gérer** &gt; **Compte** &gt; **Organisations**.
2. Identifiez l'organisation dont vous voulez afficher les membres, puis cliquez sur **Afficher les détails**.
3. Identifiez l'espace dont vous voulez afficher les membres, puis cliquez sur **Editer l'espace**.
4. Les membres de votre espace et leurs rôles s'affichent dans l'onglet **UTILISATEURS**.

## Gestion du quota
{: #managequota}

En tant que propriétaire de compte {{site.data.keyword.Bluemix_notm}} ou responsable de l'organisation, vous pouvez afficher le quota alloué et le quota utilisé pour une organisation. Le quota représente les limites de ressources pour l'organisation et est affecté lorsque l'organisation est créée. Selon que vous disposez d'un compte d'essai ou d'un compte facturable, les ressources disponibles pour une organisation varient. Toute application ou tout service dans un espace de l'organisation contribue à l'utilisation du quota alloué.

Procédez comme suit afin d'afficher le quota utilisé et le quota alloué pour une organisation :
1. Cliquez sur **Gérer** &gt; **Compte** &gt; **Organisations**.
2. Identifiez l'organisation pour laquelle afficher le quota, puis cliquez sur **Afficher les détails**.
3. Cliquez sur **Editer l'organisation**.
4. Si des espaces sont définis dans plusieurs régions, sélectionnez la région que vous souhaitez visualiser.
5. Cliquez sur **QUOTA**. 
6. Par défaut, la page du quota **Cloud Foundry** s'ouvre. Vous pouvez afficher les détails de quota des ressources suivantes :
 * MEMOIRE
 * Services
 * PLAN
 * PRIX
7. Cliquez sur **Conteneurs** pour afficher l'allocation des quotas de conteneur utilisé et disponible. L'allocation de conteneur varie en fonction du plan de tarification. Vous pouvez afficher les détails de quota des ressources suivantes :
 * MEMOIRE
 * Adresse IP publique
 * PARTAGE DE FICHIERS
8. Cliquez sur **Serveurs virtuels** pour visualiser les machines virtuelles.

**Remarque :** les conteneurs ne sont pas disponibles dans la région {{site.data.keyword.Bluemix_notm}} Sydney. 

Pour plus d'informations sur les conteneurs, voir [Quota](/docs/containers/container_planning.html#container_planning_quota) dans la documentation sur les conteneurs.
Pour modifier le quota alloué à une organisation, vous devez ouvrir un ticket de demande de service. Pour plus d'informations sur l'ouverture d'un ticket de demande de service, voir [Support client](/docs/support/index.html#contacting-support). 

## Gestion des domaines
{: #managedomains}

En tant que propriétaire de compte ou responsable de l'organisation, vous pouvez afficher le domaine de système et ajouter des données personnalisés pour les applications construites dans une organisation et ses espaces. Si vous êtes responsable de l'espace, l'onglet **Domaines** d'un espace est une liste en lecture seule des domaines affectés à l'espace.

1. Cliquez sur **Gérer** &gt; **Compte** &gt; **Organisations**.
2. Identifiez l'organisation que vous désirez éditer ou éditer les domaines.
3. Sélectionnez **Afficher les détails** pour cette organisation.
4. Cliquez sur **Editer l'organisation**.
5. Cliquez sur **DOMAINES**.

Si vous ajoutez un domaine personnalisé, vous devez configurer votre serveur DNS pour qu'il résolve votre domaine personnalisé, de telle sorte qu'il désigne le domaine de système {{site.data.keyword.Bluemix_notm}}. Ainsi, lorsque {{site.data.keyword.Bluemix_notm}} reçoit une demande pour votre domaine personnalisé, il peut l'acheminer correctement vers votre appli. Le domaine de système est toujours disponible dans un espace, et des domaines personnalisés peuvent également être alloués à un espace. Les applis créées dans un espace peuvent utiliser tout domaine répertorié pour cet espace. Pour plus d'informations sur la création et l'utilisation de domaines personnalisés, voir [Création et utilisation d'un domaine personnalisé](/docs/manageapps/updapps.html#domain).
