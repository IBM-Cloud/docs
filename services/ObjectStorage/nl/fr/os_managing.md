---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Gestion des objets

Vous pouvez utiliser l'interface de ligne de commande Swift, l'API ou l'interface Bluemix pour gérer vos objets et conteneurs.
{: shortdesc}

Avant de pouvoir gérer des objets, vous devez disposer d'une instance de service
[authentifiée](/docs/services/ObjectStorage/os_authenticate.html), [avoir
généré](/docs/services/ObjectStorage/os_credentials.html) les données d'identification du service et [configuré](/docs/services/ObjectStorage/os_configuring.html) l'interface CLi de Swift.

Gardez présents à l'esprit les points suivants lorsque vous gérez des objets :
  * Il n'y a pas de limite au volume de données que vous pouvez stocker mais chaque téléchargement ne peut pas faire plus de 5 Go. Si vous avez besoin de
télécharger des fichiers dépassant 5 Go, suivez les instructions de la rubrique
[Stockage d'objets volumineux](/docs/services/ObjectStorage/os_large_files.html).
  * Swift n'a pas de véritable structure de répertoires mais vous pouvez ajouter un [répertoire existant](/docs/services/ObjectStorage/os_directories.html) à vos commandes.
  * Pour éviter le remplacement non intentionnel d'un fichier, [configurez la fonction de gestion des objets](/docs/services/ObjectStorage/os_versioning.html).
  * Vous pouvez [planifier un moment spécifique](/docs/services/ObjectStorage/os_deletion.html) pour la suppression de vos objets.
