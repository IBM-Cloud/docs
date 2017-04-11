---

copyright:
  years: 2016, 2017
lastupdated: "2016-09-16"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Rôles d'utilisateur, d'application et de passerelle

Les rôles sont des ensembles de droits que vous pouvez utiliser pour accorder ou restreindre l'accès à certaines opérations. Vous pouvez utiliser des rôles afin de gérer des droits pour des groupes d'utilisateurs, d'applications et de passerelles.
{:shortdesc}

## Rôles d'utilisateur
{: #user_roles}

Vous pouvez affecter des rôles d'utilisateur lorsque vous ajoutez, invitez ou enregistrez un utilisateur sur votre instance {{site.data.keyword.iot_full}}. Vous pouvez également affecter ou modifier des rôles d'utilisateur à tout moment à l'aide du tableau de bord {{site.data.keyword.iot_short_notm}}. Pour plus d'informations sur l'affectation d'un rôle à un utilisateur, voir [Gestion des rôles d'utilisateur](managing_user_roles.html).

Les rôles d'utilisateur standard suivants sont disponibles :

Rôle d'utilisateur | Description
------------- | -------------
Administrateur | Rôle de superutilisateur qui accorde un accès à toutes les API liées aux utilisateurs. Les administrateurs ne peuvent pas accéder à des opérations qui sont limitées à des terminaux et à des applications.
Opérateur | Destiné aux utilisateurs de l'organisation principale. Accorde un accès à la plupart des opérations d'organisation, de contrôle d'accès, d'analyse, de service de tiers et de gestion des risques.
Développeur | Accorde un accès illimité aux opérations de terminal, de journal, de cache, d'historique, d'analyse et de service de tiers. Il fournit un accès limité aux opérations d'organisation, de contrôle d'accès et de gestion des risques.
Analyste | Accorde un accès aux opérations d'analyse, y compris la création, la mise à jour et la suppression de règles, d'actions et de schémas.
Lecteur | Rôle d'utilisateur par défaut. Accorde un accès limité aux opérations disponibles pour tous les utilisateurs.

Pour plus d'informations sur les rôles d'utilisateur, voir [Rôles d'utilisateur](reference/roles_access.html).

## Rôles d'application
{: #application_roles}
Vous pouvez affecter des rôles d'application afin d'accorder ou de refuser à vos applications l'accès à des opérations spécifiques. Tous les rôles d'application refusent l'accès aux opérations suivantes :

- Toutes les opérations de gestion des risques
- Configuration des paramètres de stockage
- Configuration des fournisseurs d'authentification
- Création, mise à jour ou suppression de la configuration de courrier

Les rôles d'application standard suivants sont disponibles :

Rôle d'application | Description
------------- | -------------
Standard | Rôle d'application par défaut. Accorde l'accès à la plupart des opérations d'application, mais pas aux opérations d'utilisateur ou de rôle.   
Opérations | Accorde l'accès à plus large gamme d'opérations, mais refuse l'accès aux opérations d'abonnement ou de publication.
Sécurisée de back end | Destiné aux applications ne requièrent pas d'interaction avec l'opérateur système. Refuse l'accès aux opérations de gestion des terminaux, d'organisation, de rôle ou d'extension.
Processeur de données | Destiné aux applications qui effectuent des opérations d'analyse et de traitement des données. Pour les applications de processeur de données, un accès limité est accordé aux opérations d'organisation et aux opérations d'utilisateur, mais un accès complet est accordé aux opérations d'analyse, y compris la création et la gestion de règles, d'actions et de schémas.
Visualisation | Destiné aux applications chargées de générer des visualisations de données. Les applications de visualisation ont accès à des opérations sur des données en temps réel et stockées et à des opérations de tableau de bord.
Terminal | Destiné aux applications qui jouent le rôle de terminaux ; autrement dit, elles fournissent une source de données qui est envoyée à {{site.data.keyword.iot_short_notm}}, comme si elles étaient un terminal. Les applications de terminal ne disposent que d'un accès limité aux opérations.

Pour plus d'informations sur l'accès aux opérations des rôles d'application, voir [Rôles d'application](reference/app_roles_access.html).

## Rôles de passerelle
{: #gateway_roles}
Les passerelles disposent d'un nombre limité de rôles qui régissent leur définition et leur capacité à enregistrer des terminaux sur {{site.data.keyword.iot_short_notm}}.

les rôles de passerelle standard suivants sont disponibles :

Rôle de passerelle | Description
------------- | -------------
Standard | Rôle de passerelle par défaut. Accorde un accès limité aux opérations.
Privilégié | Destiné aux passerelles sécurisées et permet aux passerelles privilégiées d'ajouter des terminaux à {{site.data.keyword.iot_short_notm}}. Il accorde un accès aux opérations pertinentes relatives à l'ajout, la mise à jour et la gestion des terminaux et des propriétés de terminal, mais refuse tout accès aux autres opérations.  

Pour plus d'informations sur l'accès aux opérations de rôles de passerelle, voir [Rôles de passerelle](reference/gateway_roles_access.html).
