{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

#Administration de {{site.data.keyword.Bluemix_notm}}
{: #administer}
*Dernière mise à jour : 20 janvier 2016*

Gérez vos organisations, vos espaces et les utilisateurs affectés en cliquant sur l'icône **Compte et support** ![Compte et support](../support/images/account_support.svg), puis sélectionnez **Gérer les organisations**. Si vous êtes utilisateur d'un environnement {{site.data.keyword.Bluemix_notm}} local ou d'un environnement
{{site.data.keyword.Bluemix_notm}} dédié, voir [Gestion de l'environnement {{site.data.keyword.Bluemix_notm}}
local et de l'environnement {{site.data.keyword.Bluemix_notm}} dédié](index.html#mng) pour plus d'informations sur l'administration de votre instance locale
ou dédiée.
{:shortdesc}

##Gestion de votre compte
{: #mngacct}

Dans {{site.data.keyword.Bluemix}} Public, vous pouvez gérer l'ensemble des organisations et des espaces, y compris l'accès utilisateur à partir du tableau de bord figurant dans l'interface utilisateur. Vous pouvez également surveiller votre utilisation et votre facturation.
{:shortdesc}

###Organisations et espaces
{: #orgsandspaces}

En tant que responsable de l'organisation ou propriétaire de compte, vous pouvez utiliser la page Gérer les organisations pour afficher et gérer les
paramètres de l'organisation ou de l'espace, notamment l'accès utilisateur. Pour ouvrir la page Gérer les organisations, cliquez sur l'icône **Compte et support** ![Compte et support](../support/images/account_support.svg), puis sélectionnez **Gérer les organisations**.

####Organisations

Une organisation est définie par les éléments suivants :

<dl>
<dt>Les utilisateurs</dt>
<dd>Rôle disposant du droit de base dans les organisations et les espaces. Vous devez être affecté à une organisation pour pouvoir obtenir d'autres
droits dans les espaces de l'organisation. Pour des informations détaillées, voir
[Utilisateurs et rôles](index.html#userroles).</dd>
<dt>Les domaines</dt>
<dd>Indiquez la route Internet allouée à l'organisation. Une route possède un sous-domaine et un domaine. En général, le sous-domaine est le nom de l'application. Le
domaine peut être un domaine système ou un domaine personnalisé que vous avez enregistré pour votre application.<br/>
<p>**Remarque** : si vous ajoutez un domaine personnalisé, vous devez configurer votre serveur DNS afin de résoudre votre domaine
personnalisé de sorte qu'il désigne le domaine système {{site.data.keyword.Bluemix_notm}}. Ainsi, lorsque
{{site.data.keyword.Bluemix_notm}} reçoit une demande pour votre domaine personnalisé, il peut l'acheminer correctement vers votre
application.</p></dd>
<dt>Le quota</dt>
<dd>Représente les limites des ressources pour l'organisation, notamment le nombre de services et la quantité de mémoire pouvant être alloués à
l'organisation. Les quotas sont affectés lorsque les organisations sont
créées. Toute application ou tout service dans un espace de l'organisation contribue à l'utilisation du quota. Avec les plans Paiement à la carte ou
Abonnement, vous pouvez ajuster votre quota pour les applications et les conteneurs Cloud Foundry au fur et à mesure que les besoins de votre organisation
changent.</dd>
</dl>

Dans {{site.data.keyword.Bluemix_notm}}, vous pouvez utiliser des organisations afin de permettre la collaboration entre les utilisateurs et
de faciliter le regroupement logique des ressources de projet comme suit :

<ul>
<li>Vous pouvez regrouper un ensemble d'espaces, d'applications, de services, de domaines, de routes et d'utilisateurs dans des organisations.</li>
<li>Vous pouvez gérer l'accès aux espaces et aux organisations pour chaque utilisateur.</li>
</ul>

Lorsque vous créez une organisation, le nom de l'organisation doit être unique dans {{site.data.keyword.Bluemix_notm}}. Une fois que vous
avez créé
l'organisation, le droit *Responsable de l'organisation*, qui vous permet d'éditer le nom de l'organisation, de supprimer l'organisation et de
créer des espaces dans l'organisation vous est attribué automatiquement.

Lorsque vous supprimez une organisation, tous les espaces, toutes les applications et tous les services dans l'organisation sont supprimés.

{{site.data.keyword.Bluemix_notm}} permet la collaboration dans les projets en affectant des utilisateurs dans une organisation et dans les
espaces de l'organisation. Vous pouvez vous servir de l'onglet **Utilisateurs** pour afficher et gérer les utilisateurs de
l'organisation. Vous pouvez aussi inviter des utilisateurs dans votre organisation en cliquant sur le lien **Inviter un nouvel utilisateur** dans
l'onglet **Utilisateurs**. Les droits suivants peuvent être attribués aux utilisateurs d'une organisation :

<ul>
<li>Utilisateur de l'organisation</li>
<li>Responsable de l'organisation</li>
<li>Responsable de la facturation de l'organisation</li>
<li>Auditeur de l'organisation</li>
</ul>

####Espaces

Dans une organisation, vous pouvez utiliser des espaces pour regrouper un ensemble d'applications, de services et d'utilisateurs.

Une fois que vous avez ajouté des utilisateurs à une organisation, vous pouvez leur attribuer des droits pour les espaces dans l'organisation. A
l'instar des organisations, les espaces possèdent également un ensemble de droits pouvant être attribués aux utilisateurs :

<ul>
<li>Responsable de l'espace</li>
<li>Développeur de l'espace</li>
<li>Auditeur de l'espace</li>
</ul>

**Remarque** : un utilisateur doit disposer d'au moins l'un des droits dans l'espace.

L'onglet **Domaines** d'un espace est une liste en lecture seule des domaines qui sont affectés à l'espace. Le domaine de système est
toujours disponible dans un espace, et des domaines personnalisés peuvent également être alloués à l'espace. Les applications qui ont été créées
dans l'espace peuvent utiliser n'importe quel domaine répertorié pour l'espace.

###Utilisateurs et rôles
{: #userroles}

Les propriétaires de compte effectuent toutes les opérations sur les organisations et les espaces.

####Types d'utilisateur

Vous pouvez être membre ou collaborateur d'un compte.

<dl>
<dt>Membre</dt>
<dd>Vous êtes membre d'un compte {{site.data.keyword.Bluemix_notm}} si vous avez créé le compte ou avez été invité sur le compte, et si vous vous
êtes inscrit depuis l'invitation afin d'utiliser {{site.data.keyword.Bluemix_notm}} pour la première fois. </dd>
<dt>Collaborateur</dt>
<dd>Vous êtes collaborateur d'un compte {{site.data.keyword.Bluemix_notm}} si vous avez déjà utilisé {{site.data.keyword.Bluemix_notm}}
avec un compte différent, puis avez été invité sur ce compte et avez accepté l'invitation.</dd>
</dl>

####Rôles utilisateur

Les droits suivants peuvent être accordés aux utilisateurs pour qu'ils aient différents rôles utilisateur dans une organisation ou un espace :

<dl>
<dt>Responsables de l'organisation</dt>
<dd>Les responsables de l'organisation possèdent les droits suivants :
<ul>
<li>Créer ou supprimer des espaces dans l'organisation.</li>
<li>Inviter des utilisateurs dans l'organisation si le responsable de l'organisation est aussi membre de l'organisation ou propriété du compte.</li>
<li>Gérer des utilisateurs existants qui se trouvent déjà dans l'organisation.</li>
<li>Gérer les domaines de l'organisation.</li>
</ul>
<p>**Remarque** : si vous êtes collaborateur et avez déjà utilisé {{site.data.keyword.Bluemix_notm}} avec un compte différent,
vous ne pouvez pas inviter d'utilisateur dans l'organisation même si vous possédez le rôle de responsable de l'organisation. Vous devez être membre pour
pouvoir inviter des utilisateurs. Voir <a href="../troubleshoot/index.html#ts_adduser">Impossible d'ajouter des utilisateurs à une organisation</a>
pour des informations sur le contournement de ce problème.</p>
</dd>
<dt>Responsables de la facturation</dt>
<dd>Les responsables de la facturation possèdent des droits qui leur permettent d'afficher les informations sur l'utilisation des contextes d'exécution et
des services pour l'organisation.</dd>
<dt>Auditeurs de l'organisation</dt>
<dd>Les auditeurs de l'organisation possèdent des droits qui leur permettent d'afficher le contenu des applications et des services dans l'espace.</dd>
<dt>Responsables de l'espace</dt>
<dd>Les responsables de l'espace possèdent les droits suivants :
<ul>
<li>Il ajoutent des utilisateurs dans l'espace et gèrent les utilisateurs.</li>
<li>Activer des fonctions pour l'espace.</li>
</ul>
</dd>
<dt>Développeurs de l'espace</dt>
<dd>Les développeurs de l'espace possèdent les droits suivants :
<ul>
<li>Créer, supprimer et gérer des applications et des services dans l'espace.</li>
<li>Accéder aux journaux dans l'espace.</li>
</ul>
</dd>
<dt>Auditeurs de l'espace</dt>
<dd>Les auditeurs de l'espace possèdent des droits qui leur permettent d'accéder en lecture seule à toutes les informations sur l'espace, par exemple aux
informations sur les applications et les services, aux paramètres, aux rapports et aux journaux.</dd>
</dl>

###Gestion de votre organisation
{: #orgmng}

En tant que responsable de l'organisation ou propriétaire de compte, vous pouvez gérer vos organisations. Les tâches de gestion incluent la création
d'une organisation, le changement de nom d'une organisation, la création d'un espace, l'invitation d'utilisateurs dans un espace, la modification des rôles utilisateur et la suppression d'une organisation existante.

<ul>
<li>Création d'une organisation
<p>Seuls les utilisateurs qui possèdent un compte payant peuvent créer une organisation. Avec un compte payant, vous pouvez créer une organisation en
procédant comme suit :</p>
<ol>
<li>Accédez au tableau de bord {{site.data.keyword.Bluemix_notm}}, cliquez sur l'icône **Compte et support** ![Compte et support](../support/images/account_support.svg), puis sélectionnez **Gérer les organisations**.</li>
<li>Cliquez sur **Créer une organisation** et suivez les invites pour créer votre organisation.</li>
</ol>
</li>
<li>Changement de nom d'une organisation
<p>Procédez comme suit pour renommer votre organisation :</p>
<ol>
<li>Accédez au tableau de bord {{site.data.keyword.Bluemix_notm}}, cliquez sur l'icône **Compte et support** ![Compte et support](images/account_support.svg), et sélectionnez **Gérer les organisations**.</li>
<li>Sélectionnez l'organisation à renommer.</li>
<li>Entrez un nouveau nom dans la zone **Organisation** et cliquez sur **Sauvegarder**.</li>
</ol>
</li>
<li>Liste des membres
<p>Procédez comme suit pour répertorier les membres de votre organisation ou de votre espace :</p>
<ol>
<li>Accédez au tableau de bord {{site.data.keyword.Bluemix_notm}}, cliquez sur l'icône **Compte et support** ![Compte et support](../support/images/account_support.svg), puis sélectionnez **Gérer les organisations**. Vous pouvez afficher les membres de votre organisation et leurs rôles dans l'onglet
**Utilisateurs**.</li>
<li>Cliquez sur le nom de l'espace dans votre organisation pour afficher les membres de cet espace et leurs rôles.</li>
</ol>
</li>
<li>Création d'un espace
<p>Vous pouvez créer des espaces dans votre organisation, par exemple un espace *dev* comme environnement de développement, un espace
*test* comme environnement de test et un espace *production* comme environnement de production. Ensuite, vous pouvez associer vos
applications à des espaces. Procédez comme suit pour créer un espace :</p>
<ol>
<li>Accédez au tableau de bord {{site.data.keyword.Bluemix_notm}}, cliquez sur l'icône **Compte et support** ![Compte et support](images/account_support.svg), puis sélectionnez **Gérer les organisations**.</li>
<li>Cliquez sur **Créer un espace** indiqué à la suite du nom de votre organisation et suivez les invites afin de créer votre espace.</li>
</ol>
</li>
<li>Invitation d'utilisateurs dans un espace
<p>Vous pouvez inviter des utilisateurs dans votre organisation en tant que collaborateurs. Vous pouvez aussi ajouter des utilisateurs de votre
organisation à différents espaces. Les utilisateurs ne peuvent accéder qu'à l'espace auquel ils ont été ajoutés. Procédez comme suit pour ajouter un
utilisateur à un espace :</p>
<ol>
<li>Accédez au tableau de bord {{site.data.keyword.Bluemix_notm}}, cliquez sur l'icône **Compte et support** ![Compte et support](../support/images/account_support.svg), puis sélectionnez **Gérer les organisations**. Ensuite, cliquez sur **Ajouter un utilisateur** dans votre organisation et suivez les
invites pour ajouter l'utilisateur à votre organisation.</li>
<li>Ajoutez l'utilisateur à un espace. Sélectionnez l'espace dans le panneau de navigation, cliquez sur **Ajouter un utilisateur**, puis suivez les invites pour ajouter l'utilisateur à l'espace.</li>
</ol>
</li>
<li>Modifications de rôles utilisateur
<p>Procédez comme suit pour modifier les rôles utilisateur :</p>
<ol>
<li>Dans l'interface utilisateur {{site.data.keyword.Bluemix_notm}}, cliquez sur l'icône **Compte et support** ![Compte et support](images/account_support.svg), puis sélectionnez **Gérer les organisations**.</li>
<li>Sélectionnez la case à cocher **RESPONSABLE**, **RESPONSABLE DE LA FACTURATION** ou **AUDITEUR** dans l'onglet **UTILISATEURS** pour changer les rôles des utilisateurs dans votre organisation. Vous pouvez également sélectionnez un espace dans le panneau de navigation, puis sélectionnez la case à cocher **RESPONSABLE**, **DEVELOPPEUR** ou **AUDITEUR** dans l'onglet **UTILISATEURS** pour changer les rôles des utilisateurs dans cet espace. </li>
<li>Cliquez sur **SAUVEGARDER**.</li>
</ol>
</li>
<li>Suppression d'une organisation existante
<p>Prenez contact avec le support en charge des ID et de l'enregistrement {{site.data.keyword.Bluemix_notm}} pour qu'il supprime votre
organisation.</p>
<p>**Remarque** : les opérations de suppression sont irréversibles. Vous perdez toutes vos applications et tous les services qui sont
associés à l'organisation.</p>
</li>
</ul>

## Gestion de l'environnement {{site.data.keyword.Bluemix_notm}} local et de l'environnement {{site.data.keyword.Bluemix_notm}} dédié
{: #mng}

Si vous disposez d'un accès administrateur pour l'environnement {{site.data.keyword.Bluemix_notm}} local ou {{site.data.keyword.Bluemix_notm}} dédié, accédez à la page **Administration** pour gérer les ressources, surveiller l'utilisation des quotas, administrer des droits d'utilisateur, planifier des notifications de mise à niveau, afficher des rapports de sécurité et des journaux, etc. Vous pouvez gérer vos organisations en créant des espaces et en définissant des rôles utilisateur et des droits d'accès, voir [Gestion de vos organisations](index.html#orgmng).
{:shortdesc}

*Table 1. Tâches d'administration permettant de gérer une instance {{site.data.keyword.Bluemix_notm}} locale ou dédiée*

| Que puis-je faire ? | Détails |    
|----------------|---------|
|Surveiller l'utilisation du système | Cliquez sur **ADMINISTRATION &gt; USAGE**. Afficher vos informations système, surveiller l'utilisation de l'unité centrale et planifier l'utilisation pour prendre les meilleurs décisions pour votre entreprise.|
|Gérer votre catalogue | Cliquez sur **ADMINISTRATION &gt; CATALOG MANAGEMENT**. Gérer la visibilité des services par vos utilisateurs.|
|Administrer des organisations | Cliquez sur **ADMINISTRATION &gt; ORGANIZATION ADMINISTRATION**. Créez des organisations, surveillez les quotas relatifs aux organisations et prenez des décisions rapides en fonction de vos besoins.|
|Créer des espaces et affecter des rôles utilisateur | Cliquez sur l'icône **Compte et support** ![Compte et support](../support/images/account_support.svg), puis sélectionnez **Gérer les organisations**. Créez des espaces au sein de vos organisations. Ajoutez des utilisateurs et affectez des organisation et des espaces aux utilisateurs. |
|Gérer les droits d'administrateur | Cliquez sur **ADMINISTRATION &gt; USER ADMINISTRATION**. Ajoutez des utilisateurs, supprimez des utilisateurs et adaptez les droits des utilisateurs. |
|Consulter les rapports et les journaux | Cliquez sur **ADMINISTRATION &gt; REPORTS AND LOGS**. Affichez les rapports de sécurité et les journaux d'audit correspondant à votre instance.|
|Afficher les informations système | Cliquez sur **ADMINISTRATION &gt; SYSTEM INFORMATION**. Affichez les informations système, telles que les mises à jour en attente, le nom et la version de votre instance, la région, l'URL d'API, l'URL de l'interface de ligne de commande (CLI), les détails de configuration LDAP, les mappages de groupes et d'utilisateurs, les statistiques et les domaines partagés.  |

### Affichage des informations système
{: #oc_system}

Pour afficher les informations système, cliquez sur **ADMINISTRATION &gt; SYSTEM INFORMATION**.

Vous pouvez développer et afficher diverses sections sur les mises à jour en attente, les informations système générales et les détails de
configuration LDAP.

* Dans la section des mises à jour, vous pouvez afficher les mises à jour en attente qui requièrent une intervention de votre part. Vous pouvez
aussi effectuer facilement le suivi de vos mises à jour à l'aide du lien vers le calendrier afin d'importer vos mises à jour planifiées dans une
application de calendrier.

<ol>
<li>Afin d'effectuer une action pour une mise à jour spécifique, procédez comme suit :
<ol type="a">
<li>Cliquez sur <strong><em>Nombre</em> updates pending</strong> pour afficher toutes les mises à jour en attente.</li>
<li>Sélectionnez une mise à jour pour effectuer une action ou afficher les détails de la mise à jour, qui incluent la fenêtre de mise à jour, la date
planifiée ou le statut d'interruption.</li>
<li>Cliquez sur <strong>SET UNAVAILABLE DATES</strong> pour définir des jours spécifiques dans la fenêtre de mise à jour qui ne vous conviennent pas pour
l'application de la mise à jour. Si vous définissez des dates d'indisponibilité, IBM approuve et planifie votre mise à jour en fonction de vos sélections. Vous
recevez une notification lorsque la mise à jour est approuvée et planifiée.</li>
<li>Cliquez sur <strong>APPROVE</strong> pour approuver la mise à jour si toutes les dates vous conviennent. Si vous approuvez la mise à jour, celle-ci est appliquée au cours de la fenêtre de mise à jour planifiée. IBM envoie une notification au début et à la fin
du déploiement de la mise à jour.</li>
</ol>
</li>
<li>Pour importer vos mises à jour planifiées dans une application de calendrier de votre choix, procédez comme suit :
<ol type="a">
<li>Ouvrez votre application de calendrier.</li>
<li>Importez le calendrier des mises à jour en collant l'**adresse URL du calendrier** qui figure dans la page System Information dans
votre application. Ou bien, téléchargez le fichier calendrier en cliquant sur l'adresse URL du calendrier, puis en l'important dans votre application de
calendrier avec le fichier `.ics`.</li>
<li>Entrez vos données d'identification.</li>
<li>Affichez vos mises à jour planifiées.</li>
</ol>
</li>
</ol>

* Dans la section General Information, vous pouvez consulter les informations suivantes :
    * Des informations de base sur la génération {{site.data.keyword.Bluemix_notm}}.
    * Des informations sur les API, notamment la version, l'adresse URL, la région et un lien vers la documentation de l'interface de ligne de commande.
    * Des informations sur le domaine partagées concernant votre système et votre service.
    * Des statistiques sur le nombre total d'applications, d'utilisateurs et d'organisations.
* Dans la section LDAP Configuration Details, vous pouvez sélectionner le serveur LDAP et afficher des informations sur les mappages des
utilisateurs et des groupes. Si vous utilisez l'ID Web {{site.data.keyword.IBM}}, il est également indiqué dans cette section.

### Affichage des informations relatives à l'utilisation
{: #oc_resource}

Pour afficher les informations relatives aux ressources, cliquez sur **ADMINISTRATION &gt; USAGE**.

Dans la section Resource Monitoring, vous pouvez consulter les informations suivantes :

* Des informations relatives à l'utilisation des ressources, par exemple le nombre de gigaoctets de mémoire et le nombre de gigaoctets d'espace
disque qui sont utilisés. Vous pouvez afficher l'utilisation moyenne de l'UC par tous les agents DEA (Droplet Execution Agent). Cliquez sur la vignette
de l'**UC** pour afficher l'utilisation de l'UC pour chaque agent DEA. L'agent DEA associé à l'utilisation la plus élevée est répertorié en
premier, et chaque agent est identifié par son travail et son adresse IP. L'utilisation de l'UC est exprimée dans trois catégories : la quantité d'UC
utilisée pour les processus système, la quantité d'UC utilisée pour les processus utilisateur et la quantité d'UC utilisée pour les processus en attente.
* Des informations relatives à l'utilisation du réseau pour la bande passante entrante et la bande passante sortante, pour le jour précédent, la
semaine précédente ou le mois précédent.
Les données affichées dépendent de la somme du trafic entrant et sortant pour les réseaux publics et privés.
* Le temps de réponse moyen pour {{site.data.keyword.Bluemix_notm}} au cours des dix
minutes précédentes, de l'heure précédente ou du jour précédent.
* Le nombre moyen de transactions par seconde pour {{site.data.keyword.Bluemix_notm}} au
cours des dix minutes précédentes, de l'heure précédente ou du jour précédent.

### Affichage des rapports
{: #oc_report}

Vous pouvez afficher des journaux et des rapports de sécurité, tels que des rapports DataPower&trade;, de pare-feux et d'audit de connexion,
pour votre instance {{site.data.keyword.Bluemix_notm}}.

Pour afficher les rapports et les journaux, cliquez sur **ADMINISTRATION &gt; REPORTS AND LOGS**.

Effectuez l'une des opérations suivantes :

* Vous pouvez sélectionner des dates de début et de fin dans les zones afin de filtrer les rapports et les journaux à afficher.
* Vous pouvez développer et afficher divers rapports depuis le panneau de navigation.
* Vous pouvez effectuer une recherche dans votre collection de rapports et de journaux. La recherche s'applique aux noms de rapport ainsi qu'au
contenu textuel des rapports et des journaux. Vous pouvez aussi choisir de filtrer votre recherche par **événements d'administration**,
**rapports DataPower**, **pare-feu** et **audit de connexion**.
* Lors de l'affichage d'un rapport ou d'un journal, vous pouvez cliquer sur l'icône ![Télécharger](images/icon_download.svg) pour télécharger le rapport.

### Affichage du statut
{: #oc_status}

Vous pouvez surveiller le statut de votre instance {{site.data.keyword.Bluemix_notm}} à l'aide de la page Statut de {{site.data.keyword.Bluemix_notm}}. La page Statut est l'emplacement central pour rechercher des notifications et des annonces sur les événements clés affectant la plateforme {{site.data.keyword.Bluemix_notm}} et les principaux services dans {{site.data.keyword.Bluemix_notm}}.

Vous pouvez vous abonner à un flux RSS pour recevoir les notifications automatiquement et ne pas avoir à les rechercher. Pour plus d'informations sur la page Statut et la configuration du flux RSS, voir [Affichage de {{site.data.keyword.Bluemix_notm}}](../troubleshoot/getting_customer_support.html#status).

### Gestion de votre catalogue
{: #oc_catalog}

Vous pouvez choisir les services et les modules de démarrage {{site.data.keyword.Bluemix_notm}} que les utilisateurs peuvent voir dans
le catalogue {{site.data.keyword.Bluemix_notm}}. Cliquez sur **ADMINISTRATION &gt; CATALOG MANAGEMENT**.

Sélectionnez une vignette de service ou de module de démarrage afin d'éditer la visibilité du plan de service ou de module de démarrage. Pour éditer
la visibilité, sélectionnez l'une des options suivantes :
* Pour afficher un service ou un module de démarrage masqué de sorte que vos utilisateurs puissent le voir dans le catalogue, sélectionnez **ENABLE ALL PLANS**.
* Pour masquer un service ou un module de démarrage de sorte que vos utilisateurs ne le voient pas dans le catalogue {{site.data.keyword.Bluemix_notm}}, sélectionnez **DISABLE ALL PLANS**.
* Pour contrôler la visibilité d'un plan individuel, sélectionnez le nom du plan, puis utilisez le menu déroulant afin de sélectionner
**Enable for all organizations**, **Disable for all organizations** ou **Enable plan for specific
organizations**.

### Administration des organisations
{: #oc_organizations}

Vous pouvez gérer vos organisations en créant et en supprimant des organisations, en
ajoutant des responsables à des organisations, et en surveillant l'utilisation du quota.

Cliquez sur **ADMINISTRATION &gt; ORGANIZATION ADMINISTRATION**.

Vous pouvez développer et afficher diverses sections. Vous pouvez aussi passer en revue et gérer les plans d'établissement des quotas pour vos
organisations.

* Pour créer une organisation et ajouter des responsables, cliquez sur <strong>CREATE ORGANIZATION</strong>.
Entrez un nom pour l'organisation, puis entrez le nom ou l'adresse électronique de la personne que vous voulez désigner comme responsable. Vous pouvez ajouter plusieurs responsables en entrant et en sélectionnant plusieurs noms. Cliquez sur <strong>CREATE
ORGANIZATION</strong> pour sauvegarder vos modifications et créer l'organisation.
* Vous pouvez développer la section Quota Monitoring pour afficher les informations suivantes :
    * Environment memory usage. Cette section détaille l'utilisation de la mémoire pour l'intégralité de l'environnement système.
	Le graphique fournit diverses informations, notamment la quantité de mémoire système utilisée, la quantité de mémoire système totale, le quota utilisé et
le quota total alloué. La liste de termes suivante définit les types d'utilisation de la mémoire qui sont affichés dans le graphique :
	<dl>
	<dt><strong>Used system memory</strong></dt>
	<dd>Quantité de mémoire physique utilisée par votre environnement.</dd>
	<dt><strong>Total system memory</strong></dt>
	<dd>Quantité de mémoire physique totale qui est disponible dans votre environnement.</dd>
	<dt><strong>Quota deployed</strong></dt>
	<dd>Quantité de mémoire allouée à toutes les applications déployées dans toutes les organisations. La somme du quota déployé peut dépasser la quantité de
mémoire système totale physique pour votre environnement. Par exemple, si la quantité de mémoire système totale est de 16 Go et que vous allouez 4 Go de mémoire à chaque organisation pour cinq organisations
différentes, le quota total est supérieur à la quantité de mémoire système totale qui vous a été allouée pour toutes les organisations. Cependant, dans la plupart des cas, les organisations n'utilisent pas le quota total qui leur est alloué individuellement. De plus, les organisations
n'utilisent pas toutes la totalité de leur quota d'allocation de mémoire simultanément. </dd>
	<dt><strong>Total quota</strong></dt>
	<dd>Quantité de mémoire totale qui est allouée dans toutes les organisations.</dd>
	</dl>
	* Organization memory usage. Cette section détaille l'utilisation de la mémoire au niveau de l'organisation. Vous pouvez afficher le quota total et le
quota déployé pour chaque organisation. Le graphique fournit des informations triées en fonction de l'utilisation de la mémoire la plus élevée par
organisation ; par défaut, l'organisation qui utilise la quantité de mémoire la plus élevée est répertoriée en premier. Vous pouvez effectuer un tri en fonction de l'**utilisation de la mémoire la plus élevée** (Highest Memory Usage) et de l'**allocation
de mémoire superflue** (Excess Memory Allocation).
	<dl>
	<dt><strong>Highest Memory Usage</strong></dt>
	<dd>Utilisez cette option pour identifier l'organisation qui utilise la quantité de mémoire la plus élevée. Effectuez un tri par utilisation de la mémoire la plus élevée pour identifier les organisations qui utilisent la quantité de mémoire la plus élevée. La liste est triée par quota déployé. </dd>
	<dt><strong>Excess Memory Allocation</strong></dt>
	<dd>Utilisez cette option pour identifier les organisations dont le plan d'établissement des quotas est supérieur aux besoins.
	Effectuez un tri par allocation de mémoire superflue pour identifier les organisations qui utilisent la quantité de mémoire la plus faible par rapport au
quota qui leur a été alloué. </dd>
	</dl>
* Afin de changer le plan d'établissement des quotas pour une organisation, cliquez dans le graphique sur la barre correspondant à l'organisation
que vous voulez éditer dans la section Organization memory usage ou sélectionnez le nom de l'organisation dans la section Organization List. Dans la page
Edit Organization, vous pouvez changer le plan d'établissement des quotas, modifier le nom de l'organisation, et ajouter ou supprimer des responsables. Vous recevez un message si vous sélectionnez un plan d'établissement des quotas qui n'est pas
suffisant pour l'utilisation en cours pour l'organisation. Pour sauvegarder les modifications que vous avez apportées dans la page Edit Organization,
cliquez sur **SAVE**.
* Dans la section Organization List, vous pouvez afficher toutes les organisations de l'environnement {{site.data.keyword.Bluemix_notm}}.
	* Pour supprimer une organisation, cliquez sur ![Supprimer](images/icon_trash.svg) dans la colonne Actions. 
	* Afin d'afficher et d'éditer le plan d'établissement des quotas pour une organisation, cliquez sur le nom de l'organisation dans la liste.
	* Pour éditer le nom de l'organisation et ajouter ou supprimer des responsables, cliquez sur le nom de l'organisation dans la liste.

### Gestion des utilisateurs et des droits
{: #oc_useradmin}

Vous pouvez ajouter des utilisateurs à votre instance {{site.data.keyword.Bluemix_notm}} depuis le registre d'utilisateurs de votre société via
LDAP. Vous pouvez ajouter des utilisateurs individuels ou des groupes d'utilisateurs et
afficher les droits d'utilisateur. Si vous disposez du droit `admin`, vous pouvez également définir et gérer les droits des autres
utilisateurs. Cliquez sur **ADMINISTRATION &gt; USER ADMINISTRATION**.

La page User Administration affiche tous les utilisateurs pour l'instance locale ou dédiée.
Les droits de chaque utilisateur sont affichés. Les droits peuvent être les suivants : aucun, `Admin`, `Catalog`,
`Login`, `Reports` et `Users`. Ils peuvent être activés, ou l'utilisateur peut se voir
attribuer la capacité `view` (afficher) ou `write` (écrire) pour ce droit, comme représenté par les icônes. Voir [Droits](#permissions) pour la description de chaque type et l'explication des icônes.

Effectuez l'une des opérations suivantes :
* Localisez des utilisateurs. Vous pouvez localiser des utilisateurs dans le tableau via la zone **Search**.
* Ajoutez des utilisateurs. Si vous disposez du droit `admin` ou du droit `users` avec la capacité
`write` (écrire), vous pouvez ajouter des utilisateurs. Pour ajouter un utilisateur ou un groupe d'utilisateurs, cliquez sur
**Add single user** ou **Add user group**. Dans la zone **Search**, entrez un nom d'utilisateur ou un nom de groupe à rechercher et sélectionnez
l'organisation à laquelle ajouter l'utilisateur ou le groupe d'utilisateurs dans la liste **Org**. Lorsque vous trouvez l'utilisateur ou
le groupe à ajouter, cliquez sur le nom d'utilisateur, puis cliquez sur **Add user** ou **Add users**.
Les
groupes de plus de 50 utilisateurs sont ajoutés via un travail par lots en arrière-plan. Lorsque l'opération d'ajout aboutit, l'utilisateur ou le groupe est ajouté à la table pour que vous puissiez l'afficher et le rechercher. Lorsque des utilisateurs sont ajoutés, aucun droit ne leur est affecté.
* Editez les droits et les organisations. Si vous disposez du droit `admin`, vous pouvez éditer les droits et les organisations
pour d'autres utilisateurs. Pour éditer les droits, localisez l'utilisateur et cliquez sur son nom. Pour activer ou désactiver des droits, sélectionnez
l'une des options suivantes dans la fenêtre qui s'ouvre :
	* Sélectionnez **On** dans la liste pour activer un droit.
	* Sélectionnez **Read** dans la liste pour que l'utilisateur dispose de la capacité `view` (afficher en lecture
seule) pour ce droit ou
**Write** pour qu'il dispose de la capacité `write` (écrire, c'est-à-dire éditer, ajouter ou supprimer) pour ce droit.
	* Sélectionnez **Off** pour désactiver le droit.
Pour éditer des organisations, choisissez l'une des options
suivantes :
	* Ajoutez l'utilisateur à une organisation en utilisant la zone de recherche afin de localiser une organisation, puis en sélectionnant les options de
votre choix et en cliquant sur **Add**.
	* Retirez un utilisateur d'une organisation en cliquant sur l'icône ![Retirer, représentée par le signe moins](images/icon_remove.svg).
Une fois que vous avez terminé, cliquez sur
**Save**.
* Retirez des utilisateurs. Si vous disposez du droit `admin` ou du droit `users` avec la capacité
`write` (écrire), vous pouvez retirer des utilisateurs.
Pour supprimer un utilisateur, localisez-le et cliquez sur l'icône ![Supprimer](images/icon_trash.svg) puis sur **Remove**.

### Droits
{: #permissions}

Les droits suivants peuvent être accordés aux utilisateurs :

| **Droit d'utilisateur** | **Description** |       
|-----------------|-------------------|
| Admin | Les utilisateurs disposant du droit `admin` peuvent éditer les droits des autres utilisateurs. |
| Catalog | Les utilisateurs disposant du droit `catalog` peuvent afficher (capacité `view`) ou modifier (capacité
`write`) les services qui sont disponibles dans l'instance locale ou dédiée. |  
| Login | Les utilisateurs disposant du droit `login` sont autorisés à voir la page Administration. Sans ce droit, les utilisateurs ne peuvent pas voir l'option de menu Administration. |
| Reports | Les utilisateurs disposant du droit `reports` peuvent afficher (`view`) ou modifier (`write`)
les rapports de sécurité. |
| Users | Les utilisateurs disposant du droit `users` peuvent afficher (`view`) la liste des utilisateurs ou
ajouter ou retirer (`write`) des utilisateurs. Ce droit ne vous permet pas de définir des droits pour d'autres utilisateurs.|

*Tableau 2. Droits*

Les droits peuvent être activés, ou l'utilisateur peut se voir attribuer la capacité `view` (afficher) ou
`write` (écrire) pour ces droits, comme représenté par les icônes suivantes :

* L'icône ![Activé, représentée par une coche](images/icon_enabled.svg) à côté d'un droit signifie que le droit est activé.
* L'icône ![Afficher, représenté par un oeil](images/icon_read.svg) signifie que l'utilisateur dispose de la capacité `view` (afficher en lecture seule)
pour ce droit.
* L'icône ![Ecrire, représenté par un crayon](images/icon_write.svg) signifie que l'utilisateur dispose de la capacité `write` (écrire, c'est-à-dire
éditer, ajouter ou supprimer) pour ce droit.

### Gestion des utilisateurs avec l'API REST Admin
{: #usingadminapi}

Vous pouvez utiliser l'API REST `Admin` afin d'ajouter et de retirer des utilisateurs pour votre instance
{{site.data.keyword.Bluemix_notm}}.
Les noeuds finaux de l'API REST
`Admin` et les réponses JSON sont fournis sur une base expérimentale afin de permettre des opérations de base depuis une ligne de
commande. Les noeuds finaux et les adresses URL qui figurent dans les exemples de cette documentation peuvent changer ou être abandonnés dans un délai
court.

Les outils ci-après sont requis pour l'utilisation des exemples qui suivent. Vous pouvez également choisir d'utiliser d'autres outils.
* cURL, pour entrer les demandes d'API REST sous forme de commandes. cURL est un utilitaire gratuit que vous pouvez utiliser pour envoyer des
demandes HTTP à un serveur
et recevoir les réponses du serveur via une interface de ligne de commande. Vous pouvez le télécharger depuis le
[site de téléchargement cURL](http://curl.haxx.se/download.html){: new_window}.
* Python, pour utiliser l'outil JSON d'impression élégante de Python. Cet outil facultatif transforme le texte JSON en entrée en sortie facile à lire. Vous pouvez télécharger Python depuis le [site des téléchargements Python](https://www.python.org/downloads){: new_window}.

#### Connexion à la console d'administration

Pour pouvoir exécuter des requêtes d'API `Admin`, vous devez vous connecter à la console d'administration. Si vous disposez
du droit `admin` ou du droit `users` avec la capacité `write` (écrire), vous pouvez ajouter ou
retirer
des utilisateurs. Vous devez disposer du droit `admin` pour éditer les droits des autres utilisateurs.

Pour vous connecter à la console d'administration, vous pouvez utiliser l'authentification d'accès de base sur le noeud final
`https://<votre_hôte>.ibm.com/login`. Le serveur renvoie un cookie avec votre session. Vous utilisez ce cookie pour toutes les opérations avec la console d'administration.

**Remarque :** la session n'est plus valide si elle n'est pas utilisée pendant quelques heures.

Pour vous connecter à la console d'administration, exécutez la commande suivante :

`curl --user <id_utilisateur>:<mot_de_passe> -c ./cookies.txt --header "Accept: application/json"
https://<votre_hôte>.ibm.com/login | python -m json.tool`
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">--user <em>id_utilisateur</em>:<em>mot_de_passe</em></dt>
<dd class="pd">Accepte l'ID utilisateur et le mot de passe et envoie un en-tête d'autorisation de base.</dd>


<dt class="pt dlterm">-c <em>nom_fichier</em></dt>
<dd class="pd">Stocke l'ID utilisateur et le mot de passe spécifiés sous forme de cookie dans le fichier spécifié.</dd>


<dt class="pt dlterm">--header</dt>
<dd class="pd">Envoie un en-tête Accept.</dd>

</dl>

Voici un exemple de sortie pour
cette commande :
```
{
    "message": "Logged in",
    "name": {
        "familyName": "*nom*",
        "givenName": "*prénom*"
    }
}
```
{: screen}

#### Liste des organisations
{: #listingorg}

Lorsque vous ajoutez un utilisateur, vous devez spécifier une organisation. Vous pouvez utiliser l'API REST `Admin` pour
répertorier toutes les organisations. Vous devez disposer du droit `users` avec la capacité `read` (lire) pour pouvoir
répertorier les organisations. Pour répertorier toutes les organisations, exécutez la commande suivante :

`curl -b ./cookies.txt https://<votre_hôte>.ibm.com/codi/v1/organizations | python -m json.tool`
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">-b <em>nom_fichier</em></dt>
<dd class="pd">Transmet l'ID utilisateur et le mot de passe stockés précédemment avec l'option <samp class="ph codeph">-c</samp> dans le fichier sur le serveur HTTP sous forme
de cookie.</dd>

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

#### Liste des utilisateurs
{: #listingusr}

Vous pouvez déterminer si un utilisateur a déjà été ajouté à votre environnement {{site.data.keyword.Bluemix_notm}} en utilisant l'API
REST `Admin` afin de répertorier les utilisateurs enregistrés. Vous devez disposer du droit `users` avec la capacité
`read` (lire) pour pouvoir répertorier les utilisateurs enregistrés. Pour répertorier toutes les utilisateurs, exécutez la commande
suivante :

`curl -b ./cookies.txt https://<votre_hôte>.ibm.com/codi/v1/users | python -m json.tool`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-b <em>nom_fichier</em></dt>
<dd class="pd">Transmet l'ID utilisateur et le mot de passe stockés précédemment avec l'option <samp class="ph codeph">-c</samp> dans le fichier sur le serveur HTTP sous forme
de cookie.</dd>
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

#### Ajout d'un utilisateur

Vous pouvez utiliser l'API REST `Admin` pour ajouter des utilisateurs à l'instance {{site.data.keyword.Bluemix_notm}}. Vous devez disposer du droit
`users` avec la capacité `write` (écrire) pour pouvoir ajouter des utilisateurs.

Vous pouvez ajouter un utilisateur ou une liste d'utilisateurs. Vous pouvez ajouter des utilisateurs à une seule organisation ou à plusieurs
organisations.-->Pour ajouter un utilisateur, vous devez fournir les informations suivantes :

* Prénom et nom de l'utilisateur. Indiquez les valeurs `"first_name"` et `"last_name"` figurant dans
[Liste des utilisateurs](index.html#listingusr).
* Adresse électronique et ID utilisateur. Indiquez la valeur `"user_id"` figurant dans [Liste des
utilisateurs](index.html#listingusr) pour l'adresse électronique et l'ID utilisateur.
* `"guid"`. Indiquez l'identificateur global unique de l'organisation figurant dans [Liste des organisations](index.html#listingorg).

Vous
fournissez les informations dans un fichier JSON.

`curl -b ./cookies.txt https://<votre_hôte>.ibm.com/codi/v1/users | python -m json.tool`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-b <em>nom_fichier</em></dt>
<dd class="pd">Transmet l'ID utilisateur et le mot de passe stockés précédemment avec l'option <samp class="ph codeph">-c</samp> dans le fichier sur le serveur HTTP sous forme
de cookie.</dd>
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
            "first_name": "Un_prénom",
            "last_name": "Un_nom",
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
<li>Envoyez le contenu du fichier JSON au noeud final de l'utilisateur en exécutant la commande suivante :<br/><br/>
<code>
curl -v -b ./cookies.txt -X POST -H "Content-Type: application/json" -d @./user.json https://<votre_hôte>.ibm.com/codi/v1/users
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

#### Retrait d'un utilisateur

Vous pouvez utiliser l'API REST `Admin` pour retirer des utilisateurs de l'instance {{site.data.keyword.Bluemix_notm}}. Vous devez disposer du droit
`users` avec la capacité `write` (écrire) pour pouvoir retirer des utilisateurs.

Pour retirer un utilisateur, vous devez
fournir l'ID de l'utilisateur. Exécutez la commande suivante :

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

### API de service personnalisée
{: #servicebrokerapi}

Vous pouvez utiliser trois interfaces de programmation (API) pour enregistrer ou créer un nouveau service, mettre à jour un service et supprimer un service.

Toutes les API sont relatives à <code>https://opsconsole.&lt;sous-domaine&gt;.bluemix.net/</code>.

<dl>
<dt><strong>&lt;sous-domaine&gt;</strong></dt>
<dd>Cette valeur est le nom de votre instance locale ou dédiée. Le nom de sous-domaine pour votre instance {{site.data.keyword.Bluemix}} a été affecté au cours du processus
d'intégration.</dd>
</dl>

### Enregistrement d'un nouveau service

Utilisez l'API et les exemples de code suivants pour enregistrer un nouveau service.

#### Route

```
POST /codi/v1/serviceBrokers
```
{: screen}

#### Demande

*Tableau 3. Zones*

| **Nom** | **Description** |
|-----------------|-------------------|
| name | Nom du courtier de services. |
| auth_username | Nom d'utilisateur utilisé pour se connecter au courtier de services. |
| auth_password | Mot de passe utilisé pour se connecter au courtier de services. |
| broker_url | URL utilisée pour se connecter au courtier de services. |
| owningOrganization | Organisation initiale avec laquelle enregistrer le service sur la liste blanche. |

##### Corps

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

##### En-têtes

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

#### Réponse

##### Statut

```
201 Created
```
{: screen}

##### Corps

```
{
  "entity": {
    "name": "Nom du courtier de services",
    "broker_url": "https://provision-broker.comp.bluemix.net/bmx/provisioning/brokers/2063580064-8f23230c-7f36-4ce5-a298-2ab4108f1120",
    "auth_username": "nom d'utilisateur",
    "space_guid": null
  },
  "warnings": [],
  "metadata": {
    "guid": "49f3adcc-ecc2-46fa-83c1-03322f04b3b1",
    "created_at": "2015-12-07T19:51:50Z",
    "updated_at": null,
    "url": "/v2/service_brokers/49f3adcc-ecc2-46fa-83c1-03322f04b3b1"
  }
}
```
{: screen}

### Mise à jour d'un service

Utilisez l'API et les exemples de code suivants pour mettre à jour un service.

#### Route

`PUT /codi/v1/serviceBrokers`
{: screen}

#### Demande

*Tableau 4. Zones*

| **Nom** | **Description** |
|-----------------|-------------------|
| name | Nom du courtier de services. Ce nom ne peut pas varier du nom avec lequel a été créé le service. |
| auth_username | Nom d'utilisateur utilisé pour se connecter au courtier de services. |
| auth_password | Mot de passe utilisé pour se connecter au courtier de services. |
| broker_url | URL utilisée pour se connecter au courtier de services. |
| owningOrganization | Organisation initiale avec laquelle enregistrer le service sur la liste blanche. |

##### Corps

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

##### En-têtes

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

#### Réponse

##### Statut

```
201 Created
```
{: screen}

##### Corps

```
{
  "entity": {
    "name": "Nom du courtier de services",
    "broker_url": "https://provision-broker.dys0.bluemix.net/bmx/provisioning/brokers/2063580064-d11bdd84-7556-469f-858d-2098b531f7f2",
    "auth_username": "nom d'utilisateur",
    "space_guid": null
  },
  "warnings": [],
  "metadata": {
    "guid": "2cbdb812-d37f-443b-894a-a96de31e5c38",
    "created_at": "2015-12-07T20:11:08Z",
    "updated_at": "2015-12-07T20:11:19Z",
    "url": "/v2/service_brokers/2cbdb812-d37f-443b-894a-a96de31e5c38"
  }
}
```
{: screen}

### Suppression d'un service

Utilisez l'API et les exemples de code suivants pour supprimer un service.

*Tableau 5. Paramètre*

| **Nom** | **Description** |
|-----------------|-------------------|
| name | Nom du courtier de services. Ce nom ne peut pas varier du nom avec lequel a été créé le service. |

#### Route

```
DELETE /codi/v1/serviceBrokers?name=nom du courtier de services
```
{: screen}

#### Demande

##### En-têtes

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

#### Réponse

##### Statut

```
204 No Content
```
{: screen}

### Gestion des utilisateurs avec l'interface de ligne de commande cf
{: #usingadmincli}

Vous pouvez gérer les utilisateurs pour votre environnement
{{site.data.keyword.Bluemix_notm}} local ou {{site.data.keyword.Bluemix_notm}} dédié en utilisant l'interface de ligne de commande Cloud Foundry avec le plug-in
d'interface de ligne de commande d'administration {{site.data.keyword.Bluemix_notm}}. Par exemple, vous pouvez ajouter des utilisateurs depuis
un registre LDAP.

Avant de commencer, installez l'interface de ligne de commande cf. Le plug-in d'interface de ligne de commande d'administration {{site.data.keyword.Bluemix_notm}} requiert cf version 6.11.2 ou ultérieure. [Télécharger l'interface de ligne de commande Cloud Foundry](https://github.com/cloudfoundry/cli/releases){: new_window}

**Restriction :** l'interface de ligne de commande Cloud Foundry n'est pas prise en charge par Cygwin. Utilisez-la dans une fenêtre de ligne de commande autre que Cygwin.

#### Ajout du plug-in d'interface de ligne de commande d'administration {{site.data.keyword.Bluemix_notm}}

Une fois l'interface de ligne de commande cf installée, vous pouvez ajouter le plug-in d'interface de ligne de commande d'administration
{{site.data.keyword.Bluemix_notm}}.

Procédez comme suit pour ajouter le référentiel et installer le plug-in :

<ol>
<li>Pour ajouter le référentiel de plug-in d'administration {{site.data.keyword.Bluemix_notm}}, exécutez la commande suivante : <br/><br/>
<code>
cf add-plugin-repo BluemixAdmin https://opsconsole.&lt;sous-domaine&gt;.bluemix.net/cli
</code><br/><br/>
<dl class="parml">
<dt class="pt dlterm">&lt;sous-domaine&gt;</dt>
<dd class="pd">Sous-domaine de l'adresse URL pour votre instance {{site.data.keyword.Bluemix_notm}}.</dd>
</dl>
</li>
<li>Pour installer le plug-in d'interface de ligne de commande d'administration {{site.data.keyword.Bluemix_notm}}, exécutez la commande suivante :<br/><br/> <code>
cf install-plugin bluemix-admin-cli -r BluemixAdmin
</code>
</li>
</ol>

Pour afficher la liste des commandes, exécutez la
commande suivante :

`cf plugins`
{: codeblock}

Pour obtenir de l'aide supplémentaire sur une commande, utilisez l'option `-help`.

Pour plus d'informations sur l'utilisation du plug-in d'interface de ligne de commande d'administration {{site.data.keyword.Bluemix_notm}}, voir [Administration {{site.data.keyword.Bluemix_notm}}](../cli/plugins/bluemix_admin/index.html).
