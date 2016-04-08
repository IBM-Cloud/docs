---

Copyright :
  Années : 2015, 2016

---

{:shortdesc: .shortdesc}

# Gestion des utilisateurs{: #manage-users}

Conçu pour la collaboration des équipes, {{site.data.keyword.iotrtinsights_short}} permet aux administrateurs d'ajouter des utilisateurs pour l'accès à la console {{site.data.keyword.iotrtinsights_short}}.
{: shortdesc}

Description des rôles :
- Opérateur
Les opérateurs se connectent directement à la console {{site.data.keyword.iotrtinsights_short}} pour surveiller le flux de données en temps réel de leurs périphériques et des groupes de périphériques. Ils peuvent également activer et désactiver des règles et modifier des tableaux de bords modifiables.   
- Administrateur
Outre les tâches qu'un opérateur est autorisé à exécuter, les administrateurs peuvent ajouter des utilisateurs, gérer des présentations de tableau de bord, ajouter des sources de données et gérer des types de périphérique.   
- Propriétaire
Le rôle de propriétaire est affecté à l'ID IBM qui a déployé l'instance de service {{site.data.keyword.iotrtinsights_short}} dans Bluemix. Un propriétaire possède les mêmes privilèges qu'un administrateur, mais il ne peut pas être supprimé. 

Pour ajouter un utilisateur :
1. Ajoutez l'utilisateur à {{site.data.keyword.iot_short}}.  
>**Important :** Si vous ajoutez un utilisateur doté du rôle d'administrateur, vous devez également l'ajouter à {{site.data.keyword.iot_short}}.  

  1. Connectez-vous au tableau de bord du service {{site.data.keyword.iot_short}} qui est une source de données de votre service {{site.data.keyword.iotrtinsights_short}}.   
  2. Naviguez jusqu'à **Accès > Membres** et cliquez sur **Ajouter des membres**.
  3. Entrez l'ID IBM pour l'utilisateur que vous souhaitez ajouter et cliquez sur **Ajouter des membres**.
2. Ajoutez l'utilisateur à {{site.data.keyword.iotrtinsights_short}}.
  1. Connectez-vous à la console {{site.data.keyword.iotrtinsights_short}} en tant qu'utilisateur doté du rôle d'administrateur ou du rôle de propriétaire. 
  2. Accédez à **Configurer > Gérer des utilisateurs**.
  3. Cliquez sur **Ajouter un utilisateur**.
  4. Entrez l'adresse électronique de l'utilisateur que vous souhaitez inviter, sélectionnez un rôle pour l'utilisateur et cliquez sur l'![icône Créer.](images/create.png "icône Créer").
Un courrier électronique contenant le lien de la console Web est envoyé à l'utilisateur. Si l'adresse électronique est déjà associée à un ID IBM, l'utilisateur peut se connecter et accéder à la console directement. Si tel n'est pas le cas, l'utilisateur est invité à créer gratuitement un ID IBM avant d'accéder à la console.  
>**Sélection de votre instance Real-Time Insights :** Les utilisateurs ayant accès à plusieurs instances Real-Time Insights, tels que des opérateurs ou des administrateurs, peuvent passer rapidement d'une instance à l'autre. Dans la console Real-Time Insights, ils peuvent cliquer sur leur nom d'utilisateur et sélectionner l'instance à laquelle ils souhaitent accéder.   
