---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Utilisation de répertoires

Swift n'a pas de véritable structure de répertoires mais utilise la convention d’affectation de noms pour représenter la disposition d'un répertoire. Si vous spécifiez un nom de répertoire, il est attaché à tous les noms de fichier en tant qu'élément du chemin relatif.
{: shortdesc}

## Ajout d'un répertoire à un conteneur avec Swift CLI

Pour ajouter un répertoire dans un conteneur, vous devez avoir la structure de répertoire à la place de votre unité locale.

1. Créez un répertoire local et enregistrez votre fichier.
2. Lancez la commande suivante pour télécharger un répertoire dans votre conteneur.

    ```
    swift upload <nom_conteneur> <nom_répertoire>
    ```
    {: pre}

## Téléchargement d'un répertoire avec l'interface de ligne de commande
Pour télécharger une structure de répertoire, utilisez le paramètre `-prefix` pour indiquer le répertoire ou la structure de répertoire que vous voulez charger.

1. Lancez la commande suivante pour télécharger un répertoire.

    ```
    swift download <nom_conteneur> --prefix <répertoire>
    ```
    {: pre}
