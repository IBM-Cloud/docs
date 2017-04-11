---

copyright:
  years: 2016, 2017
lastupdated: "2016-11-10"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# À propos des rôles personnalisés
{: #custom_roles}

Outre les rôles prédéfinis qui sont détaillés dans la [documentation sur les rôles d'utilisateur, d'application et de passerelle](roles_index.html), les utilisateurs peuvent créer des rôles personnalisés avec des combinaisons d'autorisations uniques. Les rôles représentent l'accès à des opérations spécifiques et, en créant un rôle personnalisé, vous pouvez combiner toutes les autorisations qui sont disponibles pour les rôles prédéfinis.
{:shortdesc}

Pour plus d'informations sur les opérations de l'API disponibles pour les rôles d'utilisateur, consultez la [documentation sur les rôles d'utilisateur, d'application et de passerelle](roles_index.html).

## Création d'un rôle personnalisé
{: #custom-role-create}

Pour créer un rôle personnalisé :

1. Dans le tableau de bord {{site.data.keyword.iot_short_notm}}, ouvrez le volet **Membres** dans la barre de navigation.
2. Sélectionnez l'onglet **Rôles** et cliquez sur **Nouveau rôle**.
3. Entrez un nom pour votre rôle personnalisé.
4. Facultatif : saisissez une description de votre rôle personnalisé.
5. Facultatif : les rôles personnalisés peuvent utiliser un rôle existant en tant que modèle. Pour baser le rôle personnalisé sur un rôle utilisateur existant, sélectionnez le rôle dans la liste.
6. Cliquez sur **Suivant**.
7. Dans la liste des droits, développez les catégories de droits et sélectionnez les opérations que le rôle personnalisé doit inclure.
8. Cliquez sur **Ajouter un rôle**.

Le rôle personnalisé est inclus dans la liste des rôles disponibles.

## Edition ou suppression d'un rôle personnalisé
{: #custom-role-edit}

Pour éditer ou supprimer un rôle personnalisé :

1. Dans le tableau de bord {{site.data.keyword.iot_short_notm}}, ouvrez le volet **Membres** dans la barre de navigation.
2. Sélectionnez l'onglet **Rôles**.
3. Localisez la colonne correspondant au rôle personnalisé que vous voulez éditer.
3. Cliquez sur l'icône d'édition correspondant au nom de rôle personnalisé.
4. Effectuez les modifications nécessaires de la description du rôle et des droits.
5. Pour supprimer le rôle, faites défiler jusqu'au bas de la liste des catégories de droits, puis cliquez sur **Supprimer le rôle**.
5. Si vous avez apporté des modifications, cliquez sur **Sauvegarder** pour mettre à jour le rôle.

Le rôle est mis à jour.
