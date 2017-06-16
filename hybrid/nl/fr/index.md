---


copyright:
  years: 2015, 2017
lastupdated: "2017-04-18"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Gestion de l'environnement {{site.data.keyword.Bluemix_notm}} local et de l'environnement {{site.data.keyword.Bluemix_notm}} dédié
{: #mng}

Si vous disposez d'un accès administrateur pour l'environnement {{site.data.keyword.Bluemix}} local ou {{site.data.keyword.Bluemix_notm}} dédié, accédez à la page **Administration** pour gérer les ressources, surveiller l'utilisation des quotas, administrer des droits d'utilisateur, planifier des notifications de mise à niveau, afficher des rapports de sécurité et des journaux, etc. Vous pouvez gérer votre organisation en créant des espaces et en configurant des [rôles utilisateur et autorisations](/docs/admin/index.html#oc_useradmin). Voir [Gestion de vos organisations](/docs/admin/orgs_spaces.html).
{:shortdesc}

{: #ld_table1}

| Que puis-je faire ? | Détails |    
|----------------|---------|
|Surveiller l'utilisation du système | Cliquez sur **ADMINISTRATION &gt; UTILISATION**. Affichez vos informations système, surveillez l'utilisation de l'unité centrale et planifiez l'utilisation afin de prendre les meilleures décisions pour votre entreprise. Voir [Affichage des informations relatives à l'utilisation](/docs/admin/index.html#oc_resource).|
|Gérer votre catalogue | Cliquez sur **ADMINISTRATION &gt; GESTION DES CATALOGUES** afin de gérer les services que vos utilisateurs et organisations peuvent voir. Voir [Gestion de votre catalogue](/docs/admin/index.html#oc_catalog).|
|Administrer des organisations | Cliquez sur **ADMINISTRATION &gt; ADMINISTRATION DES ORGANISATIONS** afin de créer des organisations, surveiller les quotas pour les organisations et prendre des décisions rapidement en fonction des besoins. Voir [Administration des organisations](/docs/admin/index.html#oc_organizations).|
|Créer des espaces et affecter des rôles utilisateur | Cliquez sur **Compte** &gt; **Gérer les organisations** afin de créer des espaces dans vos organisations. Ajoutez des utilisateurs et affectez des organisations et des espaces aux utilisateurs. Voir [Gestion de vos organisations](/docs/admin/orgs_spaces.html). |
|Gérer les droits d'administrateur | Cliquez sur **ADMINISTRATION &gt; ADMINISTRATION DES UTILISATEURS** pour ajouter des utilisateurs, retirer des utilisateurs et ajuster les droits des utilisateurs. Voir [Gestion des utilisateurs et des droits](/docs/admin/index.html#oc_useradmin). |
|Consulter les rapports et les journaux | Cliquez sur **ADMINISTRATION &gt; RAPPORTS ET JOURNAUX** afin d'afficher des rapports de sécurité et des journaux d'audit pour votre instance. Voir [Affichage des rapports](/docs/admin/index.html#oc_report). |
|Afficher les informations système | Cliquez sur **ADMINISTRATION &gt; INFORMATIONS SYSTEME** afin d'afficher des informations système, telles que les mises à jour de maintenance en attente, le nom et la version de votre instance, la région, l'adresse URL de l'API, l'adresse URL de l'interface de ligne de commande, les détails de la configuration LDAP, les mappages des groupes et des utilisateurs, des statistiques et les domaines partagés. Voir [Affichage des informations système](/docs/admin/index.html#oc_system). |
|Etendre des notifications et configurer des abonnements à des notifications | Cliquez sur **ADMINISTRATION &gt; INFORMATIONS SYSTEME &gt; *Nombre* mises à jour en attente**. Vous pouvez utiliser des webhooks pour l'intégration à un service Web de votre choix afin de configurer un abonnement aux notifications d'événement pour une mise à jour ou un incident. Voir [Notifications et abonnements à des notifications](/docs/admin/index.html#oc_eventsubscription). |
{: caption="Tableau 1. Tâches d'administration pour la gestion de votre instance Bluemix locale ou dédiée" caption-side="top"}

<!-- staging only for WoW start -->

**Astuce** : le tableau de bord Infrastructure dans la console {{site.data.keyword.Bluemix_notm}} n'est disponible que dans les comptes liés dans des environnements {{site.data.keyword.Bluemix_notm}} publics.


<!-- staging only for WoW end -->


## Notifications et abonnements à des notifications
{: #oc_eventsubscription}

Vous pouvez prendre connaissance à tout moment du statut de votre environnement en consultant la page Statut. Les incidents et les événements de mise à jour de maintenance planifiés avec interruption sont signalés sur cette page au fur et à mesure qu'ils se produisent. {{site.data.keyword.Bluemix_notm}} envoie également des notifications à la zone Notifications sur la page Administration pour des événements tels que des mises à jour de maintenance planifiées ou en attente.

### Notifications

Vous pouvez afficher les notifications pour votre environnement local ou dédié pour surveiller le statut de votre environnement. Reportez-vous au tableau ci-dessous pour plus d'informations sur les différents types de notification et les emplacements où elles sont publiées.

{: #ld_table2}

| **Type d'événement** | **Méthode de notification** |       
|-----------------|-------------------|
| Mises à jour de maintenance | Pour afficher la liste complète ainsi que l'historique de vos notifications en attente et consultées, cliquez sur **ADMINISTRATION &gt; INFORMATIONS SYSTEME** &gt; *Nombre* **en attente**. Vous êtes également prévenu en cas d'événements de mise à jour de maintenance planifiés avec interruption dans la page Statut. Cliquez sur **Support** &gt; **Statut**. Vous pouvez étendre la capacité de notification en configurant un abonnement envoyant un courrier électronique aux destinataires de votre choix. Vous pouvez également configurer un abonnement utilisant des webhooks pour intégrer les notifications de la page Administration au service Web de votre choix.|
| Incidents critiques | Vous êtes prévenu en cas d'incident critique dans la page Statut. Cliquez sur **Support** &gt; **Statut**. Vous pouvez étendre la capacité de notification en configurant un abonnement aux notifications qui envoie un courrier électronique au destinataire de votre choix. Vous pouvez également configurer un abonnement utilisant des webhooks pour intégrer les notifications de la page Administration au service Web de votre choix.  |  
| Evénements de seuil | Vous pouvez configurer un abonnement de notification qui envoie un courrier électronique au destinataire de votre choix lorsque les seuils pour le quota d'organisation, le disque physique, la mémoire physique, le disque réservé ou la mémoire réservée sont atteints dans votre environnement. Vous pouvez également configurer un abonnement utilisant des webhooks pour intégrer les notifications au service Web de votre choix.  |  
| Statut {{site.data.keyword.Bluemix_notm}} | Vous pouvez toujours examiner le statut le plus récent de la plateforme, des services et de votre instance {{site.data.keyword.Bluemix_notm}} sur la page Statut. Cliquez sur **Support** &gt; **Statut**.  |
{: caption="Tableau 2. Types d'événement et méthodes de notification" caption-side="top"}

### Configuration d'abonnements à des notifications
{: #seteventsub}

Vous pouvez étendre la fonctionnalité des notifications qui sont envoyées à la page Administration et à la page Statut en utilisant des abonnements à des notifications. Utilisez ces derniers pour configurer un courrier électronique personnalisé ou utiliser des webhooks à intégrer à l'outil de votre choix.
 * Si vous sélectionnez l'option de courrier électronique, vos notifications sont envoyées aux adresses électroniques que vous spécifiez. Vous pouvez sélectionner des notifications d'incidents, de mises à jour de maintenance ou de seuils. Une notification par courrier électronique initiale est envoyée. Ensuite, si l'événement est modifié, une autre notification comportant la modification est envoyée à chaque fois qu'une modification est effectuée.  
 * Si vous sélectionnez l'option webhooks, vos notifications sont acheminées directement à la destination de votre choix, par exemple à un numéro de téléphone (via un message SMS). Vous pouvez personnaliser le type de notification, notamment pour les mises à jour de maintenance, les alertes relatives aux incidents critiques ou les seuils. Vous pouvez indiquer si vous voulez recevoir les nouvelles notifications ou les notifications sur les modifications des abonnements, et quelles informations doivent être incluses dans le corps de chaque notification.

**Remarque** : seuls les utilisateurs disposant de l'autorisation de superutilisateur (`ops.admin`) peuvent configurer des abonnements à des notifications.

Pour créer un abonnement par courrier électronique ou webhook depuis la page **Abonnements aux notifications**, procédez comme suit :

1. Accédez à la page **Abonnements aux notifications**.  Sélectionnez **INFORMATIONS SYSTEME &gt; Environnement &gt; Abonnements**.
2. Cliquez sur **Ajouter un abonnement**.
3. Remplissez le formulaire d'abonnement aux notifications.

  * Pour créer des abonnements à des notifications par courrier électronique sur les mises à jour de maintenance ou les incidents, voir les informations du [tableau 3](index.html#emailnotmaintinc).
  * Pour créer des abonnements à des notifications par courrier électronique sur les seuils, voir les informations du [tableau 4](index.html#emailnottrhesh).
  * Pour créer des abonnements à des notifications par webhook sur les mises à jour de maintenance ou les incidents, voir les informations du [tableau 5](index.html#webhooknotsub).
  * Pour créer des abonnements à des notifications par webhook sur les seuils, voir les informations du [tableau 6](index.html#webhooknotthresh).

4. Une fois que vous avez complété ce formulaire, vous pouvez choisir parmi les options suivantes :

  * Cliquez sur **Sauvegarder** pour enregistrer l'abonnement dans votre liste d'abonnements à des notifications.
  * Cliquez sur **Sauvegarder et tester** pour enregistrer et tester la notification.
  * Cliquez sur **Sauvegarder et fermer** pour enregistrer l'abonnement dans votre liste d'abonnements à des notifications et revenir à la page précédente.

{: #emailnotmaintinc}

| **Zone** | **Description** |
|-----------------|-------------------|
| Activé | Sélectionnez l'option d'activation des notifications par courrier électronique. Effacez la sélection pour désactiver la notification par courrier électronique. Les abonnements sont activés par défaut. |
| Type | Sélectionnez **Courrier électronique**. |
| Evénement | Choisissez de vous abonner aux notifications relatives à un événement **Maintenance** ou **Incident**. |
| Combiner des notifications | Sélectionnez l'option permettant de combiner les notifications relatives aux incidents pour toutes les régions dans une seule notification. Cette option est disponible uniquement pour les incidents. |
| Objet | Renseignez la ligne d'objet du courrier électronique. Cette zone est obligatoire.  |
| Corps | Entrez le texte du corps du message à envoyer dans le message électronique. Vous pouvez utiliser les valeurs de contenu IBM pour alimenter la notification par courrier électronique avec les informations pertinentes. Voir le tableau [Valeurs de la section de contenu de maintenance et d'incident](index.html#payload) pour identifier les valeurs que vous pouvez utiliser. Servez-vous des balises HTML élémentaires pour structurer votre courrier électronique. Cette zone est obligatoire. |
| A | Entrez l'adresse ou les adresses électroniques des destinataires de la notification par courrier électronique dans une liste séparée par des virgules. Développez les options "cc" ou "bcc" pour ajouter d'autres destinataires au courrier électronique. Cette zone est obligatoire. |
| Description | Ajoutez une description unique pour l'abonnement que vous créez. |
{: caption="Tableau 3. Zones pour les abonnements à des notifications par courrier électronique sur les seuils" caption-side="top"}


{: #emailnottrhesh}

| **Zone** | **Description** |
|-----------------|-------------------|
| Activé | Sélectionnez l'option d'activation des notifications par courrier électronique. Effacez la sélection pour désactiver la notification par courrier électronique. Les abonnements sont activés par défaut. |
| Type | Sélectionnez **Courrier électronique**. |
| Evénement | Sélectionnez **Seuil**. |
| Seuil | Sélectionnez le type de seuil pour lequel vous voulez recevoir des notifications : quota d'organisation, disque physique, mémoire physique, disque réservé ou mémoire réservée. |
| Direction du seuil | Sélectionnez la direction dans laquelle les données doivent être classées, c'est-à-dire Croissant ou Décroissant, lorsqu'elles dépassent ou passent sous la valeur Notifier lors du dépassement du seuil/lors du passage sous le seuil que vous avez définie. Par exemple, si la valeur Notifier lors du dépassement du seuil/lors du passage sous le seuil est de 50 % et que la direction est décroissante, vous ne recevez de notification que si le pourcentage d'utilisation passe de 50 % ou plus à moins de 50 %. Si vous définissez la direction croissante, vous recevez une notification lorsque le pourcentage d'utilisation passe de moins de 50 % à plus de 50 %.
| Notifier lors du dépassement du seuil (%) | Entrez le seuil en pourcentage à partir duquel vous voulez recevoir une notification. Si vous avez choisi la propriété Croissant dans la zone Direction du seuil, la notification par courrier électronique est envoyée lorsque le seuil dépasse ce pourcentage. |
| Notifier lors du passage sous le seuil (%) | Entrez le seuil en pourcentage à partir duquel vous voulez recevoir une notification. Si vous avez choisi la propriété Décroissant dans la zone Direction du seuil, la notification par courrier électronique est envoyée lorsque le seuil passe sous ce pourcentage. |
| Description | Ajoutez une description unique pour l'abonnement que vous créez. |
| Objet | Renseignez la ligne d'objet du courrier électronique. Cette zone est obligatoire.  |
| Corps du message | Entrez le texte du corps du message à envoyer dans le message électronique. Vous pouvez utiliser les valeurs de contenu IBM pour alimenter la notification par courrier électronique avec les informations pertinentes. Voir le tableau [Valeurs de la section de contenu de seuil](index.html#threshpayload) pour identifier les valeurs que vous pouvez utiliser. Servez-vous des balises HTML élémentaires pour structurer votre courrier électronique. Cette zone est obligatoire. |
| A | Entrez l'adresse ou les adresses électroniques des destinataires de la notification par courrier électronique dans une liste séparée par des virgules. Développez les options "cc" ou "bcc" pour ajouter d'autres destinataires au courrier électronique. Cette zone est obligatoire. |
{: caption="Tableau 4. Zones pour les abonnements à des notifications par courrier électronique sur les mises à jour de maintenance ou les incidents" caption-side="top"}

Les données de seuil sont collectées toutes les six heures. Une notification n'est envoyée qu'une fois lorsque la valeur dépasse ou passe sous la valeur que vous avez définie. Si vous avez choisi la propriété Croissant, aucune nouvelle notification n'est envoyée sauf si la valeur passe sous le seuil, puis dépasse à nouveau le seuil. De même, si vous avez choisi la propriété Décroissant, vous ne recevez une notification que si la valeur dépasse le seuil que vous avez défini, puis passe à nouveau sous le seuil. 

Si vous ne voulez pas attendre six heures avant l'envoi de la notification lorsque le seuil est atteint, après avoir rempli les zones du formulaire, vous pouvez cliquer sur **Sauvegarder et tester** pour recevoir une notification de test avec des exemples de données.  

Une notification de seuil de quota inclut uniquement les organisations qui ont dépassé le pourcentage de seuil spécifié au cours de la période de 6 heures correspondant à cette notification. Les organisations qui ont dépassé un seuil au cours des périodes de 6 heures précédentes ne seront pas incluses, même si elles sont toujours au-dessus ou au-dessous du seuil.  Les  trois ressources qui constituent un quota d'organisation (mémoire réservée, services et routes) sont considérées de manière indépendante lorsqu'il s'agit de déterminer si une notification de quota d'organisation doit être envoyée. Par exemple, si la quantité de mémoire réservée utilisée par une organisation dépasse 50 % du quota de l'organisation, un seuil de quota d'organisation configuré avec une valeur de 50 % provoque l'envoi d'une notification.  Ultérieurement, si le nombre de services utilisés par la même organisation dépasse 50 % du quota de l'organisation, même si la quantité de mémoire utilisée est inchangée, le même abonnement à un seuil de quota d'organisation provoque également l'envoi d'une notification.

{: #webhooknotsub}

| **Zone** | **Description** |
|-----------------|-------------------|
| Activé | Sélectionnez l'option d'activation de la notification. Effacez la sélection pour désactiver la notification. Les abonnements sont activés par défaut. |
| Type | Sélectionnez **Webhook** |
| Evénement | Choisissez de vous abonner aux notifications relatives à un événement **Maintenance** ou **Incident**. |
| Autorisation | Choisissez d'activer ou non l'autorisation.  Les options sont **De base** et **Aucune**. |
| Nom d'utilisateur | Si vous avez choisi l'autorisation **De base**, entrez votre nom d'utilisateur pour votre service Web. Si vous ne voulez pas utiliser vos données d'identification personnelles, vous pouvez configurer un ID fonctionnel à utiliser spécifiquement avec {{site.data.keyword.Bluemix_notm}}. |
| Mot de passe | Si vous avez choisi l'autorisation **De base**, entrez le mot de passe pour votre service Web. |
| Description | Ajoutez une description unique pour l'abonnement que vous créez. |
| Nouvel événement | Sélectionnez cette option afin d'activer la notification pour les nouveaux événements de maintenance ou d'incident. Effacez la sélection pour désactiver la notification. |
| Méthode | Sélectionnez **GET**, **POST** ou **PUT**. |
| URL | Entrez l'URL pour connexion à votre service Web. |
| Propriété de réponse | Cette zone facultative contient le nom de propriété qui identifie la ressource créée par votre service Web lorsqu'une demande POST ou PUT est envoyée. Si vous fournissez une propriété de réponse pour un nouvel événement et choisissez de créer un abonnement pour une modification apportée à un événement, vous devez aussi la fournir pour l'abonnement Modification d'événement. Selon le service Web que vous utilisez, vous pouvez la spécifier dans l'adresse URL ou sous forme de valeur de contenu.  |
| Contenu | Si vous avez sélectionné la méthode POST ou PUT, entrez les propriétés spécifiques au service Web que vous utilisez, appariées aux valeurs de contenu utilisées pour la notification IBM. Voir le tableau [Valeurs de la section de contenu de maintenance et d'incident](index.html#payload) pour identifier les valeurs que vous pouvez utiliser. Si vous n'entrez pas d'informations dans cette section, vous recevrez une notification ne comportant pas d'information supplémentaire. |
| Modification d'événement | Sélectionnez cette option pour créer des abonnements à des notifications sur les modifications apportées aux événements de maintenance ou d'incident pour lesquels vous avez créé des abonnements. Effacez la sélection pour désactiver la notification. |
| Utiliser les valeurs et le contenu du nouvel événement | Utilise le contenu des zones Méthode, URL et Contenu de la section Nouvel événement. Si cette option est sélectionnée, ces zones ne peuvent pas être éditées dans la section Modification d'événement. |
| Méthode | Sélectionnez **GET**, **POST** ou **PUT**. |
| URL | Entrez l'URL pour connexion à votre service Web. |
| Contenu | Si vous avez sélectionné la méthode POST ou PUT, entrez les propriétés spécifiques au service Web que vous utilisez, appariées aux valeurs de contenu utilisées pour la notification IBM. Voir le tableau [Valeurs de la section de contenu de maintenance et d'incident](index.html#payload) pour identifier les valeurs que vous pouvez utiliser. Si vous n'entrez pas d'informations dans cette section, vous recevrez une notification ne comportant pas d'information supplémentaire. |
| Combiner des notifications | Sélectionnez l'option permettant de combiner les notifications relatives aux incidents pour toutes les régions dans une seule notification. Cette option est disponible uniquement pour les incidents. |
{: caption="Tableau 5. Zones de formulaire pour un abonnement aux notifications par webhook sur la maintenance ou les incidents" caption-side="top"}


{: #webhooknotthresh}

| **Zone** | **Description** |
|-----------------|-------------------|
| Activé | Sélectionnez l'option d'activation de la notification. Effacez la sélection pour désactiver la notification. Les abonnements sont activés par défaut. |
| Type | Sélectionnez **Webhook**. |
| Evénement | Sélectionnez **Seuil**. |
| Seuil | Sélectionnez le type de seuil pour lequel vous voulez recevoir des notifications : quota d'organisation, disque physique, mémoire physique, disque réservé ou mémoire réservée.|
| Direction du seuil | Indiquez si vous voulez afficher les données de seuil dans l'ordre croissant ou décroissant.  |
| Notifier lors du passage sous le seuil (%) | Si vous avez sélectionné une **direction de seuil** **décroissante**, entrez le seuil en pourcentage à partir duquel vous voulez recevoir une notification. Lorsque le seuil passe sous ce pourcentage, la notification par webhook est envoyée. |
| Notifier lors du dépassement du seuil (%) | Si vous avez sélectionné une **direction de seuil** **croissante**, entrez le seuil en pourcentage à partir duquel vous voulez recevoir une notification. Lorsque le seuil dépasse ce pourcentage, la notification par webhook est envoyée. |
| Description | Ajoutez une description unique pour l'abonnement que vous créez. |
| Autorisation | Choisissez d'activer ou non l'autorisation.  Les options sont **De base** et **Aucune**. |
| Nom d'utilisateur | Si vous avez choisi l'autorisation De base, entrez votre nom d'utilisateur pour votre service Web. Si vous ne voulez pas utiliser vos données d'identification personnelles, vous pouvez configurer un ID fonctionnel à utiliser spécifiquement avec {{site.data.keyword.Bluemix_notm}}. |
| Mot de passe | Si vous avez choisi l'autorisation De base, entrez le mot de passe pour votre service Web. |
| Méthode | Sélectionnez **GET**, **POST** ou **PUT**. |
| URL | Entrez l'URL pour connexion à votre service Web. |
{: caption="Tableau 6. Zones de formulaire pour un abonnement aux notifications par webhook sur les seuils" caption-side="top"}

Les données de seuil sont collectées toutes les six heures. Une notification n'est envoyée qu'une fois lorsque la valeur dépasse ou passe sous la valeur que vous avez définie. Aucune nouvelle notification n'est envoyée sauf si la valeur passe sous le seuil, si vous avez choisi la propriété Croissant, puis dépasse à nouveau le seuil. De même, si vous avez choisi la propriété Décroissant, vous ne recevez de nouvelle notification que si la valeur dépasse le seuil que vous avez défini, puis passe à nouveau sous le seuil. 

Si vous ne voulez pas attendre six heures avant l'envoi de la notification lorsque le seuil est atteint, après avoir rempli les zones du formulaire, vous pouvez cliquer sur **Sauvegarder et tester** pour sauvegarder et tester la notification avec des exemples de données.

Une notification de seuil de quota inclut uniquement les organisations qui ont dépassé le pourcentage de seuil spécifié au cours de la période de 6 heures correspondant à cette notification. Les organisations qui ont dépassé un seuil au cours des périodes de 6 heures précédentes ne seront pas incluses, même si elles sont toujours au-dessus/au-dessous du seuil.  Les  trois ressources qui constituent un quota d'organisation (mémoire réservée, services et routes) sont considérées de manière indépendante lorsqu'il s'agit de déterminer si une notification de quota d'organisation doit être envoyée. Par exemple, si la quantité de mémoire réservée utilisée par une organisation dépasse 50 % du quota de l'organisation, un seuil de quota d'organisation configuré avec une valeur de 50 % provoque l'envoi d'une notification.  Ultérieurement, si le nombre de services utilisés par la même organisation dépasse 50 % du quota de l'organisation, même si la quantité de mémoire utilisée est inchangée, le même abonnement à un seuil de quota d'organisation provoque également l'envoi d'une notification.

{: #payload}

| **Valeur IBM** | **Description** | **Type d'événement** |
|----------------|----------------|------------------------|
| {{content.category}} | Services affectés | Incident |
| {{content.disruption}} | Composants affectés | Mise à jour de maintenance |
| {{content.message}} | Description du message |   Mise à jour de maintenance et incident |
| {{content.scheduleWindow.start}} | Date de début planifiée pour la mise à jour | Mise à jour de maintenance |
| {{content.scheduleWindow.end}} | Heure de fin planifiée pour la mise à jour | Mise à jour de maintenance |
| {{content.severity}} | Evaluation de la gravité | Incident |
| {{content.subCategoryName}} | Composants affectés | Incident |
| {{content.title}} | Titre du message | Mise à jour de maintenance et incident |
| {{region}} | Région affectée | Mise à jour de maintenance et incident |
| {{status}} | Statut de la mise à jour | Mise à jour de maintenance |
| {{type}} | Mise à jour ou incident | Mise à jour de maintenance et incident |
{: caption="Tableau 7. Valeurs de la section de contenu de maintenance et d'incident" caption-side="top"}


{: #threshpayload}

| **Valeur IBM** | **Description** | **Type d'événement** |
|----------------|----------------|------------------------|
| {{content.org_quota}} | Seuil de quota d'organisation | Seuil |
| {{content.physical_disk}} | Seuil de disque physique | Seuil |
| {{content.physical_memory}} | Seuil de mémoire physique | Seuil |  
| {{content.reserved_disk}} | Seuil de disque réservé | Seuil |
| {{content.reserved_memory}} | Seuil de mémoire réservée | Seuil |
{: caption="Tableau 8. Valeurs de la section de contenu de seuil" caption-side="top"}

Une fois votre abonnement aux notifications sauvegardé, vous recevrez des notifications via la méthode configurée. Les notifications apparaissent toujours aux emplacements suivants :  
 * Dans la page Statut pour les incidents
 * Dans la page Statut pour les événements de mise à jour de maintenance planifiés avec interruption
 * Dans la zone Notifications de la page Administration pour les mises à jour de maintenance

Vous pouvez sélectionner n'importe quel abonnement aux notifications sauvegardé, examiner l'activité récente ou l'éditer selon vos besoins. Cliquez sur une entrée d'activité récente pour la développer et visualiser les détails de son historique.

## Mises à jour de maintenance
{: #oc_schedulemaintenance}

Vous pouvez afficher les mises à jour de maintenance planifiées et en attente, si vous disposez du droit de superutilisateur (`ops.admin`), en cliquant sur **ADMINISTRATION &gt; INFORMATIONS SYSTEME &gt; *Nombre* en attente** pour accéder à la page **Mises à jour du système**.  Tous les utilisateurs de votre environnement peuvent afficher les événements de mise à jour de maintenance planifiés avec interruption en cliquant sur **Support** &gt; **Statut**.

**Remarque **: reportez-vous tout d'abord à la section [Définition de fenêtres de maintenance pré-approuvées](index.html#preapprovedmaintenance) ci-dessous. Ces fenêtres doivent être définies pour qu'IBM puisse planifier la maintenance de votre environnement.

<dl>
<dt>Mises à jour sans interruption</dt>
<dd>Une mise à jour sans interruption n'a pas d'impact sur votre environnement, vos applications en cours d'exécution ou l'accès de vos utilisateurs à vos applications. Ce type de mise à jour ne requiert pas d'approbation au cas par cas et est appliquée au cours des fenêtres de disponibilité pré-approuvées pour la maintenance que vous avez définies dans la page Mises à jour du système.</dd>
<dt>Mises à jour avec interruption</dt>
<dd>Une mise à jour avec interruption peut avoir un impact sur votre environnement, les applications en cours d'exécution ou l'accès de vos utilisateurs à vos applications. Vous devez planifier et approuver chacune de ces mises à jour de maintenance dans la fenêtre de maintenance de 21 jours allouée. Vous pouvez sélectionner la date et l'heure de déploiement suggérées, l'option pour n'importe laquelle de vos fenêtres pré-approuvées, ou bien ouvrir le calendrier afin de sélectionner trois dates et heures spécifiques parmi lesquelles IBM pourra choisir pour planifier la mise à jour.</dd>
</dl>


### Définition de fenêtres de maintenance pré-approuvées
{: #preapprovedmaintenance}

L'exécution des mises à jour de maintenance sans interruption est planifiée au cours d'une fenêtre de temps préalablement approuvée. Par défaut, deux fenêtres de disponibilité pour les mises à jour par semaine sont créées pour votre système. En général, elles sont définies pour se reproduire tous les samedis et dimanches soir. Vous pouvez changer les paramètres par défaut de l'une des façons suivantes :
 * Editez les fenêtres de mise à jour par défaut en choisissant un jour différent ou une heure de début différente, ou les deux.
 * Créez une fenêtre de mise à jour, puis supprimez la fenêtre de mise à jour par défaut.

Pour sauvegarder vos modifications, vous devez tout de même atteindre le temps minimal requis chaque semaine.

Vous devez définir au minimum 12 heures disponibles réparties sur au moins deux jours de la semaine. Par exemple, vous pouvez définir des créneaux de six heures sur deux jours distincts, ou des créneaux de quatre heures sur trois jours distincts. Pour garantir que les créneaux soient assez longs pour l'application d'une mise à jour, la durée de chaque créneau doit être d'au moins quatre heures.  

**Remarque **: seuls les utilisateurs disposant de l'autorisation de superutilisateur (`ops.admin`) peuvent planifier et approuver des mises à jour de maintenance.

1. Accédez à **ADMINISTRATION &gt; INFORMATIONS SYSTEME &gt; *Nombre* en attente &gt; Gérer la disponibilité**.
2. Développez la section **Gérer les fenêtres de disponibilité pour les mises à jour**.
3. Cliquez sur **Ajouter** ![Ajouter](images/add-new.png).
4. Définissez votre première fenêtre de disponibilité en sélectionnant la fréquence, la durée et l'heure de début de la fenêtre.
5. Facultatif : sélectionnez **Marquer comme préféré** si vous souhaitez définir votre fenêtre de disponibilité récurrente comme période de planification préférée pour vos déploiements. Les fenêtres préférées sont prioritaires, chaque fois que cela est possible.
6. Cliquez sur **Soumettre**.
7. Répétez ce processus jusqu'à ce que vous ayez rempli les exigences minimales pour les fenêtres hebdomadaires.

### Définition de fenêtres d'indisponibilité pour la maintenance
{: #blockpreapprovedmaintenance}

Vous pouvez choisir de définir des fenêtres d'indisponibilité pour les mises à jour spécifiques au cours desquelles votre environnement ne peut pas faire l'objet de mises à jour de maintenance sans interruption. Par exemple, vous pouvez choisir un week-end ou un jour férié pendant lequel l'activité est élevée et vous ne voulez pas appliquer de maintenance, afin de garantir que vos applications seront disponibles pour vos utilisateurs.

Vous devez définir au minimum 12 heures disponibles réparties sur au moins deux jours de la semaine. Lorsque vous tentez de créer une fenêtre d'indisponibilité pour les mises à jour, il se peut que vous ne parveniez pas à sauvegarder vos modifications si avec cette nouvelle fenêtre, votre système passe sous le minimum hebdomadaire requis. Dans ce cas, vous devez d'abord supprimer certaines des fenêtres d'indisponibilité pour les mises à jour existantes et ajouter d'autres fenêtres de disponibilité pour les mises à jour avant de pouvoir sauvegarder la nouvelle fenêtre d'indisponibilité pour les mises à jour. Voir [Définition de fenêtres de maintenance pré-approuvées](index.html#preapprovedmaintenance) pour plus d'informations.

1. Accédez à **ADMINISTRATION &gt; INFORMATIONS SYSTEME &gt; *Nombre* en attente &gt; Gérer la disponibilité**.
2. Développez la section **Gérer les fenêtres d'indisponibilité pour les mises à jour**.
3. Cliquez sur **Ajouter** ![Ajouter](images/add-new.png).
4. Définissez votre fenêtre d'indisponibilité en sélectionnant la fréquence, la durée et l'heure de début de la fenêtre.
5. Cliquez sur **Soumettre**.

### Planification et approbation des mises à jour
{: #scheduleandapprove}

Une fois que vous avez défini vos fenêtres de maintenance pré-approuvées, les mises à jour sans interruption sont planifiées automatiquement à ces heures. Votre approbation explicite pour ces types de mise à jour n'est pas requise. Toutefois, vous pouvez afficher les détails de chaque mise à jour de maintenance, notamment les éléments mis à jour, la durée de la mise à jour et l'heure de planification de la mise à jour.

Afin d'afficher les détails d'une mise à jour sans interruption, procédez comme suit :

1. Accédez à **ADMINISTRATION &gt; INFORMATIONS SYSTEME &gt; *Nombre * en attente**.
2. Identifiez les lignes pour lesquelles **Customer Scheduling Required** a pour valeur **No**.
3. Sélectionnez la ligne de cette mise à jour pour afficher les détails.

Une mise à jour avec interruption peut avoir un impact sur votre environnement, les applications en cours d'exécution ou l'accès de vos utilisateurs à vos applications. Vous devez planifier et approuver chacune de ces mises à jour de maintenance dans la fenêtre de maintenance de 21 jours allouée. Vous pouvez sélectionner la date et l'heure de déploiement suggérées, l'option pour n'importe laquelle de vos fenêtres pré-approuvées, ou bien ouvrir le calendrier afin de sélectionner trois dates et heures spécifiques parmi lesquelles IBM pourra choisir pour planifier la mise à jour.

Pour les mises à jour avec interruption requérant votre approbation, procédez comme suit :

1. Accédez à **ADMINISTRATION &gt; INFORMATIONS SYSTEME &gt; *Nombre * en attente**.
2. Identifiez les lignes pour lesquelles **Customer Scheduling Required** a pour valeur **Yes**.
3. Sélectionnez la ligne de cette mise à jour afin de consulter les détails de la mise à jour, notamment sa description, la date et l'heure suggérées pour la mise à jour, les composants affectés et la durée de la mise à jour.
4. Sélectionnez **Planifier et approuver**.
5. Choisissez l'une des options suivantes : **Date suggérée**, **Autres dates** ou **Toute fenêtre pré-approuvée**. Si vous sélectionnez **Autres dates**, vous pouvez ouvrir le calendrier pour sélectionner trois options parmi lesquelles IBM pourra choisir.
6. Facultatif : dans la liste des autres dates sélectionnées dans le calendrier, sélectionnez celles que vous souhaitez définir comme date préférées pour le déploiement. Chaque date sélectionnée est indiquée comme date préférée pour le déployeur qui planifie le déploiement. IBM essaie de planifier la maintenance dans les fenêtres de mises à jour préférées.
7. Quand vous avez terminé, cliquez sur **Soumettre**.

En fonction de votre sélection, la mise à jour est planifiée pour son déploiement à la date suggérée que vous avez acceptée, lors d'une des fenêtres pré-approuvées ou à l'une des dates et heures spécifiques que vous avez sélectionnées. Lorsque la mise à jour est planifiée pour son déploiement par IBM, la date planifiée est indiquée dans les détails de la mise à jour sur la page **Mises à jour du système**. Vous pouvez replanifier un déploiement déjà planifié uniquement si un jour (24 heures) avant la date et l'heure de début planifiées est conservé. Une fois que vous avez replanifié un déploiement, vous ne pouvez plus le redéployer à nouveau.


## Affichage des informations système
{: #oc_system}

Pour afficher les informations système, cliquez sur **ADMINISTRATION &gt; INFORMATIONS SYSTEME**.

Vous pouvez afficher diverses sections, notamment la section des mises à jour du système en attente, des informations système générales, des informations sur les API et l'interface de ligne de commande, et des détails sur la configuration LDAP.

### Mises à jour du système en attente

La section Mises à jour affiche le nombre de notifications relatives à des mises à jour en attente qui requièrent une intervention de votre part. Deux types peuvent s'afficher :

<dl>
<dt>Mises à jour sans interruption</dt>
<dd>Une mise à jour sans interruption n'a pas d'impact sur votre environnement, vos applications en cours d'exécution ou l'accès de vos utilisateurs à vos applications. Ce type de mise à jour ne requiert pas d'approbation au cas par cas. Ces mises à jour sont appliquées au cours des fenêtres de disponibilité pré-approuvées pour la maintenance que vous avez définies dans la page Mises à jour du système.</dd>
<dt>Mises à jour avec interruption</dt>
<dd>Une mise à jour avec interruption peut avoir un impact sur votre environnement, les applications en cours d'exécution ou l'accès de vos utilisateurs à vos applications. Vous pouvez planifier et approuver chacune de ces mises à jour de maintenance dans la fenêtre de maintenance de 21 jours allouée pour vous assurer que la mise à jour ne sera pas appliquée pendant les heures de bureau critiques. Vous pouvez sélectionner la date et l'heure de déploiement suggérées en fonction de vos fenêtres de mise à jour pré-approuvées ou sélectionner deux combinaisons date-heure supplémentaires parmi lesquelles IBM pourra choisir lors de l'application de la mise à jour.</dd>
</dl>

Pour plus d'informations sur la définition de fenêtres de maintenance pré-approuvées et la définition de dates d'indisponibilité spécifiques pour la maintenance, voir [Mises à jour de maintenance](index.html#oc_schedulemaintenance).

### Informations système générales

Dans la section Informations générales, vous pouvez consulter les informations suivantes :

- Des informations de base sur la génération {{site.data.keyword.Bluemix_notm}}.
- Des informations sur les API, notamment la version, l'adresse URL, la région et un lien vers la documentation de l'interface de ligne de commande.
- Des informations sur le domaine partagé concernant votre système et votre service.
- Des statistiques sur le nombre total d'applications, d'utilisateurs et d'organisations.

### Détails de la configuration LDAP

Dans la section Détails de la configuration LDAP, vous pouvez sélectionner le serveur LDAP et afficher des informations sur les mappages des utilisateurs et des groupes. Si vous utilisez un ID Web {{site.data.keyword.IBM}}, il est indiqué dans cette section.

## Affichage de l'utilisation et des rapports
{: #oc_resource}

Vous pouvez afficher différents types d'informations relatives à l'utilisation pour votre instance locale ou dédiée et pour votre compte
{{site.data.keyword.Bluemix_notm}}. Vous pouvez aussi télécharger et afficher des rapports de sécurité et des journaux pour votre instance
{{site.data.keyword.Bluemix_notm}}.

- Des informations sur les ressources, notamment l'espace disque, l'utilisation de l'unité centrale, l'utilisation du réseau et les temps de réponse moyens. Voir [Utilisation des ressources](index.html#resourceusage).
- L'utilisation du compte par organisation, notamment le nombre d'applications de contexte d'exécution et leur utilisation, le nombre total de Go/heure consommé par les contextes d'exécution, ainsi que le nombre d'instances de service et leur utilisation. Voir [Utilisation du compte](index.html#accountusage).
- L'utilisation du quota de mémoire des organisations, la mémoire allouée aux applications en fonction du quota de mémoire utilisé total, et une vue de la consommation de Go/heure par application pour une organisation spécifique. Vous pouvez aussi afficher l'utilisation du quota pour toutes les organisations dans la page Administration des organisations, dans la section **Surveillance des quotas**. Voir [Administration des organisations](../admin/index.html#orgusage).


### Utilisation des ressources
{: #resourceusage}

Pour afficher des informations relatives à l'utilisation des ressources, cliquez sur **ADMINISTRATION &gt; Utilisation
des ressources**.

Dans la section **Utilisation des ressources**, vous pouvez consulter les informations suivantes :

- Des informations sur l'utilisation des ressources, comme la quantité de mémoire et l'espace disque pouvant être réservés et physiquement disponibles, ainsi que la quantité de mémoire et l'espace disque actuellement réservés et physiquement utilisés.  Vous pouvez également consulter des informations sur l'utilisation moyenne de l'unité centrale dans tous les agents DEA. Pour des informations plus détaillées sur l'utilisation de la mémoire, du disque et de l'unité centrale, voir [Détails sur la mémoire, le disque et l'unité centrale](index.html#resourceusagedetails).
- Des informations sur l'utilisation du réseau relatives à la bande passante entrante et à la bande passante sortante, au cours des 6 dernières heures ou du dernier jour. Les données affichées dépendent de la somme du trafic entrant et sortant pour les réseaux publics et privés.
- Le temps de réponse moyen pour {{site.data.keyword.Bluemix_notm}} au cours des 10 dernières minutes, de la dernière heure et du dernier jour.
- Le nombre moyen de transactions par seconde pour {{site.data.keyword.Bluemix_notm}} au cours des dix minutes précédentes, de l'heure précédente ou du jour précédent.


#### Détails sur la mémoire système, le disque et l'unité centrale
{: #resourceusagedetails}

Dans la section **Utilisation des ressources**, vous pouvez afficher un récapitulatif des quantités **réservées** et **physiques** pour votre mémoire et votre disque.    
	<dl>
	<dt><strong>Physique</strong></dt>
	<dd>Quantité de mémoire ou espace disque acheté pour votre environnement.</dd>
	<dt><strong>Réservée</strong></dt>
	<dd>Quantité totale de mémoire ou espace disque disponible pour la réservation par toutes les applications déployées et en cours d'exécution dans votre environnement. Etant donné que les applications utilisent rarement toute la mémoire qu'elles réservent, la valeur physique est généralement inférieure à la valeur réservée.</dd>
	</dl>

En plus de la représentation graphique, vous pouvez afficher le pourcentage de mémoire et d'espace disque que votre environnement utilise. Vous pouvez également afficher les quantités réservées et physiques, en gigaoctets, dans le cadre de l'utilisation réelle, par rapport à la quantité disponible.

Pour afficher l'utilisation de votre mémoire, de votre disque ou de votre unité centrale par agent DEA, cliquez sur **Répartition**.  

Pour des informations plus détaillées sur votre utilisation de la mémoire réservée et physique ou du disque pour une période donnée, cliquez sur **Historique**. Vous pouvez choisir d'afficher les données hebdomadaires ou mensuelles. La vue de l'utilisation historique affiche un graphique de l'utilisation de la mémoire ou du disque pour la période que vous choisissez.  
	<dl>
	<dt><strong>Limite mémoire réservée</strong></dt>
	<dd>Affichée sous forme de ligne en pointillés horizontale, la limite mémoire réservée est la quantité totale de mémoire ou d'espace disque qui peut être réservée collectivement par toutes les applications qui s'exécutent dans votre environnement.</dd>
	<dt><strong>Réservée</strong></dt>
	<dd>La zone Réservée indique la mémoire ou l'espace disque qui est réservé collectivement par toutes les applications qui s'exécutent dans votre environnement.
	<p>Pour identifier les organisations qui ont réservé le plus de mémoire à un moment précis, passez votre souris sur le point à côté de la zone Réservée qui est associée à ce moment. Ensuite, vous pouvez cliquer sur une organisation dans le graphique circulaire pour afficher davantage d'informations sur cette organisation.</p></dd>
	<dt><strong>Limite physique</strong></dt>
	<dd>Affichée sous forme de ligne en pointillés horizontale, la limite physique indique la quantité de mémoire physique ou d'espace disque qui a été achetée pour votre environnement.</dd>
	<dt><strong>Physique</strong></dt>
	<dd>La zone Physique affiche la quantité de mémoire ou d'espace disque utilisée.</dd>
	</dl>
	
#### Détails sur l'utilisation du service 
{: #servicesresourceusage}

L'onglet **Service** affiche l'utilisation totale du service par rapport à la capacité maximale dont vous disposez pour un service dédié. Par exemple, si vous disposez d'un service Cloudant dédié et que vous utilisez 500 Go sur une capacité de 1000 Go, un graphique indique que vous avez utilisé 50 % de votre capacité totale. La couleur du graphique change selon que vous êtes proche ou non de la limite de capacité. Le jaune indique que vous avez utilisé entre 70 % et 84 % de votre capacité et le rouge est utilisé lorsque vous avez atteint 85 % ou plus de la capacité disponible. 

**Remarque** : à l'heure actuelle, il se peut que les informations sur la consommation du service ne soient pas disponibles dans tous les environnements. Cette fonction est disponible pour Cloudant, MessageHub, API Connect et Session Cache.


### Utilisation du compte
{: #accountusage}

Vous pouvez afficher l'utilisation mensuelle pour votre compte, pour votre environnement dédié ou local. Vous pouvez utiliser ces données afin de déterminer les frais à facturer à des organisations spécifiques en fonction de leur consommation. Tous les utilisateurs de la console d'administration qui disposent du droit **Utilisateurs** avec l'accès **Lecture** peuvent afficher les données d'utilisation du compte. De plus, les responsables de la facturation des organisations peuvent afficher les données d'utilisation du compte pour leurs organisations, même s'ils ne disposent pas du droit **Utilisateurs** dans la console d'administration. En tant qu'administrateur de la console (droit de superutilisateur), vous pouvez affecter le rôle de responsable de la facturation pour des organisations en cliquant sur **Compte** &gt; **Gérer les organisations**.

Pour afficher les données d'utilisation du compte, procédez comme suit :

<ol>
<li>Cliquez sur <strong>Compte</strong> &gt; <strong>Tableau de bord de l'utilisation</strong>.</li>
<li>Sélectionnez l'organisation pour laquelle afficher les données.</li>
<li>Vous pouvez afficher des détails sur l'utilisation pour les catégories suivantes :
<ul>
<li>Les applications de contexte d'exécution qui sont utilisées</li>
<li>L'utilisation totale des applications de contexte d'exécution en Go/heure</li>
<li>Les instances de service qui sont utilisées</li>
</ul>
</li>
<li>Facultatif : affichez vos données pour un mois spécifique en utilisant le menu <strong>Votre activité de cloud</strong> pour sélectionner le mois de votre choix.</li>
<li>Facultatif : cliquez sur <strong>EXPORTER DES DONNEES</strong> et sélectionnez <strong>CSV</strong> ou <strong>JSON</strong> afin d'exporter vos données pour le mois sélectionné dans un fichier <code>CSV</code> ou <code>JSON</code>.</li>
</ol>

Vous pouvez aussi afficher l'utilisation mensuelle et les frais associés au niveau du compte pour vos contextes d'exécution, vos applications et vos services qui sont mis à disposition depuis l'environnement {{site.data.keyword.Bluemix_notm}} public. Vous pouvez utiliser ces données afin de déterminer les frais à facturer à des organisations spécifiques en fonction de leur consommation.

<ol>
<li>Cliquez sur <strong>Compte</strong> &gt; <strong>Tableau de bord de l'utilisation</strong>.</li>
<li>Cliquez sur <strong>Public</strong>.</li>
<li>Sélectionnez l'organisation pour laquelle afficher les données.</li>
<li>Vous pouvez afficher des détails sur l'utilisation pour les catégories suivantes :
<ul>
<li>Les applications de contexte d'exécution qui sont utilisées</li>
<li>L'utilisation totale des applications de contexte d'exécution en Go/heure</li>
<li>Les instances de service qui sont utilisées</li>
<li>Un récapitulatif des frais pour tous les contextes d'exécution, tous les services et toutes les applications qui sont mis à disposition</li>
</ul>
</li>
<li>Facultatif : affichez vos données pour un mois spécifique en sélectionnant le mois de votre choix dans le graphique à barres. Les données pour le mois en cours s'affichent par défaut.</li>
<li>Facultatif : cliquez sur <strong>EXPORTER DES DONNEES</strong> et sélectionnez <strong>CSV</strong> ou <strong>JSON</strong> afin d'exporter vos données pour le mois sélectionné dans un fichier <code>CSV</code> ou <code>JSON</code>.</li>
</ol>


### Utilisation des organisations
{: #orgusage}

Pour afficher l'utilisation par organisation, cliquez sur **ADMINISTRATION &gt; ADMINISTRATION DES ORGANISATIONS**, puis sélectionnez une organisation dans **Liste des organisations**. La page **Gérer les organisations** de l'organisation sélectionnée affiche les informations suivantes sur l'utilisation :

- Le nombre de services utilisés
- Le nombre de routes utilisées
- Un graphique du quota de mémoire qui représente le quota utilisé et le quota non utilisé
- Un graphique de l'allocation des applications qui indique quelles sont les applications incluses dans le quota de mémoire utilisé
- Un graphique de l'utilisation des applications mesurée qui représente un rapport sur trois mois du nombre de Go/heure consommé par application déployée. Vous pouvez sélectionner la **vue Liste** pour examiner les données de toutes les applications, notamment l'allocation mémoire par application et l'utilisation mesurée en Go par heure au cours des trois derniers mois.

Pour plus d'informations sur l'affichage de l'utilisation par organisation, l'ajustement des plans d'établissement des quotas et la gestion de vos organisations, voir [Administration des organisations](../admin/index.html#oc_organizations).

### Rapports
{: #oc_report}

Vous pouvez afficher des journaux et des rapports de sécurité, tels que des rapports DataPower&trade;, de pare-feux et d'audit de connexion, pour votre instance {{site.data.keyword.Bluemix_notm}}. Pour afficher les rapports et les journaux, cliquez sur **ADMINISTRATION &gt; RAPPORTS ET JOURNAUX**.

Effectuez l'une des opérations suivantes :

- Vous pouvez sélectionner des dates de début et de fin dans les zones afin de filtrer les rapports et les journaux à afficher.
- Vous pouvez développer et afficher divers rapports depuis le panneau de navigation.
- Vous pouvez effectuer une recherche dans votre collection de rapports et de journaux. La recherche s'applique aux noms de rapport ainsi qu'au contenu textuel des rapports et des journaux. Vous pouvez aussi choisir de filtrer votre recherche par **événements d'administration**, **rapports DataPower**, **pare-feu** et **audit de connexion**.
- Lors de l'affichage d'un rapport ou d'un journal, vous pouvez cliquer sur l'icône ![Télécharger](images/icon_download.png) pour télécharger le rapport.

Le tableau ci-dessous présente la liste des rapports de sécurité qui sont générés pour l'environnement {{site.data.keyword.Bluemix_notm}} local et l'environnement {{site.data.keyword.Bluemix_notm}} dédié. La plupart des rapports sont générés quotidiennement. Toutefois, les rapports sur les événements de gestion des clés et de chiffrement sont générés mensuellement. Tous les rapports sont conservés pendant 90 jours dans la console d'administration, à partir de laquelle vous pouvez y accéder. Au bout de ces 90 jours, {{site.data.keyword.Bluemix_notm}} les tient à disposition hors ligne sur demande pendant 9 mois. Au total, les rapports sont disponibles en vue de leur extraction pendant un an.


{: #ld_table9}

| **Catégorie** | **Rapport** | **Description** |      
|-----------------|-------------------|---------------------|
| Pare-feu | Connexions au pare-feu | Evénements liés à la connexion de l'administrateur aux unités de pare-feu Vyatta. |
| Pare-feu | Refus du pare-feu | Evénements générés par les unités de pare-feu Vyatta lorsqu'une demande d'accès est refusée selon les règles de pare-feu appliquées. |
| Evénements de connexion d'administrateur {{site.data.keyword.Bluemix_notm}} | Connexion des administrateurs {{site.data.keyword.Bluemix_notm}} | Evénements générés par le système d'exploitation lorsqu'un administrateur démarre une session SSH sur chaque système {{site.data.keyword.Bluemix_notm}}. |
| Evénements de connexion de développeur d'applications {{site.data.keyword.Bluemix_notm}} | Connexion des développeurs d'applications {{site.data.keyword.Bluemix_notm}} | Evénements générés par le composant de connexion à la plateforme {{site.data.keyword.Bluemix_notm}} lorsqu'un utilisateur de la plateforme {{site.data.keyword.Bluemix_notm}} démarre une session via la ligne de commande, les API REST ou l'interface utilisateur {{site.data.keyword.Bluemix_notm}}. |
| Evénements d'administration d'administrateur {{site.data.keyword.Bluemix_notm}} | Evénements d'administration du système d'exploitation des administrateurs {{site.data.keyword.Bluemix_notm}} | Evénements générés par le système d'exploitation lorsqu'un administrateur effectue une action dans une session de travail en cours. |
| Evénements d'administration de développeur d'applications {{site.data.keyword.Bluemix_notm}} | Evénements d'administration (Cloud Foundry) {{site.data.keyword.Bluemix_notm}} | Evénements liés aux opérations effectuées par l'utilisateur de la plateforme {{site.data.keyword.Bluemix_notm}} via la ligne de commande, les API REST ou l'interface utilisateur {{site.data.keyword.Bluemix_notm}}. |
| Evénements d'administration de base de données d'administrateur {{site.data.keyword.Bluemix_notm}} | Evénements d'administration de base de données | Evénements liés aux opérations effectuées par un administrateur de base de données sur les bases de données internes {{site.data.keyword.Bluemix_notm}}. |
| Evénements d'administration | Evénements de gestion des utilisateurs | Evénements liés aux actions de gestion des utilisateurs effectuées dans la page Administration. |
| Evénements d'administration | Catalogue | Evénements liés aux modifications du catalogue des services. |
| Evénements d'administration | Evénements de gestion des rapports de sécurité | Evénements liés aux actions de gestion des rapports de sécurité effectuées dans la page Administration. |
| Révisions d'accès | Rapport sur les révisions d'accès | Révisions pour les accès privilégiés. |
| Gestion des modifications | Gestion des modifications logicielles | Activité de gestion des modifications. |
| Gestion des clés | Gestion des certificats SSL personnalisés | Certifications SSL personnalisées qui ont été téléchargées et stockées. |
| Chiffrement | Chiffrement des données en transit | Chiffrement des données en transit configuré. |
| Antivirus | Rapport d'analyse antivirus | Logiciel antivirus installé. |
| Gestion des correctifs logiciels | Rapport d'application des correctifs | Correctifs logiciels appliqués. |
| Gestion des incidents de sécurité | Rapport de résolution des incidents de sécurité | Preuve des incidents de sécurité pour la gestion des incidents de sécurité. |
{: caption="Tableau 9. Liste des rapports de sécurité" caption-side="top"}

## Affichage du statut
{: #oc_status}

Vous pouvez afficher le statut de l'environnement {{site.data.keyword.Bluemix_notm}} et de la console d'administration.

### Statut de l'environnement {{site.data.keyword.Bluemix_notm}}

Vous pouvez surveiller le statut de votre instance {{site.data.keyword.Bluemix_notm}} à l'aide de la page Statut de {{site.data.keyword.Bluemix_notm}}. Cliquez sur **Support** &gt; **Statut**.

La page Statut est l'emplacement central pour rechercher des notifications et des annonces sur les événements clés affectant la plateforme {{site.data.keyword.Bluemix_notm}} et les principaux services dans {{site.data.keyword.Bluemix_notm}}. Vous pouvez vous abonner à un flux RSS pour recevoir les notifications automatiquement et ne pas avoir à les rechercher. Pour plus d'informations sur la page Statut et la configuration du flux RSS, voir [Affichage de {{site.data.keyword.Bluemix_notm}}](../support/index.html#viewing-bluemix-status).

### Statut de la console d'administration

Après le déploiement initial de votre environnement {{site.data.keyword.Bluemix_notm}}, une vérification est effectuée automatiquement sur les composants utilisés pour administrer l'environnement. Vous pouvez accéder à la page Vérification de la console d'administration afin de vérifier le statut des composants après l'exécution de la vérification. Pour ouvrir cette page, accédez à <code>https://console.&lt;sous-domaine&gt;.bluemix.net/check</code>, où `<sous-domaine>` est le nom de votre instance locale ou dédiée.

Vous pouvez effectuer une vérification à tout moment. Vous devez être connecté pour pouvoir sélectionner l'option d'exécution de la vérification. Si vous rencontrez des problèmes lors de l'ajout d'un utilisateur, de l'édition d'une organisation ou de la gestion de vos services, exécutez cette vérification afin de déterminer si des composants sont défaillants ou déconnectés. Vous pouvez ouvrir un ticket de demande de service avec les informations générées par la vérification pour une résolution rapide du problème.

## Gestion de votre catalogue
{: #oc_catalog}

Vous pouvez choisir les services {{site.data.keyword.Bluemix_notm}} que les utilisateurs peuvent voir dans le catalogue {{site.data.keyword.Bluemix_notm}}. Cliquez sur **ADMINISTRATION &gt; GESTION DES CATALOGUES**.

Sélectionnez une vignette de service pour éditer la visibilité du plan de service. Pour éditer la visibilité, sélectionnez l'une des options suivantes :

- Pour afficher un service masqué de sorte que vos utilisateurs puissent le voir dans le catalogue, sélectionnez **ACTIVER TOUS LES PLANS**.
- Pour masquer un service de sorte que vos utilisateurs ne le voient pas dans le catalogue {{site.data.keyword.Bluemix_notm}}, sélectionnez **DESACTIVER TOUS LES PLANS**.
- Pour contrôler la visibilité d'un plan individuel, sélectionnez le nom du plan, puis utilisez le menu déroulant afin de sélectionner **Activer pour toutes les organisations**, **Désactiver pour toutes les organisations** ou **Activer le plan pour des organisations spécifiques**.

<!-- staging only start -->

Vous pouvez également gérer l'ordre de priorité des packs de construction disponibles pour sélection par vos développeurs lorsqu'ils créent des applications compte tenu de leur compatibilité.

1. Accédez à **ADMINISTRATION &gt; GESTION DU CATALOGUE**.
2. Accédez à la section **Traitement**.
3. Sélectionnez **Priorité du pack de construction**.
4. Sélectionnez dans la liste l'option de pack de construction dont vous désirez définir la priorité.
5. Cette option étant sélectionnée, utilisez les flèches pour déplacer l'option dans la liste.

<!-- staging only end -->

### Enregistrement d'un courtier de services
{: #servicebrokerui}

Si vous voulez afficher un service dans votre catalogue {{site.data.keyword.Bluemix_notm}}, vous devez implémenter et enregistrer un [courtier de services ![Icône de lien externe](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/services/api.html){: new_window}. Une fois votre courtier enregistré, vous pouvez choisir les organisations qui peuvent accéder au service dans votre instance locale ou dédiée.

Les méthodes d'utilisation de votre courtier de services dépendent du nombre de services qu'il gère ou varient selon qu'il a déjà été enregistré dans {{site.data.keyword.Bluemix_notm}} ou non.

- Si votre courtier de services gère un service, vous pouvez vous servir de l'interface utilisateur pour l'enregistrer après avoir implémenté l'[API de courtier de services ![Icône de lien externe](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/services/api.html){: new_window}. Voir [Enregistrement d'un courtier de services qui gère un service](index.html#registerbrokerui).
- Si votre courtier de services gère plusieurs services, utilisez l'interface de ligne de commande cf avec le plug-in d'[interface de ligne de commande d'administration de {{site.data.keyword.Bluemix_notm}}](../cli/plugins/bluemix_admin/index.html) (sous-commande `ba`), ou utiliser l'[API de service personnalisé](index.html#servicebrokerapi).
- Si votre courtier de services est déjà enregistré et que vous voulez le mettre à jour ou le supprimer, utilisez l'interface de ligne de commande cf avec le plug-in d'[interface de ligne de commande d'administration {{site.data.keyword.Bluemix_notm}}](../cli/plugins/bluemix_admin/index.html) (sous-commande `ba`) ou utilisez l'[API de service personnalisé](index.html#servicebrokerapi).

#### Enregistrement d'un courtier de services qui gère un service
{: #registerbrokerui}

<!-- staging only start -->

Prenez connaissance des informations suivantes et effectuez les étapes d'enregistrement de votre courtier de services :

**Avant de commencer** : <a href="http://docs.cloudfoundry.org/services/api.html" target="_blank">implémentez l'API de courtier de services Cloud Foundry <img src="../icons/launch-glyph.svg" alt="Icône de lien externe"></a> pour permettre la communication entre votre service et {{site.data.keyword.Bluemix_notm}}. L'API de courtier de services est un ensemble de noeuds finaux REST consommés par {{site.data.keyword.Bluemix_notm}}.

Lorsque vous implémentez le courtier de services, dans la réponse JSON de <code>GET /v2/catalog</code>, vous devez fournir les définitions pour vos service et vos plans de service, notamment les informations relatives au service que vous voulez afficher. Par exemple, examinez l'exemple de code JSON de la réponse du catalogue (GET) :

```
{
"services":[
   {
      "bindable":true,
      "description":"Cool Service est une solution d'analyse et d'entreposage de données.",
      "id":"cool-service-id",
      "name":"coolservice",
      "metadata":{
         "displayName":"Cool Service",
         "serviceMonitorApi":"https://myservicesstatus.mybluemix.net/healthcheck/",
         "providerDisplayName":"Société Cool"
         "longDescription":"Cool Service est une solution d'analyse et d'entreposage de données. Vous pouvez placer rapidement vos données dans une base de données de la prochaine génération structurant les données en colonne en mémoire et commencer à exécuter des requêtes analytiques complexes.",
         "bullets":[
            {
               "title":"Rapide et simple",
               "description":"Cool Service utilise des innovations et la technologie structurant les données en colonne en mémoire, comme le traitement vectoriel parallèle et la compression afin d'analyser et de renvoyer rapidement les données pertinentes."
            },
            {
               "title":"Connectivity",
          "description": "Cool Service a été conçu pour vous permettre de vous connecter facilement à tous vos services et à toutes vos applications. Vous pouvez commencer à analyser vos données immédiatement à l'aide d'outils familiers."
         ],
         "featuredImageUrl":"http://chemin/icon_64x64.png",
         "imageUrl":"http://chemin/icon_50x50.png",
         "mediumImageUrl":"http://chemin/icon_32x32.png",
         "smallImageUrl":"http://chemin/icon_24x24.png",
         "documentationUrl":"http://chemin/documentation.html",
         "instructionsUrl":"http://chemin/servicesample.md",
         "termsUrl":"http://chemin/terms_of_agreement.pdf",
         "media":[
            {
               "type":"youtube",
               "thumbnailUrl":"http://chemin/thumbnail.png",
               "url":"http://chemin/video/youtube",
               "caption":"Utilisez Cool Service en 60 secondes"
            },
            {
               "type":"image",
               "thumbnailUrl":"http://chemin/thumbnail.png",
               "url":"http://chemin/image_file.png",
               "caption":"Cool Service connecte des applications"
            },
            {
               "type":"video",
               "thumbnailUrl":"http://chemin/thumb.png",
               "caption":"Cool Service fonctionne avec des tables",
               "source":[
                  {
                     "type":"video/mp4",
                     "url":"http://chemin/video_file.mp4"
                  },
                  {
                     "type":"video/ogg",
                     "url":"http://chemin/video_file.ogg"
                  }
               ]
            }
         ]
      },
      "plans":[
         {
            "name":"smallplan",
            "description":"Schéma et espace table dédiés par instance de service sur un serveur partagé. 1 Go et 10 Go de stockage de base de données compressées peuvent contenir respectivement jusqu'à 5 Go et 50 Go de données non compressées selon des taux de compression standard.",
            "free":false,
            "id":"cool-service-plan-id",
            "metadata":{
               "bullets":[
                  "1 Go minimum par instance. 10 Go maximum par instance."
               ],
               "costs":[
                  {
                     "unitId":"INSTANCES_PAR_MOIS",
                     "unit":"PAR MOIS",
                     "partNumber":"D15UTLL"
                  }
               ],
               "displayName":"Small"
            }
         }
      ]
   }
]
}
```
{: codeblock}

Les tableaux ci-dessous peuvent vous aider à remplir le fichier JSON.


{: #ld_table10}

| **Zones JSON** | **Description** |
|-----------------|-----------------|
|bindable   | Valeur booléenne qui indique si des instances de service peuvent être liées à des applications.  |
|description | Description du service qui s'affiche lorsque vous utilisez la commande cf marketplace ou passez votre souris sur l'icône de service dans le catalogue de l'interface utilisateur {{site.data.keyword.Bluemix_notm}}. Vous pouvez ajouter une phrase unique comme description. |
|name | Nom du service qui s'affiche dans l'interface de ligne de commande cf. Il doit être unique dans {{site.data.keyword.Bluemix_notm}} et doit utiliser des minuscules et ne pas contenir d'espace. Vous ne pouvez pas le changer une fois le service enregistré auprès de {{site.data.keyword.Bluemix_notm}}. |
|id  | ID du service. Il doit être unique dans {{site.data.keyword.Bluemix_notm}} et il doit s'agir d'un identificateur global unique. Vous ne pouvez pas le changer une fois le service enregistré auprès de {{site.data.keyword.Bluemix_notm}}. |
|metadata | Métadonnées du plan de service qui s'affichent dans le catalogue {{site.data.keyword.Bluemix_notm}} et dans la fiche de prix. La zone metadata est facultative. Vous pouvez spécifier d'autres zones pour les métadonnées. Voir le tableau suivant intitulé [Zones de métadonnées](index.html#metadatafields) pour plus d'informations. |
|plans | Tableau de définitions de plan de service. Voir le tableau suivant intitulé [Zones de plan](index.html#planfields) pour plus d'informations. |
{: caption="Tableau 10. Zones JSON" caption-side="top"}


{: #metadatafields}

| **Valeurs des métadonnées** | **Description** |
|---------------------|-----------------|
|displayName          | Nom du plan qui est affiché dans l'interface utilisateur de {{site.data.keyword.Bluemix_notm}}. Il est affiché dans la page des détails du service dans le catalogue ainsi que dans la fiche de prix. La première lettre du plan seulement doit être en majuscule. N'utilisez pas "Default" comme nom de plan par défaut ; utilisez plutôt "Standard". |
|providerDisplayName | Nom du fournisseur de services. |
|longDescription | Description détaillée du service. Envisagez d'utiliser deux phrases au moins pour une description longue. |
|plans                | Tableau de définitions de plan de service. Chaque entrée de tableau dans la zone des plans se compose des zones suivantes : name, description, free, id et metadata. Voir le tableau suivant intitulé [Zones de plan](index.html#planfields) pour plus d'informations. |
|bullets | Tableau de chaînes affichées pour un service. Vous pouvez utiliser des puces pour fournir des informations en plus de la description longue. La zone bullets doit contenir deux éléments de puce au moins. Chaque puce inclut la zone de titre et la zone de description. |
|imageUrl | Adresse URL d'une grande image PNG (50 x 50 pixels). |
|smallImageUrl | Adresse URL d'une petite image PNG (24 x 24 pixels). |
|mediumImageUrl | Adresse URL d'une image moyenne PNG (32 x 32 pixels). |
|featuredImageUrl | Adresse URL de l'image mise en évidence (64 x 64 pixels). |
|documentationUrl | Adresse URL de la documentation sur le service. |
|termsUrl | Adresse URL des fichiers PDF contenant les termes du contrat. |
|media (facultative) | Tableau d'éléments pour l'affichage des vidéos et des captures d'écran qui présentent le service dans l'interface utilisateur {{site.data.keyword.Bluemix_notm}}. Un élément media peut contenir les zones suivantes : type (image, youtube, video), thumbnailUrl (adresse URL de l'image d'aperçu pour l'élément de support, url (adresse URL de la capture d'écran ou de la vidéo YouTube), source (sources des vidéos qui ne sont pas hébergées sur YouTube. Le "type" de la source de la vidéo doit être pris en charge par HTML5. Incluez les zones "type" et "url" pour la vidéo.), et caption (légende pour l'élément media. Les légendes contribuent à l'accessibilité pour les personnes souffrant de handicaps et leur permettent de comprendre vos éléments support.). |
|serviceKeysSupported | Valeur booléenne qui indique si l'API des clés de service est prise en charge. Celle-ci permet d'activer un service à utiliser hors de {{site.data.keyword.Bluemix_notm}}. La valeur par défaut est false. |
|plan_updateable | Valeur booléenne qui indique si le service prend en charge les changements de plan. La valeur par défaut est false. |
|embeddableDashboard (facultative) | Zone qui indique comment le tableau de bord du service est affiché dans l'interface utilisateur de {{site.data.keyword.Bluemix_notm}}. Si vous ne spécifiez pas cette zone, le tableau de bord est imbriqué mais est limité à une largeur minimale de 960 pixels et présente un remplissage horizontal supplémentaire autour de l'iframe. Vous pouvez utiliser true, false, drilldown ou launch. Vous pouvez utiliser les zones suivantes pour cette valeur : true, false, drilldown et launch.  |
|notCreatable (facultative) | Valeur booléenne qui indique si des instances pour le service peuvent être créées depuis l'interface utilisateur {{site.data.keyword.Bluemix_notm}} et depuis l'interface de ligne de commande cf. La valeur true signifie que les instances de service ne peuvent pas être créées depuis l'interface utilisateur {{site.data.keyword.Bluemix_notm}} ou l'interface de ligne de commande cf. La valeur par défaut est false. |
|notCreatableMessage (facultative) | Message affiché dans l'interface utilisateur {{site.data.keyword.Bluemix_notm}} si des instances de service ne peuvent pas être créées. Si vous ne spécifiez pas cette zone, le message par défaut suivant est affiché : Pour être averti de sa disponibilité, confirmez votre adresse électronique ou entrez une nouvelle adresse. |
|notCreatableRobotMessage (facultative) | Message affiché dans la bulle de la page des détails du service dans l'interface utilisateur {{site.data.keyword.Bluemix_notm}}. Il indique qu'un service présente un problème ou toute autre raison rendant le service indisponible. Vous pouvez spécifier un message afin d'expliquer la raison. Si vous ne spécifiez pas cette zone, le message par défaut suivant est affiché : Ce service n'est pas disponible actuellement. |
|apiReferenceUrl (facultative) | Adresse URL de l'iframe dans la zone Référence d'API de la page des détails du service dans le catalogue. Si elle n'est pas utilisée pour la page des détails du service dans le catalogue, vous pouvez entrer la valeur numérique affectée à votre documentation d'API REST pour votre service lorsque vous avez enregistré le service dans le microservice de la documentation d'API REST {{site.data.keyword.Bluemix_notm}}. Ainsi, votre documentation d'API REST s'affichera dans le tableau de bord du service. |
|sdkDownloadUrl (facultative) | Adresse URL de la page Web qui est ouverte lorsque vous cliquez sur le bouton Télécharger les logiciels SDK. Ce dernier se trouve sur la vignette du service dans la page de présentation des applications dans le	tableau de bord. La page Web est ouverte dans un nouvel onglet de navigateur. |
|serviceMonitorApi    | Adresse URL d'une API qui renvoie les données JSON indiquant la santé du service, conformément à l'exemple ci-après. La zone serviceMonitorApi ou serviceMonitorApp doit être définie dans vos métadonnées de service. Voir l'exemple de code ci-après. |
|serviceMonitorApp    | Adresse URL d'une application qui peut être déployée dans {{site.data.keyword.Bluemix_notm}} et liée à un service afin de fournir la sortie spécifique de statut du service. L'application doit renvoyer le même format de données JSON que serviceMonitorApi. La zone serviceMonitorApi ou serviceMonitorApp doit être définie dans vos métadonnées de service. Voir l'exemple de code ci-après. |
{: caption="Tableau 11. Zones de métadonnées" caption-side="top"}


```
{
    "service": "nomservice",
    "version": 1,
    "health": [
        {
            "plan": "starter",
            "status": 0,
            "serviceinput": "count(*) from healthcheck",
            "serviceoutput": "10…or error 1234 database not running",
            "responsetime": 4
        },
        {
            "plan": "enterprise",
            "status": 1,
            "serviceinput": "count(*)fromhealthcheck",
            "serviceoutput": "10…orerror1234databasenotrunning",
            "responsetime": 4
        }
    ]
}
```
{: pre}

L'exemple suivant montre comment la réponse JSON de GET /v2/catalog est mappée à la page des détails du service dans le catalogue {{site.data.keyword.Bluemix_notm}} :

![Détails du service dans le catalogue.](images/metadata.png "Vue des détails du service dans le catalogue Bluemix")


{: #planfields}

| **Valeurs de plan** | **Description** |
|---------------------|-----------------|
|name       | Nom du service qui est utilisé dans l'interface de ligne de commande cf. Par exemple, le nom du plan est affiché dans la sortie de la commande cf marketplace. Il doit être en minuscules, ne pas contenir d'espace, et être unique dans le service.  |
|description       | Description du plan de service. Elle est affichée une fois que vous sélectionnez un plan dans la page des détails du service dans le catalogue {{site.data.keyword.Bluemix_notm}}. |
|free      | Valeur booléenne qui indique si le plan de service est gratuit. La valeur par défaut est true. |
|id       | ID du plan de service. Il doit être unique et il doit s'agir d'un identificateur global unique.  |
|metadata (facultative)    | Métadonnées du plan de service qui s'affichent dans le catalogue {{site.data.keyword.Bluemix_notm}} et dans la fiche de prix. La zone metadata est facultative. Vous pouvez spécifier les zones suivantes dans la zone metadata : displayName, type (subscription, reservable, planDetails), bullets, costs (unitId, unit, partNumber) et paidOnly. Voir le tableau ci-après intitulé [Zones de métadonnées de plan](index.html#planmetadata) pour plus d'informations. |
{: caption="Tableau 12. Zones de plan" caption-side="top"}


{: #planmetadata}

| **Valeurs des métadonnées de plan** | **Description** |
|------------------------|-----------------|
|displayName             | Nom du plan qui est affiché dans l'interface utilisateur de {{site.data.keyword.Bluemix_notm}}. Il est affiché dans la page des détails du service dans le catalogue ainsi que dans la fiche de prix.   |
|type                    | Type de plan. Vous pouvez utiliser les valeurs suivantes pour cette zone : subscription (un plan d'abonnement. La valeur par défaut est false.), reservable (un plan réservable. Cette valeur n'est utilisée que lorsque le plan est un plan d'abonnement, c'est-à-dire lorsque la valeur de plan.metadata.subscription est true. La valeur par défaut est false.), planDetails (quantité détaillée et description des ressources pouvant être utilisées avec le plan. Cette valeur n'est utilisée que lorsque le plan est réservable, c'est-à-dire lorsque la valeur de plan.metadata.reserveable est true.) |
|bullets                 | Description des ressources pouvant être utilisées avec le plan. Elle est affichée dans la colonne **Fonctions** dans la page des détails du service du catalogue et dans la fiche de prix. |
|costs                   | Informations sur le coût du service qui sont affichées dans la colonne Prix dans la page des détails du service du catalogue et dans la fiche de prix. Chaque entrée de tableau contient les zones suivantes : unitId (ID de l'unité. Utilisez le pluriel et des majuscules seulement. Pour les plans gratuits, cette zone est facultative.), unit (mesure utilisée pour le calcul du prix du service. La valeur de cette zone est utilisée dans l'interface utilisateur {{site.data.keyword.Bluemix_notm}} pour représenter le paramètre de calcul des frais.), et partNumber (identificateur `part_number` utilisé par le système de facturation. Pour les plans gratuits, cette zone est facultative.).   |
|paidOnly (facultative)     | Valeur booléenne qui indique si ce plan de service est disponible pour les comptes {{site.data.keyword.Bluemix_notm}} payants seulement. Si la valeur est **true**, le plan de service n'est valable que pour les comptes payants et ne peut pas être ajouté à des comptes d'essai. Si la valeur est **false**, le plan de service peut être ajouté à des comptes payants et à des comptes d'essai. La valeur par défaut est **false**.	  |
{: caption="Tableau 13. Zones de métadonnées de plan" caption-side="top"}

L'exemple ci-après montre comment la réponse JSON de GET /v2/catalog est mappée à la page des détails du service dans le catalogue {{site.data.keyword.Bluemix_notm}}. Il illustre notamment comment les zones de métadonnées de plan décrites dans le tableau précédent sont mappées à l'interface utilisateur :

![Détails des métadonnées de plan dans le catalogue Bluemix.](images/plan_metadata.png "Vue des valeurs des métadonnées de plan dans le catalogue Bluemix")


<!-- staging only end -->

<ol>
<li>Après avoir implémenté l'API de courtier de services, accédez à <strong>Administration</strong> &gt; <strong>Gestion du catalogue</strong>.</li>
<li>Cliquez sur <strong>Enregistrement d'un courtier de services</strong>.</li>
<li>Remplissez le formulaire en entrant des valeurs dans les zones suivantes :
<ul>
<li>Nom du courtier de services</li>
<li>Adresse URL du courtier de services</li>
<li>Nom d'utilisateur du courtier de services</li>
<li>Mot de passe du courtier de services</li>
</ul>
</li>
<li>Cliquez sur <strong>CONNECTER</strong>.</li>
<li>Passez en revue les informations relatives à votre service, notamment les plans disponibles, l'icône et la description du service.<br />
<p><strong>Remarque</strong> : si vous devez changer les informations de catalogue pour le service, mettez à jour votre courtier de services et lancez à nouveau le processus d'enregistrement en remplissant le formulaire.</p>
</li>
<li>Cliquez sur <strong>ENREGISTRER</strong>.</li>
<li>Choisissez d'activer tous les plans ou des plans spécifiques seulement pour le service. Tous les plans sont désactivés par défaut.</li>
<li>Activez l'instance de service pour toutes les organisations ou pour des organisations spécifiques.</li>
</ol>

A présent, votre service apparaît dans la catégorie Services personnalisés de votre catalogue {{site.data.keyword.Bluemix_notm}}. Accédez à **ADMINISTRATION &gt; GESTION DES CATALOGUES** et sélectionnez la vignette dans le catalogue. Vous pouvez activer différents plans et éditer la visibilité d'un plan pour vos organisations à tout moment.


## Administration des organisations
{: #oc_organizations}

Vous pouvez gérer vos organisations en créant et en supprimant des organisations, en ajoutant ou en retirant des responsables pour les organisations, et en surveillant l'utilisation des quotas afin de prendre les meilleures décisions pour votre entreprise.

Cliquez sur **ADMINISTRATION &gt; ADMINISTRATION DES ORGANISATIONS**.

Vous pouvez développer et afficher diverses sections. Vous pouvez aussi passer en revue et gérer les plans d'établissement des quotas pour vos organisations.

### Création d'organisations

Pour créer une organisation et ajouter des responsables, procédez comme suit :

1. Cliquez sur <strong>CREATION D'ORGANISATION</strong>.
2. Entrez un nom pour l'organisation.
3. Entrez le nom ou l'adresse électronique de la personne à ajouter en tant que responsable. Vous pouvez ajouter plusieurs responsables en entrant et en sélectionnant plusieurs noms.
4. Cliquez sur <strong>CREATION D'ORGANISATION</strong> pour sauvegarder vos modifications et créer l'organisation.

### Création d'espaces

Vous pouvez créer des espaces dans votre organisation, par exemple un espace *dev* comme environnement de développement, un espace *test* comme environnement de test et un espace *production* comme environnement de production. Ensuite, vous pouvez associer vos applications à des espaces. Procédez comme suit pour créer un espace :

1. Dans la barre de menu, cliquez sur **Compte** &gt; **Gérer les organisations**.
2. Sélectionnez l'organisation à laquelle ajouter un espace.
3. Cliquez sur **Créer un espace**.
4. Entrez un nom d'espace.
5. Cliquez sur **Créer**.

### Surveillance des quotas

Vous pouvez développer la section **Surveillance des quotas** pour afficher les informations suivantes :

- L'utilisation de la mémoire de l'environnement présente en détail l'utilisation de la mémoire dans l'environnement système complet. Le graphique affiche les informations suivantes :
<ul>
<li>La mémoire physique qui est utilisée et la limite de mémoire physique qui est disponible</li>
<li>Le quota de mémoire qui est actuellement réservée et la limite de mémoire qui peut être réservée</li>
<li>Le quota total de mémoire pour vos organisations</li>
</ul>
Les types ci-après d'utilisation de la mémoire sont affichés dans le graphique.

	<dl>
	<dt><strong>Mémoire physique utilisée</strong></dt>
	<dd>Quantité de mémoire physique utilisée par votre environnement.</dd>
	<dt><strong>Limite physique</strong></dt>
	<dd>Quantité de mémoire physique totale qui est disponible dans votre environnement.</dd>
	<dt><strong>Quota mémoire réservée</strong></dt>
	<dd>Quantité de mémoire réservée pour toutes les applications déployées, dans toutes les organisations. La somme du quota qui est réservé peut dépasser la limite physique de mémoire pour votre environnement. Par exemple, si la limite de mémoire physique est de 16 Go, vous pouvez réserver 4 Go de mémoire à chaque application, pour un total de cinq applications différentes. Le quota qui est réservé dépasse la limite physique de mémoire. Cependant, dans la plupart des cas, les applications n'utilisent pas le quota total qui est réservé individuellement pour chaque application. De plus, les applications n'utilisent pas toutes la totalité de leur quota de mémoire réservée simultanément.</dd>
	<dt><strong>Limite de réservation</strong></dt>
	<dd>Mémoire totale pouvant être réservée pour toutes les applications dans votre environnement.</dd>
	<dt><strong>Quota total</strong></dt>
	<dd>Quota total de mémoire dans toutes les organisations.</dd>
	</dl>
	**Remarque** : les données sont actualisées automatiquement toutes les 4 heures. Cliquez sur **Recalculer** si vous voulez actualiser les données figurant sur la page avant qu'elles ne soient mises à jour automatiquement.

- Utilisation de la mémoire de l'organisation. Cette section détaille l'utilisation de la mémoire au niveau de l'organisation. Vous pouvez afficher le quota total de mémoire, le quota réservé et la mémoire physique utilisée par chaque organisation. Le graphique fournit des informations triées en fonction de la réservation de mémoire la plus élevée par organisation ; par défaut, l'organisation qui réserve la quantité de mémoire la plus élevée est répertoriée en premier. Vous pouvez effectuer un tri en fonction du paramètre **Utilisation de la mémoire la plus élevée** et du paramètre **Allocation de mémoire superflue**.

	<dl>
	<dt><strong>Utilisation de la mémoire la plus élevée</strong></dt>
	<dd>Utilisez cette option pour identifier l'organisation qui a réservé la quantité de mémoire la plus élevée. Effectuez un tri par utilisation de la mémoire la plus élevée pour identifier les organisations qui ont réservé la quantité de mémoire la plus élevée. La liste est triée par quota réservé. </dd>
	<dt><strong>Allocation de mémoire superflue</strong></dt>
	<dd>Utilisez cette option pour identifier les organisations dont le quota total de mémoire est supérieur aux besoins. Effectuez un tri par allocation de mémoire superflue pour identifier les organisations qui utilisent la quantité de mémoire la plus faible par rapport au quota qui leur a été alloué. </dd>
	</dl>

### Gestion des quotas
{: #manageorgquota}

Un quota représente les limites de ressources pour les organisations de votre environnement et est affecté lorsque l'organisation est créée. Toute application ou tout service dans un espace de l'organisation contribue à l'utilisation du quota alloué. Pour gérer le quota d'une organisation, procédez comme suit :

<ol>
<li>Cliquez dans le graphique sur la barre correspondant à l'organisation que vous voulez éditer dans la section Utilisation de la mémoire de l'organisation ou sélectionnez le nom de l'organisation dans la section Liste des organisations. Dans la page Informations sur l'organisation, vous pouvez renommer l'organisation et ajouter ou supprimer des responsables.
<p><strong>Remarque</strong> : vous recevez un message si vous sélectionnez un plan d'établissement des quotas qui n'est pas suffisant pour l'utilisation en cours pour l'organisation.</p></li>
<li>Cliquez sur <strong>Cloud Foundry</strong> ou sur <strong>Conteneurs</strong>.  Par défaut, la page du quota Cloud Foundry s'ouvre. 
<ul>
<li>A partir de la page Cloud Foundry, vous pouvez sélectionner un plan et afficher les détails du quota des ressources suivantes :
<ul>
<li>Services</li>
<li>Routes</li>
<li>Quota de mémoire</li>
<li>Allocation des applications</li>
</ul>
</li>
<li>Dans la page <strong>Conteneurs</strong>, vous pouvez affecter des valeurs entières aux zones suivantes :
<dl class="parml">
<dt class="pt dlterm">Limite d'image</dt>
<dd class="pd">Nombre maximal d'images de conteneur pouvant être contenues dans votre registre privé. Une image de conteneur est la base de chaque conteneur que vous créez. Une image est créée depuis un Dockerfile, lequel est un fichier en lecture seule contenant le système d'exploitation, l'application et toutes ses dépendances, et décrivant comment un conteneur est configuré. Les images sont partagées entre tous les membres d'une organisation.</dd>
<dt class="pt dlterm">Allocation de mémoire par défaut</dt>
<dd>Quantité de mémoire de conteneur automatiquement allouée à la création d'un nouvel espace. Lors de la création d'un conteneur, vous devez choisir une taille de conteneur. Cette taille détermine la quantité de mémoire que le conteneur peut utiliser sur l'hôte de calcul et est comptabilisée dans votre limite de mémoire de conteneur. </dd>
<dt class="pt dlterm">Allocation de mémoire maximale</dt>
<dd>Quantité maximale de mémoire de conteneur pouvant être allouée entre tous les espaces d'une organisation.</dd>
<dt class="pt dlterm">Adresses IP flottantes par défaut</dt>
<dd>Nombre d'adresses IP publiques automatiquement allouées à la création d'un nouvel espace. Vous pouvez lier des adresses IP publiques à des conteneurs isolées et des groupes de conteneurs afin de les rendre accessibles depuis Internet.</dd>
<dt class="pt dlterm">Adresses IP flottantes maximales</dt>
<dd>Nombre maximal d'adresses IP publiques pouvant être allouées entre tous les espaces d'une organisation.</dd>
</dl>
<strong>Remarque</strong> : si vous ne disposez pas encore de conteneurs dans votre environnement, ou si les conteneurs de votre environnement ne sont pas encore configurés, vous obtenez un message d'erreur.
<p>Pour plus d'informations sur les conteneurs, voir [A propos d'IBM containers](/docs/containers/container_ov.html). Pour plus d'informations sur les quotas de conteneur, voir [Quota et comptes Bluemix](/docs/containers/container_planning_org_ov.html#container_planning_quota).</p>
<strong>Remarque :</strong> Les conteneurs ne sont pas disponibles dans la région {{site.data.keyword.Bluemix_notm}} Sydney.</li>
</ul>
<li>Pour sauvegarder les modifications que vous avez apportées dans la page Gérer l'organisation, cliquez sur <strong>SAUVEGARDER</strong>.</li>
</ol>


### Gestion de vos organisations depuis la liste des organisations
{: #manageorgfrolis}

Dans la section Liste des organisations, vous pouvez afficher toutes les organisations de l'environnement {{site.data.keyword.Bluemix_notm}}, et vous pouvez effectuer des actions pour des organisations individuelles en cliquant sur le nom de l'organisation.

- Pour supprimer une organisation, cliquez sur l'icône **Supprimer** ![Supprimer](images/icon_trash.svg) dans la colonne Actions.
- Afin d'afficher le plan d'établissement des quotas et l'utilisation pour une organisation, cliquez sur le nom de l'organisation dans la liste. La page **Gérer les organisations** de l'organisation sélectionnée affiche les informations suivantes sur l'utilisation :

  - Le nombre de services utilisés
  - Le nombre de routes utilisées
  - Un graphique du quota de mémoire qui représente le quota utilisé et le quota non utilisé
  - Un graphique de l'allocation des applications qui indique quelles sont les applications incluses dans le quota de mémoire utilisé
  - Un graphique de l'utilisation des applications mesurée qui représente un rapport sur trois mois du nombre de Go/heure consommé par application déployée. Vous pouvez sélectionner la **vue Liste** pour examiner les données de toutes les applications, notamment l'allocation mémoire par application et l'utilisation mesurée en Go par heure au cours des trois derniers mois.

- Pour éditer le nom de l'organisation et ajouter ou retirer des responsables, cliquez sur le nom de l'organisation dans la liste et suivez les invites à l'écran.
- Pour afficher des informations sur un utilisateur particulier de l'organisation que vous visualiser, cliquez sur le nom d'utilisateur pour voir les Informations utilisateur. Vous pouvez ensuite cliquer sur le nom de l'organisation pour revenir aux Informations sur l'organisation. 

## Gestion des utilisateurs et des droits
{: #oc_useradmin}

Vous pouvez utiliser des utilisateurs individuels ou des groupes d'utilisateurs. En général, les utilisateurs sont ajoutés à votre instance {{site.data.keyword.Bluemix_notm}} depuis le registre d'utilisateurs de votre société via LDAP (Lightweight Directory Access Protocol). Vous pouvez aussi afficher les droits utilisateur. Si vous disposez du droit **Superutilisateur**, vous pouvez également définir et gérer les droits des autres utilisateurs. Cliquez sur **ADMINISTRATION &gt; ADMINISTRATION DES UTILISATEURS**.

La page Administration des utilisateurs affiche tous les utilisateurs pour l'instance locale ou dédiée. Les droits de chaque utilisateur sont affichés sous forme d'icônes dans le tableau. Les droits possibles sont les suivants : Aucun, **Superutilisateur**, **Accès de base**,**Connexion**, **Catalogue**, **Rapports** et **Utilisateurs**.
Les droits **Superutilisateur** et **Accès de base** peuvent être associés à la valeur **Activé** ou **Désactivé**, alors que les droits restants sont activés ou désactivés avec des types d'accès spécifiques, notamment **Lecture** ou **Ecriture**, représentés par des icônes. Voir [Droits](#permissions) pour la description de chaque type et l'explication des icônes.

### Gestion des utilisateurs
{: #workwithusers}

En fonction de l'accès **Lecture** ou **Ecriture** pour les droits des utilisateurs, vous pouvez rechercher des utilisateurs existants, retirer des utilisateurs et ajouter des utilisateurs individuellement ou via un groupe. Si vous possédez le droit **Superutilisateur**, vous disposez d'un accès complet vous permettant d'exécuter n'importe quelle tâche pour la gestion des utilisateurs dans l'environnement. Passez en revue les tâches de gestion des utilisateurs suivantes et le niveau d'accès requis pour accomplir chacune de ces tâches :

* Localisez les utilisateurs. Si vous disposez des accès **Lecture** ou **Ecriture** et que vous connaissez une partie ou la totalité du nom d'utilisateur, vous pouvez localiser des utilisateurs dans la table à l'aide de la zone **Rechercher**. Vous pouvez également filtrer la liste des utilisateurs en fonction de leur organisation et de leurs droits. Pour filtrer une liste d'utilisateurs, procédez comme suit :
  <ol>
  <li>Cliquez sur <strong>Filtrer</strong>.</li>
  <li> Cliquez sur <strong>Organisations</strong> ou <strong>Droits</strong>, selon le filtrage que vous voulez appliquer.
  <dl>
	<dt><strong>Organisation</strong></dt>
	<dd>Pour filtrer des utilisateurs par organisation, commencez à saisir le nom de l'organisation dans la zone <strong>Organisation</strong> et sélectionnez l'organisation dans la liste. Ensuite, sélectionnez le ou les rôles affectés aux utilisateurs dans l'organisation.</dd>
	<dt><strong>Droits</strong></dt>
	<dd>Pour filtrer les utilisateurs en fonction de leurs droits, sélectionnez d'abord le type d'utilisateur. Par exemple, vous pouvez choisir d'afficher tous les superutilisateurs. Pour les droits autres que <strong>Superutilisateur</strong> ou <strong>Accès de base</strong>, vous pouvez aussi sélectionner le type d'accès, par exemple <strong>Lecture</strong> ou <strong>Ecriture</strong>.</dd>
	</dl></li>
  <li>Cliquez sur <strong>Appliquer</strong>.</li>
   </ol>

   La fenêtre Administration des utilisateurs affiche les filtres que vous définissez et les utilisateurs qui sont trouvés avec les filtres spécifiés. Ensuite, vous pouvez rechercher un utilisateur dans la table filtrée. Vous pouvez aussi modifier la liste des filtres spécifiés en retirant une option de filtre de la liste.

* Ajoutez un seul utilisateur. Si vous disposez des droits **Superutilisateur** ou **Utilisateurs** avec un accès **Ecriture**, vous pouvez ajouter des utilisateurs.

  1. Pour ajouter un seul utilisateur depuis votre annuaire LDAP, cliquez sur **Ajouter un utilisateur**.
  2. Dans la zone **Rechercher**, entrez l'adresse électronique de l'utilisateur, puis sélectionnez l'utilisateur dans la liste.
  3. Ensuite, dans la zone **Organisation**, choisissez l'organisation à laquelle ajouter l'utilisateur en entrant le nom de l'organisation et en le sélectionnant dans la liste.
  4. Pour ajouter l'utilisateur à l'organisation sélectionnée, cliquez sur **Ajouter un utilisateur**.

  **Remarque** : lorsque l'opération d'ajout aboutit, l'utilisateur est ajouté au tableau pour que vous puissiez l'afficher et le rechercher. Lorsque des utilisateurs sont ajoutés, aucun droit ne leur est affecté.

* Ajoutez un groupe d'utilisateurs depuis votre annuaire LDAP. Si vous disposez des droits **Superutilisateur** ou **Utilisateurs** avec un accès **Ecriture**, vous pouvez ajouter des utilisateurs.

  1. Cliquez sur **Ajouter un groupe d'utilisateurs**.
  2. Dans la zone **Rechercher**, entrez un nom de groupe à rechercher, puis sélectionnez le nom de groupe dans la liste.
  3. Ensuite, dans la zone **Organisation**, choisissez l'organisation à laquelle ajouter le groupe d'utilisateurs en entrant le nom de l'organisation et en le sélectionnant dans la liste.
  4. Pour ajouter le groupe d'utilisateurs à l'organisation sélectionnée, cliquez sur **Ajouter des utilisateurs**.

  **Remarque** : les groupes de plus de 50 utilisateurs sont ajoutés via un travail par lots en arrière-plan. Lorsque l'opération d'ajout aboutit, l'utilisateur ou le groupe est ajouté au tableau pour que vous puissiez l'afficher et le rechercher. Lorsque des utilisateurs sont ajoutés, aucun droit ne leur est affecté.

* Ajoutez un groupe d'utilisateurs en important une feuille de calcul qui répertorie des ID utilisateur, des adresses électroniques d'utilisateur et l'organisation à laquelle vous voulez ajouter l'utilisateur. Si vous disposez des droits **Superutilisateur** ou **Utilisateurs** avec un accès **Ecriture**, vous pouvez ajouter des utilisateurs.

**Remarque** : entrez les ID utilisateur qui correspondent aux valeurs utilisées dans votre registre d'utilisateurs.

  1. Cliquez sur **Importer des utilisateurs**.
  2. Cliquez sur **Télécharger un modèle (.CSV)** pour télécharger une feuille de calcul avec les colonnes requises que vous pourrez remplir ou créez votre propre modèle en utilisant une feuille de calcul qui comporte les en-têtes de colonne requis : **ID utilisateur**, **Courrier électronique** et **Organisation**.  Deux colonnes facultatives sont également incluses dans le modèle : **Prénom** et **Nom**.
  3. Indiquez les valeurs d'utilisateur dans les colonnes requises. Si vous n'utilisez pas d'annuaire LDAP, utilisez les en-têtes de colonne requis et les en-têtes de colonne facultatifs pour les utilisateurs que vous importez.
  4. Sauvegardez votre fichier et cliquez sur **Envoyer le fichier par téléchargement**.

  **Remarque** : Les colonnes de votre feuille de calcul peuvent apparaître dans n'importe quel ordre tant que toutes les colonnes requises sont présentes. Si l'importation aboutit, vous recevez un message de confirmation indiquant que tous les utilisateurs ont été ajoutés. Si l'importation n'a abouti que pour certains utilisateurs, consultez le message d'erreur afin de prendre des mesures pour les utilisateurs qui n'ont pas pu être ajoutés.

* Retirez des utilisateurs. Si vous disposez du droit **Superutilisateur** ou du droit **Utilisateurs** avec l'accès **Ecriture**, vous pouvez retirer définitivement des utilisateurs de l'environnement.

    1. Localisez l'utilisateur et cliquez sur l'icône ![Supprimer](images/icon_trash.svg).
    2. Cliquez sur **Retirer**.

* Pour éditer les droits et les organisations des utilisateurs, vous devez disposer du droit **Superutilisateur**. Pour éditer les droits des utilisateurs, localisez ces derniers et cliquez sur leur nom. Dans la page **Edition d'utilisateur**, vous pouvez activer ou désactiver les droits :

    * Sélectionnez **Activé** dans la liste pour activer le droit **Superutilisateur** ou **Accès de base**.
    * Sélectionnez **Lecture** dans la liste pour que l'utilisateur dispose de l'accès **Lecture** (en lecture seule) pour ce droit ou sélectionnez **Ecriture** pour que l'utilisateur dispose de l'accès **Ecriture** (édition ou ajout et retrait) pour ce droit.
    * Sélectionnez **Désactivé** pour désactiver n'importe lequel des droits.

    **Remarque** : lorsque le droit **Superutilisateur** a pour valeur **Activé**, tous les autres droits sont définis avec l'accès **Ecriture**.

* Pour ajouter ou retirer un utilisateur dans une organisation spécifique, vous devez disposer du droit **Superutilisateur** ou du droit **Utilisateurs** avec l'accès **Ecriture**.

    1. Pour ajouter un utilisateur à une organisation, sélectionnez le nom de celui-ci dans le tableau pour accéder à la page **Edition d'utilisateur**. Ensuite, utilisez la zone de recherche pour localiser une organisation, sélectionnez celle-ci dans la liste, puis cliquez sur **Sauvegarder**.
    2. Pour retirer un utilisateur d'une organisation, sélectionnez le nom de l'utilisateur concerné dans le tableau afin d'accéder à la page **Edition d'utilisateur**. Ensuite, cliquez sur ![Retirer](images/icon_remove.svg) pour l'organisation dont vous souhaitez retirer l'utilisateur, puis cliquez sur **Sauvegarder**.
    
* Pour afficher les informations sur l'organisation à laquelle l'utilisateur est affecté, cliquez sur le nom de l'organisation pour afficher les Informations sur l'organisation. Vous pouvez ensuite cliquer sur le nom d'utilisateur pour revenir aux Informations utilisateur. 

### Droits
{: #permissions}

Les droits suivants peuvent être accordés aux utilisateurs avec des niveaux d'accès particuliers (lecture ou écriture) qui permettent à ces derniers d'exécuter des tâches spécifiques dans la console d'administration.


{: #ld_table14}

| **Droit d'utilisateur** | **Description** |       
|-----------------|-------------------|
| Superutilisateur | Les utilisateurs pour lesquels le droit **Superutilisateur** a pour valeur **Activé** sont autorisés à éditer des droits pour d'autres utilisateurs. Si le droit est activé, l'accès complet à tous les autres droits est automatiquement activé . En plus des tâches décrites dans ce tableau pour chaque droit, ces utilisateurs peuvent également configurer des abonnements à des notifications afin de recevoir directement des alertes relatives à des opérations de maintenance ou à des incidents, planifier des tâches de maintenance, exécuter des vérifications sur les composants de console et créer des organisations et des espaces pour l'environnement. Ce droit équivaut au rôle d'administrateur (admin) pour la console d'administration.  |
| Accès de base | Les utilisateurs pour lesquels le droit **Accès de base** a pour valeur **Activé** sont autorisés à afficher l'option de page d'administration dans l'interface utilisateur de {{site.data.keyword.Bluemix_notm}}. Les utilisateurs pour lesquels le droit est activé peuvent accéder aux vignettes [Informations système](#oc_system) et [Utilisation des ressources](#oc_resource). Sans ce droit, les utilisateurs ne peuvent pas voir l'option de menu d'administration ni y accéder. Ce droit équivaut au rôle d'administrateur (admin) pour la console d'administration. Il équivaut aussi au droit de connexion utilisé précédemment pour la console d'administration. |
| Catalogue | Les utilisateurs disposant du droit **Catalogue** peuvent lire (accès **Lecture** ou modifier (accès **Ecriture**) les services disponibles dans l'instance locale ou dédiée. L'accès en lecture permet à l'utilisateur d'accéder à la vignette Gestion du catalogue pour afficher les services disponibles. L'accès en écriture permet à l'utilisateur d'accéder à la vignette [Gestion du catalogue](#oc_catalog) pour afficher les services, éditer la visibilité des services, enregistrer des services personnalisés et contrôler la liste de priorité du pack de construction. |  
| Rapports | Les utilisateurs disposant du droit **Rapports** peuvent lire (accès **Lecture**) ou modifier (accès **Ecriture**) les rapports de sécurité. L'accès en lecture permet à l'utilisateur d'accéder à la vignette Rapports et journaux pour télécharger des rapports. L'accès en écriture permet à l'utilisateur d'afficher la vignette [Rapports et journaux](#oc_report) et d'utiliser l'interface de ligne de commande pour télécharger de nouveaux rapports et créer de nouvelles catégories auxquelles les utilisateurs pourront accéder. |
| Utilisateurs | Les utilisateurs disposant du droit **Utilisateurs** peuvent afficher (accès **Lecture**) la liste d'utilisateurs ou ajouter ou retirer des utilisateurs (accès **Ecriture**). Ce droit ne vous permet pas de définir des droits pour d'autres utilisateurs. L'accès en écriture permet à l'utilisateur d'ajouter de nouveaux utilisateurs à l'environnement, de supprimer des utilisateurs de l'environnement et d'ajouter des utilisateurs existants à des organisations qui existent déjà dans l'environnement. De plus, l'accès **Ecriture** permet à l'utilisateur d'ajouter de nouvelles organisations, de supprimer des organisations et d'éditer les utilisateurs des organisations. |
{: caption="Tableau 14. Droits" caption-side="top"}

## Utilisation d'API REST 
{: #auth_adminapi}

Pour utiliser les commandes d'API REST, vous devez d'abord vous authentifier. Pour générer et prendre en charge des sessions, vous pouvez utiliser des commandes cURL pour exécuter les tâches suivantes :

* [Connexion à la console d'administration](#auth_loginapi) 
* [Stockage de votre ID utilisateur et de votre mot de passe](#auth_setuidpw)
* [Stockage de cookies](#auth_apistorecook)
* [Réutilisation de cookies](#auth_apireusecook)

### Connexion à la console d'administration
{: #auth_loginapi}

Pour pouvoir exécuter des requêtes d'API `Admin`, vous devez vous connecter à la console d'administration. 

Pour vous connecter à la console d'administration, vous pouvez utiliser l'authentification d'accès de base sur le noeud final `https://console.<region>.bluemix.net/login`. Le serveur renvoie un cookie avec votre session. Vous utilisez ce cookie pour toutes les opérations avec la console d'administration.

**Remarque :** la session n'est plus valide si elle n'est pas utilisée pendant quelques heures.

Pour vous connecter à la console d'administration, exécutez la commande suivante :

`curl --user <user_id>:<password> -c ./cookies.txt --header "Accept: application/json" https://console.<region>.bluemix.net/login | python -m json.tool`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">--user <em>id_utilisateur</em>:<em>mot_de_passe</em></dt>
<dd class="pd">Accepte l'ID utilisateur et le mot de passe et envoie un en-tête d'autorisation de base.</dd>
<dt class="pt dlterm">-c <em>nom_fichier</em></dt>
<dd class="pd">Stocke l'ID utilisateur et le mot de passe spécifiés sous forme de cookie dans le fichier spécifié.</dd>
<dt class="pt dlterm">-b <em>nom_fichier</em></dt>
<dd class="pd">Extrait l'ID utilisateur et le mot de passe spécifiés sous forme de cookie dans le fichier spécifié.</dd>
<dt class="pt dlterm">--header</dt>
<dd class="pd">Envoie un en-tête Accept.</dd>
</dl>

Voici un exemple de sortie pour
cette commande :
```
{
    "message": "Logged in",
    "name": {
        "familyName": "*last_name*",
        "givenName": "*first_name*"
    }
}
```
{: screen}

### Stockage de votre ID utilisateur et de votre mot de passe
{: #auth_setuidpw}

Vous pouvez également stocker votre ID utilisateur et votre mot de passe de manière à ne pas avoir à les saisir manuellement chaque fois que vous vous connectez.  Pour stocker votre ID utilisateur et votre mot de passe afin de les réutiliser ultérieurement, utilisez l'exemple cURL suivant :

`curl -X GET -H "Authorization: Basic <redacted>" -H "Accept: application/json" "http://localhost:3000/login"`
{: codeblock}

Pour configurer vos informations de connexion dans un fichier distinct, puis appeler ce fichier de manière à ne pas avoir à le saisir à nouveau pour chaque demande d'authentification, utilisez l'option `--netrc` fournie par la commande cURL.

Pour utiliser l'option `--netrc` avec cURL, commencez par créer un fichier dans le répertoire de base de l'utilisateur en procédant de l'une des manières suivantes :
* Sur un système Unix, créez un fichier nommé .netrc 
* Sur un système Windows, créez un fichier nommé _netrc. 

Dans le fichier, entrez les informations suivantes :

`machine console.<region>.bluemix.net
login <id>
password <password>`
{: codeblock}

Lors de l'appel d'une commande cURL, ajoutez l'argument suivant : `--netrc`.
<p>Pour utiliser un fichier netrc situé dans un autre répertoire, utilisez l'option `--netrc-file [file]`, `[file]` correspondant à l'emplacement du fichier netrc.</p>
</li>
</ol>


### Stockage de cookies
{: #auth_apistorecook}

Lorsque vous vous connectez à la console d'administration, le serveur renvoie un cookie avec votre session. Ce cookie est requis dans le cadre du processus de connexion pour les futurs appels API relatifs à toutes les opérations liées à la console d'administration. Vous pouvez stocker des cookies afin de les utiliser ultérieurement.

Pour stocker des cookies après vous être connecté, utilisez l'option `-c`, comme illustré dans l'exemple CURL suivant :

`curl --user <user_id>:<password> -c ./cookies.txt --header "Accept: application/json" https://console.<region>.bluemix.net/login | python -m json.tool`
{: codeblock}

### Réutilisation de cookies
{: #auth_apireusecook}

Pour réutiliser des cookies, utilisez l'option `-b` avec le nom de fichier de cookie que vous avez affecté à l'aide de l'option `-c`, comme illustré dans l'exemple CURL suivant :

`curl --user <user_id>:<password> -b ./cookies.txt`
{: codeblock}

## Gestion des utilisateurs avec l'API REST Admin

{: #usingadminapi}

Vous pouvez utiliser l'API REST `Admin` afin d'ajouter et de retirer des utilisateurs pour votre instance {{site.data.keyword.Bluemix_notm}}.
Les noeuds finaux de l'API REST `Admin` et les réponses JSON sont fournis sur une base expérimentale afin de permettre des opérations de base depuis une ligne de commande. Les noeuds finaux et les adresses URL qui figurent dans les exemples de cette documentation peuvent changer ou être abandonnés dans un délai court.

Si vous disposez des droits **Superutilisateur** ou **Utilisateurs** avec un accès **Ecriture**, vous pouvez ajouter ou retirer des utilisateurs. Vous devez disposer du droit **Superutilisateur** pour éditer les droits des autres utilisateurs.

Bien que vous puissiez choisir d'utiliser d'autres outils, les outils suivants sont prérequis pour les exemples ci-après.
* cURL, pour entrer les demandes d'API REST sous forme de commandes. cURL est un utilitaire gratuit que vous pouvez utiliser pour envoyer des demandes HTTP à un serveur et recevoir les réponses du serveur via une interface de ligne de commande. Vous pouvez le télécharger depuis le [site de téléchargement cURL ![Icône de lien externe](../icons/launch-glyph.svg)](http://curl.haxx.se/download.html){: new_window}.
* Python, pour utiliser l'outil JSON de formatage de Python. Cet outil facultatif transforme le texte JSON en entrée en sortie facile à lire. Vous pouvez télécharger Python depuis le [site des téléchargements Python ![Icône de lien externe](../icons/launch-glyph.svg)](https://www.python.org/downloads){: new_window}.


### Liste des organisations
{: #listingorg}

Lorsque vous ajoutez un utilisateur, vous devez spécifier une organisation. Vous pouvez utiliser l'API REST `Admin` pour répertorier toutes les organisations. Vous devez disposer du droit **Utilisateurs** avec l'accès **Lecture** pour pouvoir répertorier les organisations. Pour répertorier toutes les organisations, exécutez la commande suivante :

`curl -b ./cookies.txt https://<votre_hôte>.ibm.com/codi/v1/organizations | python -m json.tool`
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">-b <em>nom_fichier</em></dt>
<dd class="pd">Transmet l'ID utilisateur et le mot de passe stockés précédemment avec l'option <samp class="ph codeph">-c</samp> dans le fichier sur le serveur HTTP sous forme de cookie.</dd>

</dl>

Pour chaque organisation, les résultats incluent les informations suivantes :
* `"guid"`, identificateur global unique de l'organisation
* `"name"`, nom de l'organisation

Voici un exemple de sortie pour
cette commande :
```
{
     "resources": [
         {
             "guid": "05af098d-d476-4fb0-8b87-a84350e72af3",
             "name": "org-1"
         },
         {
             "guid": "5129a5a8-37c2-4ee4-a9b2-bebae3531db5",
             "name": "org-2"
         },

		 		 ....

		 ],
		 "total_results": 284
}
```
{: screen}

### Liste des utilisateurs
{: #listingusr}

Vous pouvez déterminer si un utilisateur a déjà été ajouté à votre environnement {{site.data.keyword.Bluemix_notm}} en utilisant l'API REST `Admin` afin de répertorier les utilisateurs enregistrés. Vous devez disposer du droit **Utilisateurs** avec l'accès **Lecture** pour pouvoir répertorier les utilisateurs enregistrés. Pour répertorier tous les utilisateurs, exécutez la commande suivante :

`curl -b ./cookies.txt https://<votre_hôte>.ibm.com/codi/v1/users | python -m json.tool`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-b <em>nom_fichier</em></dt>
<dd class="pd">Transmet l'ID utilisateur et le mot de passe stockés précédemment avec l'option <samp class="ph codeph">-c</samp> dans le fichier sur le serveur HTTP sous forme de cookie.</dd>
</dl>

Pour chaque utilisateur enregistré, les résultats incluent les informations suivantes :
* `"first_name"` (prénom) et `"last_name"` (nom)
* `"user_id"`, ID utilisateur et adresse électronique
* `"guid"`, identificateur global unique de l'organisation.
* `"permissions"`, droits qui sont affectés à l'utilisateur pour la console d'administration.

Voici un exemple de sortie pour
cette commande :

```
{
    "next_url": "/codi/v1/users?results_per_page=100&amp;page=2",
    "prev_url": "",
    "resources": [
        {
            "active": true,
            "created_at": "2015-04-08T17:38:51.788Z",
            "created_by": "",
            "first_name": "un prénom",
            "guid": "5d5268cf-39c0-48d3-96ae-7afe928e5dd7",
            "last_name": "un nom",
            "permissions": [
                {
                    "display": "ops.admin"
                },
                {
                    "display": "ops.catalog.write"
                },
                {
                    "display": "ops.reports.write"
                },
                {
                    "display": "ops.catalog.read"
                },
                {
                    "display": "ops.users.write"
                },
                {
                    "display": "ops.reports.read"
                },
                {
                    "display": "ops.login"
                },
                {
                    "display": "ops.users.read"
                }
            ],
            "user_id": "un_id@us.ibm.com"
        },
		 		 ...


     }
    ],
    "total_pages": 395,
    "total_results": 39421
}

```
{: screen}

### Ajout d'un utilisateur

Vous pouvez utiliser l'API REST `Admin` pour ajouter des utilisateurs à l'instance {{site.data.keyword.Bluemix_notm}}. Vous devez disposer du droit **Utilisateurs** avec l'accès **Ecriture** pour pouvoir ajouter des utilisateurs ou du droit **Superutilisateur** (ops.admin) pour la console d'administration. De plus, en tant qu'administrateur, vous pouvez autoriser les membres d'organisation qui ne disposent pas des droits `Utilisateur` ou `Superutilisateur` à ajouter de nouveaux utilisateurs uniquement à leur organisation. Utilisez la commande d'API suivante pour cette fonction spécifique pour les responsables d'organisation :

```
PUT console.<sous-domaine>.bluemix.net/codi/env_config/allow_managers?flag=<TRUE ou FALSE>
```
{: screen}

Vous pouvez ajouter un utilisateur ou une liste d'utilisateurs. Vous pouvez ajouter des utilisateurs à une seule organisation ou à plusieurs organisations. Pour ajouter un utilisateur, vous devez fournir les informations suivantes :

* Prénom et nom de l'utilisateur. Indiquez les valeurs `"first_name"` et `"last_name"` figurant dans [Liste des utilisateurs](index.html#listingusr).
* Adresse électronique et ID utilisateur. Indiquez la valeur `"user_id"` figurant dans [Liste des utilisateurs](index.html#listingusr) pour l'adresse électronique et l'ID utilisateur.
* `"guid"`. Indiquez l'identificateur global unique de l'organisation figurant dans [Liste des organisations](index.html#listingorg).

Vous
fournissez les informations dans un fichier JSON.

`curl -b ./cookies.txt https://<votre_hôte>.ibm.com/codi/v1/users | python -m json.tool`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-b <em>nom_fichier</em></dt>
<dd class="pd">Transmet l'ID utilisateur et le mot de passe stockés précédemment avec l'option <samp class="ph codeph">-c</samp> dans le fichier sur le serveur HTTP sous forme de cookie.</dd>
</dl>

<ol>
<li>Créez un fichier JSON qui contient les informations dans un format JSON correct.
<p>Par exemple, créez un fichier appelé `user.json` dont le contenu est le suivant :</p>
<pre>
{
    "members": [
        {
            "emails": [
                "un_id_utilisateur@domaine.com"
            ],
            "first_name": "un_prénom",
            "last_name": "un_nom",
            "user_id": "un_id_utilisateur@domaine.com"
        }
    ],
    "organization_roles": [
        {
            "id": "7a891f9c-e4e7-46c7-8b4e-dffaa7eb3bcd"
        }
    ]
}
</pre>
</li>
<li>Publiez le contenu du fichier JSON sur le noeud final de l'utilisateur en exécutant la commande suivante :<br/><br/>
<code>
curl -v -b ./cookies.txt -X POST -H "Content-Type: application/json" -d @./user.json https://<your_host>.ibm.com/codi/v1/users
</code>
</li>
</ol>

<dl class="parml">
<dt class="pt dlterm">-v </dt>
<dd class="pd">Spécifie la sortie prolixe.</dd>
<dt class="pt dlterm">-X POST</dt>
<dd class="pd">Spécifie une demande POST, qui remplace la demande GET par défaut.</dd>
<dt class="pt dlterm">-H "Content-Type: application/json"</dt>
<dd class="pd">Spécifie l'en-tête content-type, qui dans ce cas est JSON.</dd>
<dt class="pt dlterm">-d *données*</dt>
<dd class="pd">Spécifie les données, dans ce cas le fichier `user.json`, à envoyer dans la demande POST au serveur HTTP.</dd>
</dl>

Voici un exemple de sortie pour
cette commande :

```
* Connected to localhost (127.0.0.1) port 3000 (#0)
 > POST /codi/v1/users HTTP/1.1
 > User-Agent: curl/7.37.1
 > Host: localhost:3000
 > Accept: */*
 > Cookie: opsConsole.sid=s%3AHLcwKGumyEb3IxREmikDOG3ATKD5xYMe.jfjWAa1tJC0rGghpeV8RPHqE2JaFVL4ZFIJbQpSC%2FAI
 > Content-Type: application/json
 > Content-Length: 333
 >
 * upload completely sent off: 333 out of 333 bytes
 < HTTP/1.1 201 Created
 < x-powered-by: Express
 < vary: X-HTTP-Method-Override
 < content-type: application/json
 < date: Wed, 22 Apr 2015 19:32:54 GMT
 < connection: close
 < transfer-encoding: chunked
 < X-Time_Check: Proxy Time: 5612 msec
 ```
{: screen}

### Retrait d'un utilisateur

Vous pouvez utiliser l'API REST `Admin` pour retirer des utilisateurs de l'instance {{site.data.keyword.Bluemix_notm}}. Vous devez disposer du droit **Utilisateurs** avec l'accès **Ecriture** pour pouvoir retirer des utilisateurs.

Pour retirer un utilisateur, vous devez fournir l'ID de l'utilisateur. Exécutez la commande suivante :

`curl -v -b ./cookies.txt -X DELETE
https://<votre_hôte>.ibm.com/codi/v1/users?user_id=<un_id_utilisateur@domaine.com>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-X DELETE</dt>
<dd class="pd">Spécifie une demande DELETE.</dd>
</dl>

Voici un exemple de sortie pour
cette commande :

```
 * connect to ::1 port 3000 failed: Connection refused
 *   Trying 127.0.0.1...
 * Connected to localhost (127.0.0.1) port 3000 (#0)
 > DELETE /codi/v1/users?user_id=exampleuser@domain.com HTTP/1.1
 > User-Agent: curl/7.37.1
 > Host: localhost:3000
 > Accept: */*
 > Cookie: opsConsole.sid=s%3AHLcwKGumyEb3IxREmikDOG3ATKD5xYMe.jfjWAa1tJC0rGghpeV8RPHqE2JaFVL4ZFIJbQpSC%2FAI
 >
 < HTTP/1.1 201 Created
 < x-powered-by: Express
 < content-type: application/json
 < date: Wed, 22 Apr 2015 21:01:09 GMT
 < connection: close
 < transfer-encoding: chunked
 < X-Time_Check: Proxy Time: 1922 msec
 <
 ```
{: screen}

## API pour les mesures (expérimental)
{: #envappmetricsapi}

Vous pouvez employer trois API expérimentales pour regrouper des mesures relatives à votre environnement ou à vos applications. Ces API renvoient un tableau de points de données des mesures demandées sur la durée indiquée.

Les API de mesures décrites dans les sections suivantes sont accessibles à partir du noeud final spécifique de la région, par exemple : 

`https://console.<région>.bluemix.net/admin/metrics`
{: codeblock}

**Remarques** :

1. Un utilisateur peut effectuer jusqu'à 200 demandes d'API de mesures par heure.
2. Chaque demande d'API renvoie jusqu'à 200 points de données par demande. Si des données supplémentaires sont disponibles, une URL est fournie en réponse au chargement de l'ensemble de données suivant.
3. Chaque demande d'API nécessite qu'un utilisateur dispose au moins des droits d'accès de base à la console d'administration.  Des droits supplémentaires peuvent être nécessaires, comme indiqué ci-dessous.

## Regroupement des mesures relatives à votre environnement 

Vous pouvez utiliser l'API d'environnement expérimentale pour regrouper des informations de niveau supérieur relatives à votre environnement sur une période que vous définissez. Les points de données disponibles sur la durée indiquée sont renvoyés. Les données sont enregistrées environ toutes les heures. SI, par exemple, vous avez demandé six heures de données relatives à l'unité centrale de votre environnement, la réponse inclut les données relatives à l'unité centrale pour chacune des six heures demandées.


### Noeuds finaux d'environnement 

Vous pouvez utiliser le noeud final suivant pour appeler cette commande d'API : `/api/v1/env`

**Remarque** : l'un des droits suivants sont nécessaires pour accéder à ces noeuds finaux : **Accès de base**, **Accès en lecture de l'utilisateur**, **Accès en écriture de l'utilisateur** ou **Superutilisateur**

### Paramètres de requête des mesures relatives à l'environnement

Les paramètres de requête suivants permettent de regrouper les mesures relatives à l'unité centrale, le disque, la mémoire, le réseau, le quota et les applications :

<dl class="parml">
<dt class="pt dlterm">metric</dt>
<dd class="pd">Une ou plusieurs des valeurs suivantes séparées par une virgule : `memory`, `disk`, `cpu`, `network`, `quota` et `apps`.</dd>
<dt class="pt dlterm">startTime</dt>
<dd class="pd">Point le plus ancien dans le temps à partir duquel les données sont renvoyées. Si aucun paramètre startTime n'est indiqué, le point de données disponible le plus récent est inclus. Par exemple, pour regrouper les données situées entre 14h et 17h, indiquez la valeur correspondant à 14h pour startTime.</dd>
<dt class="pt dlterm">endTime</dt>
<dd class="pd">Point le plus récent dans le temps à partir duquel les données sont renvoyées. Si aucun paramètre endTime n'est indiqué, le point de données le plus récent est utilisé. Par exemple, pour regrouper les données situées entre 14h et 17h, indiquez la valeur correspondant à 17h pour endTime.</dd>
<dt class="pt dlterm">sort</dt>
<dd class="pd">Ordre dans lequel les données sont renvoyées. Les valeurs valides sont `asc` (croissant) et `desc` (décroissant). La valeur par défaut est l'ordre décroissant qui renvoie d'abord les données les plus récentes. </dd>
</dl>

L'exemple suivant utilise les paramètres de requête pour regrouper des mesures sur votre environnement :

```
curl -b ./cookies.txt --header "Accept: application/json" https://console.<région>.bluemix.net/admin/metrics/api/v1/env?metric=cpu,network,disk,apps,memory
```
{: codeblock}


### Format des données de mesure relatives à l'environnement

Les sections suivantes indiquent le format des données.

 * Pour regrouper les enregistrements de données concernant l'utilisation de la mémoire, employez le format de données suivant :
 
```
{
  "sample_time": 1477494000000,
  "memory": {
    "total": {
      "physical": {
        "total_gb": 1728,
        "used": {
          "value_gb": 673.68,
          "percent": 38.99
        }
      },
    "allocated": {
        "reserved_gb": 3456,
        "total_allocated": {
          "value_gb": 2575.18,
          "percent": 74.51
        }
      },
    },
  	"cell": {
      "physical": {
        "total_gb": 864,
      "used": {
          "value_gb": 336.84,
        "percent": 38.99
      }
      },
    "allocated": {
        "reserved_gb": 1728,
      "total_allocated": {
          "value_gb": 1287.59,
        "percent": 74.51
      }
      },
    },
    "dea": {
      "physical": {
      	"total_gb": 864,
      "used": {
          "value_gb": 336.84,
        "percent": 38.99
      }
      },
    "allocated": {
        "reserved_gb": 1728,
      "total_allocated": {
          "value_gb": 1287.59,
        "percent": 74.51
      }
      },
    },
    "memory_by_container": [
      {
        "name": "dea_next/0",
        "type": "dea",
        "ip": "169.53.225.93",
        "percent": "47"
      },
      {
        "name": "dea_next/1",
        "type": "dea",
        "ip": "169.53.225.89",
        "percent": "51"
      },
      {
        "name": "dea_next/2",
        "type": "dea",
        "ip": "169.53.230.49",
        "percent": "45"
      },
      {
        "name": "dea_next/3",
        "type": "dea",
        "ip": "169.44.109.231",
        "percent": "43"
      }
    ]
  }
}
```
{: screen}

 * Pour regrouper les enregistrements de données concernant l'utilisation du disque, employez le format de données suivant :
 
```
{
  "sample_time": 1477494000000,
  "disk": {
    "total": {
      "physical": {
        "total_gb": 16200,
        "used": {
          "value_gb": 1614,
          "percent": 9.96
        }
      },
    "allocated": {
        "reserved_gb": 32400,
        "total_allocated": {
          "value_gb": 3979,
          "percent": 12.28
        }
      },
    },
    "cell": {
      "physical": {
        "total_gb": 8100,
      "used": {
          "value_gb": 807,
        "percent": 9.96
      }
      },
    "allocated": {
        "reserved_gb": 16200,
      "total_allocated": {
          "value_gb": 1989.5,
        "percent": 12.28
      }
      },
    },
    "dea": {
      "physical": {
        "total_gb": 8100,
      "used": {
          "value_gb": 807,
        "percent": 9.96
      }
      },
    "allocated": {
        "reserved_gb": 16200,
      "total_allocated": {
          "value_gb": 1989.5,
        "percent": 12.28
      }
      },
    },
    "disk_by_container": [
      {
        "name": "dea_next/0",
        "type": "dea",
        "ip": "169.53.225.93",
        "percent": "13"
      },
      {
        "name": "dea_next/1",
        "type": "dea",
        "ip": "169.53.225.89",
        "percent": "14"
      },
      {
        "name": "dea_next/2",
        "type": "dea",
        "ip": "169.53.230.49",
        "percent": "13"
      },
      {
        "name": "dea_next/3",
        "type": "dea",
        "ip": "169.44.109.231",
        "percent": "12"
      }
    ]
  }
}
```
{: screen}

 * Pour regrouper les enregistrements de données concernant l'utilisation de l'unité centrale, employez le format de données suivant :
 
```
{
  "sample_time": 1477494000000,
  "cpu": {
    "total": {
      "average_percent_cpu_used": 14.725
    },
    "cell": {
      "average_percent_cpu_used": 19
    },
    "dea": {
      "average_percent_cpu_used": 10.45
    },
    "cpu_by_container": [
      {
        "name": "dea_next/0",
        "type": "dea",
        "ip": "169.53.225.93",
        "sys_percent": "8.4",
        "user_percent": "2.7",
        "wait_percent": "0.0"
      },
      {
        "name": "dea_next/1",
        "type": "dea",
        "ip": "169.53.225.89",
        "sys_percent": "7.4",
        "user_percent": "2.4",
        "wait_percent": "0.0"
      },
      {
        "name": "cell/1",
        "type": "cell",
        "ip": "169.53.230.49",
        "sys_percent": "5.3",
        "user_percent": "1.9",
        "wait_percent": "0.0"
      },
      {
        "name": "cell/2",
        "type": "cell",
        "ip": "169.44.109.231",
        "sys_percent": "8.2",
        "user_percent": "22.6",
        "wait_percent": "0.0"
      }
    ]
  }
}
```
{: screen}

 * Pour regrouper les enregistrements de données concernant votre réseau, employez le format de données suivant :
 
```
{
  "sample_time": 1477494000000,
  "network": {
    "datapower": {
    "response_times": [
      {
        "proxy": "custom_certificates",
        "ten_seconds_ms": "0",
        "one_minute_ms": "0",
        "ten_minutes_ms": "0",
        "one_hour_ms": "0",
        "one_day_ms": "0"
      },
      {
        "proxy": "bluemix",
        "ten_seconds_ms": "90",
        "one_minute_ms": "89",
        "ten_minutes_ms": "83",
        "one_hour_ms": "85",
        "one_day_ms": "95"
      }
      ],
        "transactions": [
      {
        "proxy": "custom_domains",
        "ten_seconds_ms": "0",
        "one_minute_ms": "0",
        "ten_minutes_ms": "0",
        "one_hour_ms": "0",
        "one_day_ms": "0"
      },
      {
        "proxy": "bluemix",
        "ten_seconds_ms": "697",
        "one_minute_ms": "747",
        "ten_minutes_ms": "802",
        "one_hour_ms": "794",
        "one_day_ms": "730"
      }
      ],
        "bandwidth": {
        "in_kbps": 10855,
        "out_kbps": 38090
      }
  }
}
```
{: screen}

* Pour regrouper les enregistrements de données concernant l'utilisation de quota, employez le format de données suivant :
 
```
{
  "sample_time": 1477494000000,
  "quota": {
    "reserved_memory": {
      "total_bytes": 33176474877952
    },
    "services": {
      "total": 111650
    },
    "routes": {
      "total": 1675000
    }
  }
}
```
{: screen}

* Pour regrouper les enregistrements de données concernant vos applications, employez le format de données suivant :
 
```
{
  "sample_time": 1477494000000,
  "apps": {
    "count": 1406,
    "allocation": {
      "memory_gb": 571.8,
      "disk_gb": 1204
    }
  }
}
```
{: screen}

### Format de réponse des mesures relatives à l'environnement

```
{
   docs: [],
   next_url:
}
```
{: screen}

## Regroupement des mesures relatives à vos organisations

Des données sont enregistrées pour toutes les organisations environ toutes les heures. Une demande de mesure particulière renvoie ces informations pour toutes les organisations de chaque échantillon de données de la période indiquée, dans l'ordre décroissant de la mesure demandée. Par exemple, si vous demandez la mesure relative à la mémoire de toutes les organisations sur une période de six heures dans un environnement comportant 200 applications, 1200 enregistrements sont renvoyés : 200 par heure.

Pour réduire la quantité d'informations renvoyées pour chaque échantillon de données sur la période demandée, vous pouvez indiquer une option count. Si vous ajoutez l'option count avec une valeur égale à 5, l'exemple précédent renvoie 30 enregistrements, qui représentent les 5 organisations les plus importantes par mémoire de chaque échantillon de données.

### Noeuds finaux relatifs aux organisations 

Vous pouvez utiliser les noeuds finaux suivants pour appeler cette commande d'API :
* `/api/v1/org/memory/physical`
* `/api/v1/org/memory/reserved`
* `/api/v1/org/disk/physical`
* `/api/v1/org/disk/reserved`

**Remarque** : l'un des droits suivants sont nécessaires pour accéder à ces noeuds finaux : **Accès en lecture de l'utilisateur**, **Accès en écriture de l'utilisateur** ou **Superutilisateur**

### Paramètres de requête relatifs aux organisations
 
Utilisez les paramètres de requête suivants pour regrouper des mesures concernant vos organisations :

<dl class="parml">
<dt class="pt dlterm">startTime</dt>
<dd class="pd">Point le plus ancien dans le temps à partir duquel les données sont renvoyées. Si aucun paramètre startTime n'est indiqué, le point de données disponible le plus récent est inclus. Par exemple, pour regrouper les données situées entre 14h et 17h, indiquez la valeur correspondant à 14h pour startTime.</dd>
<dt class="pt dlterm">endTime</dt>
<dd class="pd">Point le plus récent dans le temps à partir duquel les données sont renvoyées. Si aucun paramètre endTime n'est indiqué, le point de données le plus récent est utilisé. Par exemple, pour regrouper les données situées entre 14h et 17h, indiquez la valeur correspondant à 17h pour endTime.</dd>
<dt class="pt dlterm">count</dt>
<dd class="pd">Nombre d'enregistrements à renvoyer pour chaque échantillon de données.
</dd>
<dt class="pt dlterm">minValue</dt>
<dd class="pd">Valeur la plus petite à renvoyer pour la mesure indiquée.  Si aucune valeur n'est indiquée, toutes les valeurs sont renvoyées.  Par exemple, pour regrouper les organisations qui utilisent au moins 20000 octets de mémoire physique, spécifiez une valeur de minValue égale à 20000.
</dd>
</dl>

L'exemple suivant regroupe les mesures concernant vos organisations :

```
curl -b ./cookies.txt --header "Accept: application/json" https://console.<region>.bluemix.net/admin/metrics/api/v1/org/memory/physical?count=5&startTime=2016-12-02T16:54:09.467Z
```
{: codeblock}

### Format de réponse relatif aux organisations

```
{
   docs: [],
   next_url:
}
```
{: screen}

Chaque document renvoyé représente les mesures demandées pour une organisation de chaque échantillon de données, au moment de la demande.

## Regroupement des mesures relatives à vos applications

Les données sont enregistrées pour toutes les applications environ toutes les heures. Une demande de mesure particulière renvoie ces informations pour toutes les applications de chaque échantillon de données de la période indiquée, dans l'ordre décroissant de la mesure demandée. Par exemple, si vous demander la mesure relative à l'unité centrale de toutes les applications sur une période de six heures dans un environnement comportant 200 applications, 1200 enregistrements sont renvoyés : 200 par heure.

Pour réduire la quantité d'informations renvoyées pour chaque échantillon de données sur la période demandée, vous pouvez indiquer une option count. Si vous ajoutez l'option count avec une valeur égale à 5, l'exemple précédent renvoie 30 enregistrements, qui représentent les 5 applications les plus importantes par unité centrale de chaque échantillon de données.

### Noeuds finaux des applications 

Vous pouvez utiliser les noeuds finaux suivants pour appeler cette commande d'API :
* `/api/v1/app/cpu/physical` 
* `/api/v1/app/memory/physical`
* `/api/v1/app/memory/reserved`
* `/api/v1/app/disk/physical`
* `/api/v1/app/disk/reserved`

**Remarque** : l'un des droits suivants sont nécessaires pour accéder à ces noeuds finaux : **Accès en lecture de l'utilisateur**, **Accès en écriture de l'utilisateur** ou **Superutilisateur**

### Paramètres de requête relatifs aux applications
 
Utilisez les paramètres de requête suivants pour regrouper des mesures concernant vos applications :

<dl class="parml">
<dt class="pt dlterm">startTime</dt>
<dd class="pd">Point le plus ancien dans le temps à partir duquel les données sont renvoyées. Si aucun paramètre startTime n'est indiqué, le point de données disponible le plus récent est inclus. Par exemple, pour regrouper les données situées entre 14h et 17h, indiquez la valeur correspondant à 14h pour startTime.</dd>
<dt class="pt dlterm">endTime</dt>
<dd class="pd">Point le plus récent dans le temps à partir duquel les données sont renvoyées. Si aucun paramètre endTime n'est indiqué, le point de données le plus récent est utilisé. Par exemple, pour regrouper les données situées entre 14h et 17h, indiquez la valeur correspondant à 17h pour endTime.</dd>
<dt class="pt dlterm">count</dt>
<dd class="pd">Nombre d'enregistrements à renvoyer pour chaque échantillon de données.
</dd>
<dt class="pt dlterm">minValue</dt>
<dd class="pd">Valeur la plus petite à renvoyer pour la mesure indiquée. Si aucune valeur n'est indiquée, toutes les valeurs sont renvoyées. Par exemple, pour regrouper les applications qui utilisent au moins 20000 octets de mémoire physique, spécifiez une valeur de minValue égale à 20000.
</dd>
</dl>

L'exemple suivant regroupe les mesures concernant vos applications :

```
curl -b ./cookies.txt --header "Accept: application/json" https://console.<région>.bluemix.net/admin/metrics/api/v1/app/cpu/physical?count=5&startTime=2016-12-02T16:54:09.467Z
```
{: codeblock}


### Format de réponse pour les applications

```
{
   docs: [],
   next_url:
}
```
{: screen}

Chaque document renvoyé représente les mesures demandées pour une application de chaque échantillon de données, au moment de la demande.


## API de service personnalisée
{: #servicebrokerapi}

Vous pouvez utiliser trois API pour enregistrer ou créer un service, mettre à jour un service et supprimer un service.

Toutes les API sont relatives à <code>https://console.&lt;sous-domaine&gt;.bluemix.net/</code>.

<dl>
<dt><strong>&lt;sous-domaine&gt;</strong></dt>
<dd>Cette valeur est le nom de votre instance locale ou dédiée. Le nom de sous-domaine pour votre instance {{site.data.keyword.Bluemix}} a été affecté au cours du processus
d'intégration.</dd>
</dl>

## Enregistrement d'un nouveau service

Utilisez l'API et les exemples de code suivants pour enregistrer un nouveau service.

### Route
{: #registerroute}

```
POST /codi/v1/serviceBrokers
```
{: screen}

### Demande
{: #registerrequest}

{: #ld_table15}

| **Nom ** | **Description** |
|-----------------|-------------------|
| name | Nom du courtier de services. |
| auth_username | Nom d'utilisateur utilisé pour se connecter au courtier de services. |
| auth_password | Mot de passe utilisé pour se connecter au courtier de services. |
| broker_url | URL utilisée pour se connecter au courtier de services. |
| owningOrganization | Organisation initiale avec laquelle enregistrer le service sur la liste blanche. |
{: caption="Tableau 15. Zones" caption-side="top"}

#### Corps
{: #registerbody}

```
{
  "name" : "Nom du courtier de services",
  "auth_username" : "nom d'utilisateur",
  "auth_password" : "mot de passe",
  "broker_url" : "https://broker.comp.com",
  "owningOrganization" : "ORG"
}
```
{: screen}

#### En-têtes
{: #registerheaders}

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

### Réponse
{: #registerresponse}

#### Statut
{: #registerstatus}

```
201 Created
```
{: screen}

#### Corps
{: #registerbody2}

```
{
    "_id": "2063580064-0ca80769-8e9e-4e1c-9b99-68bdcf1a2c68",
    "name": "Nom du courtier de services",
    "broker_url": "https://provision-broker.comp.bluemix.net/bmx/provisioning/brokers/2063580064-8f23230c-7f36-4ce5-a298-2ab4108f1120",
    "proxy_broker_url": "https://provision-broker.dys0.bluemix.net/bmx/provisioning/brokers/2063580064-0ca80769-8e9e-4e1c-9b99-68bdcf1a2c68",
    "auth_username": "nom d'utilisateur",
    "created_on": "2016-09-30T16:45:56.304Z"
}

```
{: screen}

## Mise à jour d'un service

Utilisez l'API et les exemples de code suivants pour mettre à jour un service.

### Route
{: #updateroute}

`PUT /codi/v1/serviceBrokers`
{: screen}

### Demande
{: #updaterequest}

{: #ld_table16}

| **Nom ** | **Description** |
|-----------------|-------------------|
| name | Nom du courtier de services. Ce nom ne peut pas varier du nom avec lequel a été créé le service. |
| auth_username | Nom d'utilisateur utilisé pour se connecter au courtier de services. |
| auth_password | Mot de passe utilisé pour se connecter au courtier de services. |
| broker_url | URL utilisée pour se connecter au courtier de services. |
| owningOrganization | Organisation initiale avec laquelle enregistrer le service sur la liste blanche. |
{: caption="Tableau 16. Demandes" caption-side="top"}

#### Corps
{: #updatebody}

```
{
  "name" : "Nom du courtier de services",
  "auth_username" : "nom d'utilisateur",
  "auth_password" : "nouveau mot de passe",
  "broker_url" : "https://broker.comp.com",
  "owningOrganization" : "ORG"
}
```
{: screen}

#### En-têtes
{: #updateheaders}

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

### Réponse
{: #updateresponse}

#### Statut
{: #updatestatus}

```
201 Created
```
{: screen}

#### Corps
{: #updatebody2}

```
{
    "_id": "2063580064-0ca80769-8e9e-4e1c-9b99-68bdcf1a2c68",
    "name": "Nom du courtier de services",
    "broker_url": "https://provision-broker.dys0.bluemix.net/bmx/provisioning/brokers/2063580064-d11bdd84-7556-469f-858d-2098b531f7f2",
    "proxy_broker_url": "https://provision-broker.dys0.bluemix.net/bmx/provisioning/brokers/2063580064-0ca80769-8e9e-4e1c-9b99-68bdcf1a2c68",
    "auth_username": "nom d'utilisateur",
    "created_on": "2016-09-30T16:45:56.304Z"
}
```
{: screen}

## Suppression d'un service

Utilisez l'API et les exemples de code suivants pour supprimer un service.


{: #ld_table17}

| **Nom ** | **Description** |
|-----------------|-------------------|
| name | Nom du courtier de services. Ce nom ne peut pas varier du nom avec lequel a été créé le service. |
{: caption="Tableau 17. Paramètre" caption-side="top"}

### Route

```
DELETE /codi/v1/serviceBrokers?name=nom du courtier de services
```
{: screen}

### Demande
{: #deleterequest}

#### En-têtes
{: #deleteheaders}

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

### Réponse
{: #deleteresponse}

#### Statut
{: #deletestatus}

```
204 No Content
```
{: screen}

### Gestion des utilisateurs avec l'interface de ligne de commande cf
{: #usingadmincli}

Vous pouvez gérer les utilisateurs pour votre environnement {{site.data.keyword.Bluemix_notm}} via l'interface de ligne de commande Cloud Foundry, avec le plug-in d'interface de ligne de commande d'administration {{site.data.keyword.Bluemix_notm}}. Vous devez télécharger ce plug-in pour votre interface de ligne de commande Cloud Foundry.

Avant de commencer, installez l'interface de ligne de commande cf. Le plug-in d'interface de ligne de commande d'administration {{site.data.keyword.Bluemix_notm}} requiert cf version 6.11.2 ou ultérieure. [Télécharger l'interface de ligne de commande Cloud Foundry ![Icône de lien externe](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window}.

**Restriction :** l'interface de ligne de commande Cloud Foundry n'est pas prise en charge par Cygwin. Utilisez-la dans une fenêtre de ligne de commande autre que Cygwin.

#### Ajout du plug-in d'interface de ligne de commande d'administration {{site.data.keyword.Bluemix_notm}}

Une fois l'interface de ligne de commande cf installée, vous pouvez ajouter le plug-in d'interface de ligne de commande d'administration {{site.data.keyword.Bluemix_notm}}.

**Remarque** : si vous avez déjà installé le plug-in d'administration {{site.data.keyword.Bluemix_notm}}, il peut être nécessaire de le désinstaller, de supprimer le référentiel, puis de réinstaller le plug-in afin de bénéficier des mises à jour les plus récentes.

Procédez comme suit pour ajouter le référentiel et installer le plug-in :

<ol>
<li>Pour ajouter le plug-in d'administration {{site.data.keyword.Bluemix_notm}}, exécutez la commande suivante :<br/><br/>
<code>
cf add-plugin-repo BluemixAdmin https://console.&lt;subdomain&gt;.bluemix.net/cli
</code><br/><br/>
<dl class="parml">
<dt class="pt dlterm">&lt;sous-domaine&gt;</dt>
<dd class="pd">Sous-domaine de l'adresse URL pour votre instance {{site.data.keyword.Bluemix_notm}}.</dd>
</dl>
</li>
<li>Pour installer le plug-in de l'interface de ligne de commande d'administration {{site.data.keyword.Bluemix_notm}}, exécutez la commande suivante :<br/><br/>
<code>
cf install-plugin bluemix-admin-cli -r BluemixAdmin
</code>
</li>
</ol>

Pour afficher la liste des sous-commandes disponibles à partir des plug-ins que vous avez installés, exécutez la commande suivante :

```
cf plugins
```
{: codeblock}

Pour afficher la liste des groupes de commandes disponibles pour le plug-in d'administration {{site.data.keyword.Bluemix_notm}}, exécutez la commande suivante :

```
cf ba
```
{: codeblock}

Pour obtenir de l'aide supplémentaire sur une commande, utilisez l'option `-help`.

Pour plus d'informations sur l'utilisation du plug-in d'interface de ligne de commande d'administration {{site.data.keyword.Bluemix_notm}}, voir [Administration {{site.data.keyword.Bluemix_notm}}](../cli/plugins/bluemix_admin/index.html).
