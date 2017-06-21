---

copyright:
  years: 2016, 2017
lastupdated: "2016-10-16"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Niveaux d'accès pour des rôles d'utilisateur

Les tableaux ci-après illustrent le niveau d'accès de chacun des rôles d'utilisateur.

Les tableaux répertorient les niveaux d'accès pour :
- Les [opérations de terminal](#user-device-ops)
- Les [opérations de journal](#user-log-ops)
- Les [opérations de cache](#user-cache-ops)
<!-- [Historian Operations](#user-historian) -->
- Les [opérations d'organisation](#user-org-ops)
- Les [opérations de contrôle d'accès](#user-access-ops)
- Les [opérations d'analyse](#user-analytics-ops)
- Les [opérations de service de tiers](#user-third-party)  
<!-- - [Risk Management Operations](#user-risk-mgt) -->

## Droit associés aux rôles d'utilisateur {: #user-roles}

### Opérations de terminal {: #user-device-ops}

Opérations de terminal ||| Rôles d'utilisateur|||
:--------: | -------------|-------------|---------------|-----|---
           | **Administrateur** | **Opérateur** | **Développeur** | **Analyste** | **Lecteur**
Créer, mettre à jour, ou supprimer des terminaux | X | X | X | - | -
Afficher les terminaux | X | X | X | X | X
Activer un terminal | X | X | X | - | -
Publier un événement | - | - | - | - | -
S'abonner à un événement | X | X | X | X | X
Publier une commande | X | X | X | - | -
S'abonner à une commande | - | - | - | - | -
Lancer une action de gestion des terminaux | X | X | X | - | -
Afficher des actions de gestion des terminaux | X | X | X | X | X
Effacer des actions de gestion des terminaux | X | X | X | - | -
Gérer les regroupements d'actions de gestion des terminaux | X | X | X | - | -
Créer, mettre à jour ou supprimer des types de terminaux | X | X | X | - | -
Afficher des types de terminaux | X | X | X | X | X
Gérer des journaux de diagnostic | X | X | X | - | -
Afficher des journaux de diagnostic | X | X | X | - | -

### Opérations de journal {: #user-log-ops}

Opérations de journal ||| Rôles d'utilisateur|||
:--------: | -------------|-------------|---------------|-----|---
           | **Administrateur** | **Opérateur** | **Développeur** | **Analyste** | **Lecteur**
Afficher les journaux serveur | X | X | X | X | X

### Opérations de cache {: #user-cache-ops}

Opérations de cache ||| Rôles d'utilisateur|||
:--------: | -------------|-------------|---------------|-----|---
           | **Administrateur** | **Opérateur** | **Développeur** | **Analyste** | **Lecteur**
Afficher les données en temps réel (cache d'événement) | X | X | X | X | X
Gérer les données en temps réel (cache d'événement) | X	| X | X |	X	| -

### Opérations d'organisation {: #user-org-ops}

Opérations d'organisation ||| Rôles d'utilisateur|||
:--------: | -------------|-------------|---------------|-----|---
           | **Administrateur** | **Opérateur** | **Développeur** | **Analyste** | **Lecteur**
Configurer les paramètres de stockage|	X| - |-|-|-
Configurer le fournisseur d'authentification|	X|-|-|-|-				
Créer, afficher, mettre à jour, supprimer la configuration de courrier	|X|-|-|-|-				
Afficher les fournisseur de messagerie IoTP disponibles	|X|	X|-|-|-			
Créer, afficher, mettre à jour, supprimer des modèles de courrier	|X	|X	|-|-|-		
Créer, mettre à jour et supprimer des utilisateurs	|X|	X|-|-|-
Afficher les utilisateurs	|X|	X|	X|	X|-
Créer, mettre à jour, supprimer des invitations d'utilisateur|	X	|X	| -|-|-
Afficher les invitations d'utilisateur	|X	|X	|- |- |-
Terminer une invitation	|X|	X|	X|	X|	X
Créer, mettre à jour et supprimer des clés d'API	|X	|X	| -|-|-
Afficher les clés d'API	|X	|X	|- |- |-		
Afficher les informations d'utilisation de l'organisation	|X	|X	| -|-|-		

### Opérations de contrôle d'accès {: #user-access-ops}

Opérations de contrôle d'accès ||| Rôles d'utilisateur|||
:--------: | -------------|-------------|---------------|-----|---
           | **Administrateur** | **Opérateur** | **Développeur** | **Analyste** | **Lecteur**
Afficher les propriétés utilisateur, y compris les droits d'accès	|X|	X|	X|	X| -
Afficher les propriétés des utilisateurs, y compris les droits d'accès	|X|	X|	X|	X|	X
Gérer les utilisateurs, y compris les droits d'accès	|X	|X	|-|-|-
Afficher les propriétés de clé d'API, y compris les droits d'accès|	X|	X|	X|	X|-
Afficher les propriétés de la clé d'API, y compris les droits d'accès	|-|	-|	-| -| -		
Créer, mettre à jour, supprimer des clés d'API, y compris les droits d'accès	|X	|X	|-|-|-
Afficher les propriétés de terminal, y compris les droits d'accès	|X|	X|	X|	X|	X
Afficher les propriétés du terminal, y compris les droits d'accès	|-	|- |- |- |-
Créer, mettre à jour, supprimer un terminal, y compris les droits d'accès	|X|	X|	X|	-| -
Afficher les rôles	|X	|X	|X	|X	|X
Créer, mettre à jour et supprimer des rôles personnalisés	|X	|X |- |- |-
Afficher les opérations*	|X	|X	|X	|X	|X

### Opérations d'analyse {: #user-analytics-ops}

Opérations d'analyse ||| Rôles d'utilisateur|||
:--------: | -------------|-------------|---------------|-----|---
           | **Administrateur** | **Opérateur** | **Développeur** | **Analyste** | **Lecteur**
Afficher les règles d'analyse|	X|	X|	X|	X|	X
Gérer les règles d'analyse|	X|	X|	X|	X| -
Afficher les actions d'analyse|	X|	X|	X|	X|	X
Gérer les actions d'analyse|	X|	X|	X|	X| -
Afficher les alertes d'analyse|	X|	X|	X|	X|	X
Afficher les schémas de message d'analyse|	X|	X|	X|	X|	X
Gérer les schémas de message d'analyse|	X|	X|	X|	X| -

### Opérations de service de tiers {: #user-third-party}

Opérations de service de tiers ||| Rôles d'utilisateur|||
:--------: | -------------|-------------|---------------|-----|---
           | **Administrateur** | **Opérateur** | **Développeur** | **Analyste** | **Lecteur**
Traiter des notifications par lots depuis une plateforme externe	|X|	X	|X |-|-
Traiter des notifications par lots et les envoyer à une plateforme externe	|X|	X	|X| -| -
Publier un événement pour un terminal	|X|	X	|X|	- |-
S'abonner à des événements depuis un terminal	|X	|X	|X |-| -
Définir une URL de rappel pour la plateforme externe	|X	|X	|X|	-| -
Définir le niveau d'abonnement de la plateforme externe|	X|	X|	X |- |-
Obtenir l'état de santé du connecteur	|X|	X	|X	|- |-
Vérifier si un système externe est opérationnel et valider les données d'identification	|X	|X|	X	|- |-
