---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Stockage d'objets

Vous pouvez télécharger des objets dans l'espace de stockage via l'interface utilisateur ou l'interface de ligne de commande. Le téléchargement des objets est limité à une taille maximale de 5 Go par téléchargement. Vous pouvez toutefois télécharger des objets plus volumineux en les segmentant en objets plus petits.
{: shortdesc}


## Stockage d'objets dans des conteneurs via l'interface utilisateur {: #storing-ui}

**Remarque **: quand vous téléchargez un fichier portant le même nom qu'un fichier existant, {{site.data.keyword.objectstorageshort}} remplace le fichier stocké par le nouveau fichier. Si vous téléchargez un fichier puis l'éditez, prenez soin de donner un autre nom au fichier ou [configurez la fonction de gestion des versions d'objets](/docs/services/ObjectStorage/os_versioning.html) avant de procéder au téléchargement pour conserver les deux versions du fichier.


1. Depuis votre tableau de bord d'instance de service, ajoutez un conteneur à partir du menu déroulant **Actions**.
2. Nommez votre conteneur et cliquez sur **CREER**.
3. Depuis le menu déroulant **Actions**, sélectionnez la commande d'ajout de fichiers. Une boîte de dialogue s'ouvre.
4. Sélectionnez le ou le fichiers que vous voulez téléchargez puis cliquez sur **Ouvrir**.



## Stockage d'objets dans des conteneurs via l'interface de ligne de commande {: #storing-cli}

1. Si vous n'êtes pas connecté à {{site.data.keyword.Bluemix_notm}}, connectez-vous à l'organisation et l'espace contenant votre instance d'{{site.data.keyword.objectstorageshort}}.

  ```
  cf login -a api.ng.bluemix.net -u <ID_utilisateur> -p <mot_de_passe> -o <organisation> -s <space>
  ```
  {: pre}

2. Créez un conteneur {{site.data.keyword.objectstorageshort}} en exécutant la commande suivante. Vous y définissez par la même occasion la variable
*nom_conteneur*.

  ```
  swift post <nom_conteneur>
  ```
  {: pre}

**Remarque **: Si vous recevez un message d'erreur, vérifiez que les
[logiciels prérequis](/docs/services/ObjectStorage/os_configuring.html#install-swift-client) ont été installés.

3. Facultatif - pour vérifier que votre conteneur a été créé, exécutez la commande suivante pour répertorier vos conteneurs.

  ```
  swift list
  ```
  {: pre}

4. Pour empêcher une destruction des données par un remplacement non intentionnel, [configurez la fonction de gestion des versions d'objets](/docs/services/ObjectStorage/os_versioning.html). Si vous ne voulez pas mettre en place cette gestion, répertoriez les fichiers existants dans votre magasin et, si nécessaire, renommez le répertoire ou les fichiers avant l'envoi par téléchargement.

5. Téléchargez un fichier dans votre conteneur en exécutant la commande suivante.

  ```
  swift upload <nom_conteneur> <nom_fichier>
  ```
  {: pre}

  **Remarque** : pour télécharger des fichiers qui font plus de 5 Go, des [étapes supplémentaires sont nécessaires](/docs/services/ObjectStorage/os_large_files.html).

6. (Facultatif) - pour vérifier que le chargement a abouti, affichez le contenu de votre conteneur en exécutant la commande suivante.

  ```
  swift list <nom_conteneur>
  ```
  {: pre}
