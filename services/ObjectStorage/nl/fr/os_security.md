---

copyright:
  years: 2014, 2016
lastupdated: "2016-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}



# Gestion des accès

Les listes de contrôle d'accès peuvent être utilisées pour gérer l'accès au service. Les [administrateurs](/docs/services/ObjectStorage/os_access_types.html) peuvent accorder un accès en lecture et en écriture, et également retirer l'accès lors de la gestion de votre instance de service.
{: shortdesc}


Les listes de contrôle d'accès peuvent être gérées en utilisant l'interface de ligne de commande Swift ou l'interface utilisateur Bluemix. Avant de gérer les accès, assurez-vous d'avoir configuré le service et commencé à stocker des objets. Gardez à l'esprit les remarques ci-dessous quand vous gérez les accès.
  * Quand un utilisateur crée un conteneur, il se voit automatiquement accorder les privilèges d'administrateur à ce conteneur.
  * Les listes de contrôle d'accès ne sont pas disponibles pour l'instance de service, le compte de stockage ou au niveau du projet. L'accès ne peut être géré qu'au niveau du conteneur.
  * Prenez soin de vérifier que l'accès à un conteneur a été [retiré](/docs/services/ObjectStorage/os_remove_access.html).
