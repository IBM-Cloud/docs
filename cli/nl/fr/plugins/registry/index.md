---



copyright:

  years: 2017

lastupdated: "2017-05-12"


---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Interface de ligne de commande d'{{site.data.keyword.registrylong_notm}}
{: #containerregcli}

L'interface de ligne de commande {{site.data.keyword.registrylong}} est un plug-in qui vous permet de gérer votre registre et ses ressources pour votre compte.
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
 <td>[bx cr api](#bx_cr_api)</td>
 <td>[bx cr info](#bx-cr-info)</td>
 <td>[bx cr image-inspect](#bx-cr-image-inspect)</td>
 <td>[bx cr image-list (bx cr images)](#bx-cr-image-list)</td>
 <td>[bx cr image-rm](#bx-cr-image-rm)</td>
 </tr>
 <tr>
 <td>[bx cr login](#bx-cr-login)</td>
 <td>[bx cr namespace-add](#bx-cr-namespace-add)</td>
 <td>[bx cr namespace-list (bx cr namespaces)](#bx-cr-namespace-list)</td>
 <td>[bx cr namespace-rm](#bx-cr-namespace-rm)</td>
 <td>[bx cr token-add](#bx-cr-token-add)</td>
 </tr>
 <tr>
 <td>[bx cr token-get](#bx-cr-token-get)</td>
 <td>[bx cr token-list (bx cr tokens)](#bx-cr-token-list)</td>
 <td>[bx cr token-rm](#bx-cr-token-rm)</td>
 </tr>
 </tbody></table>



## bx cr api
{: #bx_cr_api}

Renvoie les informations sur le noeud final de l'API de registre face auquel les commandes sont exécutées.

```
bx cr api
```
{: codeblock}


## bx cr info
Affiche le nom et le compte du registre auquel vous êtes connecté. 

```
bx cr info
```
{: codeblock}


## bx cr image-inspect
Affiche les détails d'une image spécifique. 

```
bx cr image-inspect [--format FORMAT] IMAGE [IMAGE]
```
{: codeblock}

**Paramètres**


<dl>
<dt>--format FORMAT</dt>
<dd>(Facultatif) Formate la sortie en utilisant un modèle Go. 


</dd>
<dt>IMAGE</dt>
<dd>Chemin de registre {{site.data.keyword.Bluemix_short}} complet vers l'image à inspecter, au format `espace_de_nom/image:balise`. Si aucune balise n'est spécifiée dans le chemin de l'image, celle portant la balise `latest` (dernière) est inspectée. Vous pouvez inspecter plusieurs images en listant dans la commande chaque chemin de registre {{site.data.keyword.Bluemix_short}} privé et en les séparant par un espace.</dd>
</dl>


## bx cr image-list (bx cr images)
Affiche toutes les images de votre compte {{site.data.keyword.Bluemix_short}}. 

```
 bx cr image-list [--no-trunc] [-q, --quiet] [--include-ibm] [--format FORMAT]
```
{: codeblock}

**Paramètres**
<dl>
<dt>--no-trunc</dt>
<dd>(Facultatif) Permet de ne pas tronquer l'historique des images. </dd>
<dt>-q, --quiet</dt>
<dd>(Facultatif) Chaque image est répertoriée au format `référentiel:balise`.</dd>
<dt>--include-ibm</dt>
<dd>(Facultatif) Inclut dans la sortie les images publiques fournies par IBM. Sans cette option, seules les images privées sont répertoriées par défaut. </dd>
<dt>--format FORMAT</dt>
<dd>(Facultatif) Formate la sortie en utilisant un modèle Go. 


</dd>

</dl>


## bx cr image-rm
Supprime une ou plusieurs images spécifiées de votre registre. 

```
bx cr image-rm IMAGE [IMAGE]
```
{: codeblock}

**Paramètres**
<dl>
<dt>IMAGE</dt>
<dd>Chemin de registre {{site.data.keyword.Bluemix_short}} complet vers l'image à retirer, au format `espace_de_nom/image:balise`. Si une balise n'est pas spécifiée dans le chemin de l'image,
celle associée à la balise `latest` (dernière) est supprimée par défaut. Vous pouvez supprimer plusieurs images en listant dans la commande chaque chemin de registre {{site.data.keyword.Bluemix_short}} privé et en les séparant par un espace.</dd>
</dl>


## bx cr login
Cette commande exécute la commande `docker login` sur le registre. La commande `docker login` est requise pour pouvoir exécuter les commandes `docker push` ou `docker pull` pour le registre. Cette commande n'est pas requise pour exécuter d'autres commandes `bx cr`. Si Docker n'est pas installé, cette commande renvoie un message d'erreur.

```
bx cr login
```
{: codeblock}


## bx cr namespace-add
Ajoute un espace de nom à votre compte {{site.data.keyword.Bluemix_short}}. 

```
bx cr namespace-add ESPACE DE NOM
```
{: codeblock}

**Paramètres**
<dl>
<dt>ESPACE DE NOM</dt>
<dd>Espace de nom à ajouter. Il doit être unique sur tous les comptes {{site.data.keyword.Bluemix_short}} d'une même région. </dd>
</dl>


## bx cr namespace-list (bx cr namespaces)
Affiche tous les espaces de nom détenus par votre compte {{site.data.keyword.Bluemix_short}}. 

```
bx cr namespace-list
```
{: codeblock}


## bx cr namespace-rm
Retire un espace de nom de votre compte {{site.data.keyword.Bluemix_short}}. Les images dans cet espace de nom sont supprimées lorsque l'espace de nom est retiré. 

```
bx cr namespace-rm ESPACE DE NOM
```
{: codeblock}

**Paramètres**
<dl>
<dt>ESPACE DE NOM</dt>
<dd>Espace de nom que vous désirez supprimer.</dd>
</dl>


## bx cr token-add
Ajoute un jeton que vous pouvez utiliser pour contrôler l'accès à un registre. 

```
bx cr token-add [--description VALEUR] [-q, --quiet] [--non-expiring] [--readwrite]
```

{: codeblock}


**Paramètres**
<dl>
<dt>--description VALEUR </dt>
<dd>(Facultatif) Permet de spécifier la description du jeton qui s'affiche lorsque vous exécutez `bx cr token-list`. Si votre jeton est créé automatiquement par IBM Bluemix Container Service, la description est le nom de votre cluster Kubernetes. Dans ce cas, le jeton est retiré automatiquement lorsque votre cluster est retiré. </dd>
<dt>-q, --quiet</dt>
<dd>(Facultatif) Affiche le jeton uniquement, sans aucun autre texte. </dd>
<dt>--non-expiring</dt>
<dd>(Facultatif) Crée un jeton dont l'accès n'expire jamais. Si ce paramètre n'est pas défini, l'accès à l'aide d'un jeton expire au bout de 24 heures par défaut. </dd>
<dt>--readwrite</dt>
<dd>(Facultatif) Crée un jeton qui accorde l'accès en lecture et en écriture. Sans cette option, l'accès est en lecture seule par défaut. </dd>
</dl>


## bx cr token-get
Extrait le jeton spécifié du registre. 

```
bx cr token-get JETON
```

{: codeblock}

**Paramètres**
<dl>
<dt>JETON </dt>
<dd>(Facultatif) Identificateur unique du jeton à extraire. </dd>
</dl>


## bx cr token-list (bx cr tokens)
Affiche tous les jetons qui existent pour votre compte {{site.data.keyword.Bluemix_short}}. 

```
bx cr token-list --format FORMAT
```
{: codeblock}

**Paramètres**
<dl>
<dt>--format FORMAT</dt>
<dd>(Facultatif) Formate la sortie en utilisant un modèle Go. 


</dd>
</dl>


## bx cr token-rm
Retire un ou plusieurs jetons spécifiés. 

```
bx cr token-rm JETON [JETON]
```
{: codeblock}

**Paramètres**
<dl>
<dt>JETON </dt>
<dd>(Facultatif) JETON peut correspondre au jeton lui-même ou à l'identificateur unique du jeton, comme indiqué dans `bx cr token-list`. Vous pouvez spécifier plusieurs jetons en les séparant par un espace. </dd>
</dl>


</dd>
</dl>


