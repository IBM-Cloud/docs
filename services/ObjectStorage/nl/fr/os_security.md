---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}



# Gestion des accès

Les listes de contrôle d'accès peuvent être utilisées pour gérer l'accès au service. [Les
administrateurs](/docs/services/ObjectStorage/os_access_types.html) peuvent accorder un accès en lecture et en écriture ainsi que supprimer les droits d'accès.
{: shortdesc}

Avant de gérer les accès depuis l'interface utilisateur ou l'interface CLI de Swift, vérifiez que vous avez configuré le service et commencé à gérer des
objets.

Si vous utilisez des listes de contrôle d'accès, gardez présents à l'esprit les points suivants :
  * Quand un utilisateur crée un conteneur, il se voit automatiquement accorder les privilèges d'administrateur à ce conteneur.
  * Les listes de contrôle d'accès ne sont pas disponibles pour l'instance de service, le compte de stockage ou au niveau du projet. L'accès ne peut être
géré qu'au niveau du conteneur ou de l'objet.
  * Vérifiez que l'accès à un conteneur a été [supprimé](/docs/services/ObjectStorage/os_remove_access.html).
