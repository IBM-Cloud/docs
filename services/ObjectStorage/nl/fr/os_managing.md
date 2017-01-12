---

copyright:
  years: 2014, 2016
lastupdated: "2016-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Gestion des objets

Vous pouvez utiliser l'interface de ligne de commande Swift, l'API ou l'interface Bluemix pour gérer vos objets et conteneurs.
{: shortdesc}

Avant de pouvoir gérer les objets, vous devez avoir procédé aux opérations suivantes : authentification de votre instance de service, génération des données d'identification de service et configuration de l'interface de ligne de commande Swift.

Vous pouvez stocker, télécharger et supprimer des objets quand vous utilisez le service. Gardez à l'esprit les informations ci-après quand vous gérez vos objets.
  * Il n'y a pas de limite au volume de données que vous pouvez stocker mais chaque téléchargement ne peut pas faire plus de 5 Go. Si vous avez besoin de télécharger des fichiers supérieurs à 5 Go, suivez la procédure décrite dans [Stockage d'objets volumineux](/docs/services/ObjectStorage/os_large_files.html).
  * Swift n'a pas de véritable structure de répertoires mais vous pouvez ajouter un [répertoire existant](/docs/services/ObjectStorage/os_directories.html) à vos commandes.
  * Pour éviter le remplacement non intentionnel d'un fichier, [configurez la fonction de gestion des objets](/docs/services/ObjectStorage/os_versioning.html).
  * Vous pouvez [planifier un moment spécifique](/docs/services/ObjectStorage/os_deletion.html) pour la suppression de vos objets.
