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

# Niveaux d'accès pour les rôles de passerelle

Les tableaux ci-après illustrent le niveau d'accès de chacun des rôles de passerelle.

Les tableaux répertorient les niveaux d'accès pour :
- Les [opérations de terminal](#gateway-device-ops)
- Les [opérations de journal](#gateway-log-ops)
- Les [opérations de cache](#gateway-cache-ops)
<!-- [Historian Operations](#gateway-historian) -->
- Les [opérations d'organisation](#gateway-org-ops)
- Les [opérations de contrôle d'accès](#gateway-access-ops)
- Les [opérations d'analyse](#gateway-analytics-ops)
- Les [opérations de service de tiers](#gateway-third-party)  
<!-- - [Risk Management Operations](#gateway-risk-mgt) -->

## Rôles de passerelle
{: #gateway-roles}

### Opérations de terminal {: #gateway-device-ops}

Opérations de terminal || Rôles de passerelle|
:--------: | ---------------------|------------------------
           | **Passerelle standard** | **Passerelle privilégiée**
Créer, mettre à jour ou supprimer de terminaux|-|X
Afficher les terminaux|X|X
Activer un terminal|-|X
Publier un événement|X|X
S'abonner à un événement|-|-
Publier une commande|-|-
S'abonner à une commande|X|X
Lancer une action de gestion des terminaux|X|X
Afficher des actions de gestion des terminaux|X|X
Effacer des actions de gestion des terminaux|-|-
Gérer les regroupements d'actions de gestion des terminaux|-|X
Créer, mettre à jour ou supprimer des types de terminaux|-|-
Afficher des types de terminaux|X|X
Gérer des journaux de diagnostic|-|-
Afficher des journaux de diagnostic|-|-

### Opérations de journal {: #gateway-log-ops}

Opérations de journal || Rôles de passerelle|
:--------: | ---------------------|------------------------
           | **Passerelle standard** | **Passerelle privilégiée**
Afficher les journaux serveur|-|-

### Opérations de cache {: #gateway-cache-ops}

Opérations de cache || Rôles de passerelle|
:--------: | ---------------------|------------------------
           | **Passerelle standard** | **Passerelle privilégiée**
Afficher les données en temps réel (cache d'événement)|-|-
Gérer les données en temps réel (cache d'événement)|-|-


### Opérations d'organisation {: #gateway-org-ops}

Opérations d'organisation || Rôles de passerelle|
:--------: | ---------------------|------------------------
           | **Passerelle standard** | **Passerelle privilégiée**
Configurer les paramètres de stockage|-|-
Configurer le fournisseur d'authentification|-|-
Créer, afficher, mettre à jour ou supprimer la configuration de courrier|-|-
Afficher les fournisseurs de messagerie disponibles|-|-
Créer, afficher, mettre à jour ou supprimer des modèles de courrier|-|-
Créer, mettre à jour ou supprimer des utilisateurs|-|-
Afficher les utilisateurs|-|-
Créer, mettre à jour, supprimer des invitations d'utilisateur|-|-
Afficher les invitations d'utilisateur|-|-
Terminer une invitation|-|-
Créer, mettre à jour ou supprimer des clés d'API|-|-
Afficher les clés d'API|-|-
Afficher les informations d'utilisation de l'organisation|-|-

### Opérations de contrôle d'accès {: #gateway-access-ops}

Opérations de contrôle d'accès || Rôles de passerelle|
:--------: | ---------------------|------------------------
           | **Passerelle standard** | **Passerelle privilégiée**
Afficher les propriétés utilisateur (y compris les droits d'accès)|-|-
Afficher les propriétés des utilisateurs (y compris les droits d'accès)|-|-
Gérer les utilisateurs( y compris les droits d'accès)|-|-
Afficher les propriétés de clé d'API (y compris les droits d'accès)|-|-
Afficher les propriétés des clés d'API (y compris les droits d'accès)|-|-
Créer, mettre à jour ou supprimer des clés d'API (y compris les droits d'accès)|-|-
Afficher les propriétés de terminal (y compris les droits d'accès)|X|X
Afficher les propriétés des terminaux (y compris les droits d'accès)|X|X
Créer, mettre à jour, supprimer un terminal (y compris les droits d'accès)|-|X
Afficher les rôles|-|-
Créer, mettre à jour, supprimer des rôles personnalisés|-|-
Afficher les opérations|-|-

### Opérations d'analyse {: #gateway-analytics-ops}

Opérations d'analyse || Rôles de passerelle|
:--------: | ---------------------|------------------------|
           | **Passerelle standard** | **Passerelle privilégiée** |
Afficher les règles d'analyse|-|-
Gérer les règles d'analyse|-|-
Afficher les actions d'analyse|-|-
Gérer les actions d'analyse|-|-
Afficher les alertes d'analyse|-|-
Afficher les schémas de message d'analyse|-|-
Gérer les schémas de message d'analyse|-|-

### Opérations de service de tiers {: #gateway-third-party}

Opérations de service de tiers || Rôles de passerelle|
:--------: | ---------------------|------------------------
           | **Passerelle standard** | **Passerelle privilégiée**
Traiter des notifications par lots depuis une plateforme externe|-|-
Traiter des notifications par lots et les envoyer à une plateforme externe|-|-
Publier un événement pour un terminal|-|-
S'abonner à des événements depuis un terminal|-|-
Définir une URL de rappel pour la plateforme externe|-|-
Définir le niveau d'abonnement de la plateforme externe|-|-
Obtenir l'état de santé du connecteur|-|-
Vérifier si un système externe est opérationnel et valider les données d'identification|-|-
