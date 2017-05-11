---



copyright:

  years: 2017

lastupdated: "2017-04-07"


---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Interface de ligne de commande d'{{site.data.keyword.registrylong_notm}}
{: #containerregcli}

L'interface CLI d'{{site.data.keyword.registrylong}} est un plug-in qui vous permet de gérer votre registre de ressources, telles que des espaces de nom et les images, dans votre organisation.
{: shortdesc}

**Prérequis**
* Avant d'exécuter des commandes de registre, connectez-vous à {{site.data.keyword.Bluemix_short}} avec la commande `bx login` pour générer un jeton d'accès {{site.data.keyword.Bluemix_short}} et authentifier votre session.

<table summary="Gestion de votre registre Containers Registry">
<caption>Tableau 1. Commandes de gestion de {{site.data.keyword.registryshort}} sur {{site.data.keyword.Bluemix_short}}
</caption>
 <thead>
 <th colspan="5">Commandes de gestion du registre</th>
 </thead>
 <tbody>
 <tr>
 <td>[bx cr api](#bx-cr-api)</td>
 <td>[bx cr info](#bx-cr-info)</td>
 <td>[bx cr image-inspect](#bx-cr-image-inspect)</td>
 <td>[bx cr image-list](#bx-cr-image-list)</td>
 <td>[bx cr image-rm](#bx-cr-image-rm)</td>
 </tr>
 <tr>
 <td>[bx cr login](#bx-cr-login)</td>
 <td>[bx cr namespace-add](#bx-cr-namespace-add)</td>
 <td>[bx cr namespace-list](#bx-cr-namespace-list)</td>
 <td>[bx cr namespace-rm](#bx-cr-namespace-rm)</td>
 </tr></tbody></table>


## bx cr api
Renvoie les informations sur le noeud final de l'API de registre face auquel les commandes sont exécutées.

```
bx cr api
```
{: codeblock}


## bx cr info
Affiche le nom et l'organisation du registre à laquelle vous êtes connecté.

```
bx cr info
```
{: codeblock}


## bx cr image-inspect
Affiche des informations détaillées sur une image spécifique.

```
bx cr image-inspect [--format FORMAT] IMAGE [IMAGE]
```
{: codeblock}

**Paramètres**
<dl>
<dt>--format FORMAT</dt>
<dd>(Facultatif) Formate la sortie en utilisant un modèle Go.</dd>
<dt>IMAGE</dt>
<dd>Chemin de registre {{site.data.keyword.Bluemix_short}} complet vers l'image que vous désirez inspecter, au format namespace/image:tag. Si aucune balise n'est spécifiée dans le chemin de l'image, celle portant la balise `latest` (dernière) est inspectée. Vous pouvez inspecter plusieurs images en listant dans la commande chaque chemin de registre {{site.data.keyword.Bluemix_short}} privé et en les séparant par un espace.</dd>
</dl>


## bx cr image-list
Liste toutes les images dans votre organisation {{site.data.keyword.Bluemix_short}}.

```
 bx cr image-list [--no-trunc] [-q, --quiet] [--include-ibm] [--format FORMAT]
```
{: codeblock}

**Paramètres**
<dl>
<dt>--no-trunc</dt>
<dd>(Facultatif) Ne pas tronquer la sortie.</dd>
<dt>-q, --quiet</dt>
<dd>(Facultatif) Affiche l'identificateur unique de l'image au format : 'référentiel:balise'.</dd>
<dt>--include-ibm</dt>
<dd>(Facultatif) Inclut dans la sortie les images publiques fournies par IBM. Sans cette option, seules les images privées sont répertoriées.</dd>
<dt>--format FORMAT</dt>
<dd>(Facultatif) Formate la sortie en utilisant un modèle Go.</dd>
</dl>


## bx cr image-rm
Supprime de votre registre l'image spécifiée.

```
bx cr image-rm IMAGE [IMAGE]
```
{: codeblock}

**Paramètres**
<dl>
<dt>IMAGE</dt>
<dd>Chemin de registre {{site.data.keyword.Bluemix_short}} complet vers l'image que vous désirez supprimer, au format namespace/image:tag. Si une balise n'est pas spécifiée dans le chemin de l'image,
celle associée à la balise `latest` (dernière) est supprimée par défaut. Vous pouvez supprimer plusieurs images en listant dans la commande chaque chemin de registre {{site.data.keyword.Bluemix_short}} privé et en les séparant par un espace.</dd>
</dl>


## bx cr login
Si Docker est installé, cette commande exécute la commande `docker login` face au registre. La commande `docker login` est requise pour pouvoir exécuter les commandes `docker push` ou `docker pull` pour le registre. Cette commande n'est pas requise pour exécuter d'autres commandes `bx cr`. Si Docker n'est pas installé, cette commande renvoie un message d'erreur.

```
bx cr login
```
{: codeblock}


## bx cr namespace-add
Ajoute un espace de nom dans votre organisation Bluemix. 

```
bx cr namespace-add ESPACE DE NOM
```
{: codeblock}

**Paramètres**
<dl>
<dt>ESPACE DE NOM</dt>
<dd>Espace de nom que vous désirez ajouter. Cet espace de nom doit être unique à travers toutes les organisations {{site.data.keyword.Bluemix_short}}.</dd>
</dl>


## bx cr namespace-list
Répertorie tous les espaces de nom de votre organisation {{site.data.keyword.Bluemix_short}}.

```
bx cr namespace-list
```
{: codeblock}


## bx cr namespace-rm
Supprime un espace de nom dans votre organisation {{site.data.keyword.Bluemix_short}}. Les images dans cet espace de nom sont supprimées en même temps que l'espace de nom.

```
bx cr namespace-rm ESPACE DE NOM
```
{: codeblock}

**Paramètres**
<dl>
<dt>ESPACE DE NOM</dt>
<dd>Espace de nom que vous désirez supprimer.</dd>
</dl>
