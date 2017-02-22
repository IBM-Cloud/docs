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

# Téléchargement d'objets

Vous pouvez télécharger vos objets stockés pour les examiner ou les éditer via l'interface utilisateur ou l'interface de ligne de commande.
{: shortdesc}


## Téléchargement d'objets depuis l'interface utilisateur {: #downloading-ui}

1. Pour empêcher une destruction des données par un remplacement non intentionnel, [configurez la fonction de gestion des versions d'objets](/docs/services/ObjectStorage/os_versioning.html). Si vous ne voulez pas mettre en place cette fonction, renommez le répertoire ou les fichiers avant le téléchargement, si nécessaire.
2. Dans votre tableau de bord d'instance de service, sélectionnez le conteneur avec le fichier que vous voulez télécharger.
3. Sélectionnez le fichier.
4. Dans le menu déroulant **Actions**, sélectionnez **Télécharger le fichier**.


## Téléchargement d'objets avec Swift CLI {: #downloading-cli}

1.  Si vous n'êtes pas connecté à {{site.data.keyword.Bluemix_notm}}, connectez-vous à l'organisation et l'espace contenant votre instance d'{{site.data.keyword.objectstorageshort}}.

```
cf login -a api.ng.bluemix.net -u <ID_utilisateur> -p <mot_de_passe> -o <organisation> -s <space>
```
{: pre}

2. Pour empêcher une destruction des données par un remplacement non intentionnel, [configurez la fonction de gestion des versions d'objets](/docs/services/ObjectStorage/os_versioning.html). Si vous ne voulez pas mettre en place cette gestion, répertoriez les fichiers existants dans votre magasin et, si nécessaire, renommez le répertoire ou les fichiers avant la réception par téléchargement.

3. Téléchargez un fichier en exécutant la commande suivante :

```
swift download <nom_conteneur> <nom_fichier>
```
{: pre}
