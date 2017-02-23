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

# Niveaux d'accès pour les rôles d'application

Les tableaux ci-après illustrent le niveau d'accès de chacun des rôles d'application.

Les tableaux répertorient les niveaux d'accès pour :
- Les [opérations de terminal](#app-device-ops)
- Les [opérations de journal](#app-log-ops)
- Les [opérations de cache](#app-cache-ops)
<!-- [Historian Operations](#app-historian) -->
- Les [opérations d'organisation](#app-org-ops)
- Les [opérations de contrôle d'accès](#app-access-ops)
- Les [opérations d'analyse](#app-analytics-ops)
- Les [opérations de service de tiers](#app-third-party)  
<!-- - [Risk Management Operations](#app-risk-mgt) -->

## Rôles d'application
{: #app-roles}

### Opérations de terminal {: #app-device-ops}

Opérations de terminal ||| Rôles d'application||||
:--------: | -------------|-------------|---------------|-----|---
           | **Application standard** | **Application d'opérations** | **Application sécurisée de back end** | **Application de processeur de données** | **Application de visualisation** | **Application de terminal**
Créer, mettre à jour ou supprimer des terminaux|X|X|X|-|-|-
Afficher les terminaux|X|X|X|X|X|-
Activer un terminal|X|X|X|-|-|-
Publier un événement|X|-|X|-|-|X
S'abonner à un événement|X|X|X|X|X|X
Publier une commande|X|X|X|X|-|-
S'abonner à une commande|X|-|X|-|-|X
Lancer une action de gestion des terminaux|X|X|-|-|-|-
Afficher des actions de gestion des terminaux|X|X|-|-|-|X
Effacer des actions de gestion des terminaux|X|X|-|-|-|-
Gérer les regroupements d'actions de gestion des terminaux|X|X|-|-|-|-
Créer, mettre à jour ou supprimer des types de terminal|X|X|X|-|-|-
Afficher des types de terminal|X|X|X|X|-|-
Gérer les journaux de diagnostic|X|X|-|-|-|X
Afficher les journaux de diagnostic|X|X|X|-|-|-

### Opérations de journal {: #app-log-ops}

Opérations de journal ||| Rôles d'application||||
:--------: | -------------|-------------|---------------|-----|---
           | **Application standard** | **Application d'opérations** | **Application sécurisée de back end** | **Application de processeur de données** | **Application de visualisation** | **Application de terminal**
Afficher les journaux serveur|X|X|X|-|-|-

### Opérations de cache {: #app-cache-ops}

Opérations de cache ||| Rôles d'application||||
:--------: | -------------|-------------|---------------|-----|---
           | **Application standard** | **Application d'opérations** | **Application sécurisée de back end** | **Application de processeur de données** | **Application de visualisation** | **Application de terminal**
Afficher les données en temps réel (cache d'événement)|X|X|X|X|X|X
Gérer les données en temps réel (cache d'événement)|X|X|X|X|X|X

### Opérations d'organisation {: #app-org-ops}

Opérations d'organisation ||| Rôles d'application||||
:--------: | -------------|-------------|---------------|-----|---
           | **Application standard** | **Application d'opérations** | **Application sécurisée de back end** | **Application de processeur de données** | **Application de visualisation** | **Application de terminal**
Configurer les paramètres de stockage|-|-|-|-|-|-
Configurer le fournisseur d'authentification|-|-|-|-|-|-
Créer, afficher, mettre à jour ou supprimer la configuration de courrier|-|-|-|-|-|-
Afficher les fournisseurs de messagerie disponibles|X|X|-|-|-|-
Créer, afficher, mettre à jour ou supprimer des modèles de courrier|X|X|-|-|-|-
Créer, mettre à jour ou supprimer des utilisateurs|-|X|-|-|-|-
Afficher les utilisateurs|X|X|-|-|-|-
Créer, mettre à jour ou supprimer des invitations d'utilisateur|-|X|-|-|-|-
Afficher les invitations d'utilisateur|X|X|-|-|-|-
Terminer une invitation|X|X|-|-|-|-
Créer, mettre à jour ou supprimer des clés d'API|-|X|-|-|-|-
Afficher les clés d'API|X|X|-|-|-|-
Afficher les informations d'utilisation de l'organisation|X|X|-|-|-|-

### Opérations de contrôle d'accès {: #app-access-ops}

Opérations de contrôle d'accès ||| Rôles d'application||||
:--------: | -------------|-------------|---------------|-----|---
           | **Application standard** | **Application d'opérations** | **Application sécurisée de back end** | **Application de processeur de données** | **Application de visualisation** | **Application de terminal**
Afficher les propriétés utilisateur, y compris les droits d'accès|X|X|-|-|-|-
Afficher les propriétés des utilisateurs, y compris les droits d'accès|-|-|-|-|-|-
Gérer les utilisateurs, y compris les droits d'accès|-|X|-|-|-|-
Afficher les propriétés de clé d'API, y compris les droits d'accès|X|X|-|-|-|-
Afficher les propriétés de la clé d'API, y compris les droits d'accès|X|X|X|X|X|X
Créer, mettre à jour, supprimer des clés d'API, y compris les droits d'accès|-|X|-|-|-|-
Afficher les propriétés de terminal, y compris les droits d'accès|X|X|X|X|X|-
Afficher les propriétés du terminal, y compris les droits d'accès|-|-|-|-|-|-
Créer, mettre à jour, supprimer un terminal, y compris les droits d'accès|X|X|X|-|-|-
Afficher les rôles|X|X|-|-|-|-
Créer, mettre à jour, supprimer des rôles personnalisés|-|X|-|-|-|-
Afficher les opérations*|X|X|-|-|-|-

### Opérations d'analyse {: #app-analytics-ops}

Opérations d'analyse ||| Rôles d'application||||
:--------: | -------------|-------------|---------------|-----|---
           | **Application standard** | **Application d'opérations** | **Application sécurisée de back end** | **Application de processeur de données** | **Application de visualisation** | **Application de terminal**
Afficher les règles d'analyse|X|X|-|X|X|-
Gérer les règles d'analyse|X|X|-|X|-|-
Afficher les actions d'analyse|X|X|-|X|X|-
Gérer les actions d'analyse|X|X|-|X|X|-
Afficher les alertes d'analyse|X|X|-|X|X|X
Afficher les schémas de message d'analyse|X|X|-|X|X|-
Gérer les schémas de message d'analyse|X|X|-|X|-|-

### Opérations de service de tiers {: #app-third-party}

Opérations de service de tiers ||| Rôles d'application||||
:--------: | -------------|-------------|---------------|-----|---
           | **Application standard** | **Application d'opérations** | **Application sécurisée de back end** | **Application de processeur de données** | **Application de visualisation** | **Application de terminal**
Traiter des notifications par lots depuis une plateforme externe|X|X|-|-|-|-
Traiter des notifications par lots et les envoyer à une plateforme externe|X|X|-|-|-|-
Publier un événement pour un terminal|X|X|-|-|-|-
S'abonner à des événements depuis un terminal|X|X|-|-|-|-
Définir une URL de rappel pour la plateforme externe|X|X|-|-|X|-
Définir le niveau d'abonnement de la plateforme externe|X|X|-|-|X|-
Obtenir l'état de santé du connecteur|X|X|X|-|X|-
Vérifier si un système externe est opérationnel et valider les données d'identification|X|X|X|-|X|-
