---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Activation des notifications utilisateur
{: #user_based_notifications}
Dernière mise à jour : 16 janvier 2017
{: .last-updated}

Les notifications de type {{site.data.keyword.mobilepushshort}} basées sur les utilisateurs sont envoyées vers les utilisateurs d'applications mobiles avec des messages personnalisés. Avec ce type de notifications, vous pouvez choisir de notifier certains individus spécifiques en fonction de leurs préférences.

## Enregistrement de l'appareil avec l'ID utilisateur
Pour activer les notifications push ciblées par ID utilisateur, prenez soin d'enregistrer l'appareil avec une zone ID utilisateur définie.     

L'ID utilisateur peut être toute chaîne fournie par l'application à l'API d'enregistrement d'appareil. Généralement, une application mobile exécute d'abord un cycle d'authentification au cours duquel l'utilisateur de l'application mobile s'authentifie auprès d'un service d'authentification tel que [{{site.data.keyword.amafull}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://console.ng.bluemix.net/docs/services/mobileaccess/index.html){: new_window}. Si l'authentification aboutit, l'ID de l'utilisateur authentifié est transféré vers l'API d'enregistrement d'appareil Push. 

## Synchronisation de la connexion et de la déconnexion utilisateur 

Vous pouvez choisir de n'envoyer des notifications que si l'utilisateur est connecté. 

Supposez par exemple qu'un appareil est partagé par les membres d'une même famille ou par une équipe au travail et qu'il est nécessaire de s'adresser uniquement à certains de ces utilisateurs. Dans un tel cas, il y aura une séquence de connexion/déconnexion. Ce mécanisme d'authentification permet à l'application d'effectuer un suivi de l'identité de l'utilisateur actuel de l'application, ce qui garantit que les notifications envoyées à un utilisateur spécifique ne sont toujours reçues que par cet utilisateur uniquement. Une fois la connexion effectuée, invoquez l'API d'enregistrement d'appareil en passant l'ID utilisateur de l'utilisateur connecté. De la même façon, avant de vous déconnecter, appelez l'API de désenregistrement de l'appareil. Le séquencement de ces API Push avec les opérations de connexion et de déconnexion garantit que les notifications destinées à un utilisateur spécifique ne sont envoyées qu'à cet utilisateur uniquement.
