---

copyright:

  years: 2017

lastupdated: "2017-05-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Plug-in d'interface de ligne de commande de {{site.data.keyword.bpshort}} pour l'interface de ligne de commande de {{site.data.keyword.Bluemix_notm}} 
{: #cli}

Servez-vous des commandes {{site.data.keyword.bpshort}} pour l'interface de ligne de commande de {{site.data.keyword.Bluemix}} afin de gérer vos environnements et d'effectuer d'autres opérations dans {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

Avant d'utiliser les commandes d'interface de ligne de commande : 

* Connectez-vous à {{site.data.keyword.Bluemix_notm}} avec `bx login [--sso]` pour authentifier votre session. Les utilisateurs qui possèdent un ID fédéré doivent utiliser l'indicateur `--sso` pour gérer un code d'accès unique. 

Pour afficher la liste des commandes, vous pouvez exécuter `bx schematics help`.

<table id="manage_environments" summary="Gérez vos environnements avec les commandes bx schematics environment.">
<caption>Tableau 1. Commandes disponibles pour gérer votre environnement. Les commandes respectent la syntaxe <code>bx schematics environment</code>.
</caption>
 <thead>
 <th colspan="5">Gestion de votre environnement</th>
 </thead>
 <tbody>
 <tr>
 <td>[bx schematics environment create](#environment-create)</td>
 <td>[bx schematics environment delete](#environment-delete)</td>
 <td>[bx schematics environment list](#environment-list)</td>
 <td>[bx schematics environment show](#environment-show)</td>
 <td>[bx schematics environment update](#environment-update)</td>
 </tr>
</tbody></table>
 
 <table id="update_resources" summary="Mettez à jour les ressources mises à disposition par votre environnement avec les commandes bx schematics action.">
 <caption>Tableau 2. Commandes disponibles pour mettre à jour des ressources dans votre environnement. Les commandes respectent la syntaxe <code>bx schematics action</code>.
 </caption>
  <thead>
  <th colspan="5">Mise à jour de vos ressources </th>
  </thead>
  <tbody>
  <td>[bx schematics action apply](#action-apply)</td>
  <td>[bx schematics action destroy](#action-destroy)</td>
  <td>[bx schematics action plan](#action-plan)</td>
  </tr></tbody></table>
  
  <table id="audit_environment" summary="Audit d'activités exécutées pour votre environnement avec les commandes bx schematics activity.">
  <caption>Tableau 3. Commandes disponibles pour auditer les activités que vous avez exécutées pour votre environnement. Les commandes respectent la syntaxe <code>bx schematics activity</code>.
  </caption>
   <thead>
   <th colspan="5">Audit de votre environnement </th>
   </thead>
   <tbody>
   <td>[bx schematics activity list](#activity-list)</td>
   <td>[bx schematics activity log](#activity-log)</td>
   <td>[bx schematics activity planfile](#activity-planfile)</td>
   <td>[bx schematics activity show](#activity-show)</td>
   </tr></tbody></table>

## bx schematics environment create
{: #environment-create notoc}

Créez un environnement dans {{site.data.keyword.Bluemix_notm}} à partir de votre configuration.

```
bx schematics environment create --file NOM_FICHIER [--json]
```
{: codeblock}

### Paramètres 

<dl>
<dt>--file NOM_FICHIER </dt>
<dd>Fichier JSON utilisé pour transmettre des détails sur votre environnement.
<p>
<p>Exemple de fichier JSON avec toutes les valeurs disponibles :
<pre>{
    "description": "(Optional) Description of the environment",
    "frozen": false,
    "name": "Name of the environment",
    "sourceurl": "The GitHub URL that points to the Terraform configuration",
    "tags": ["(Optional) metadata_tag_1", "(Optional) metadata_tag_2"],
    "terraformversion": "0.9",
    "variablestore": [{
        "name": "(Optional) variable_1",
        "secure": false,
        "value": "Visible value"
    },
    {
        "name": "(Optional) variable_2_secret",
        "secure": true,
        "value": "Secured value"
    }]
}</pre></dd>
<dt>--json</dt>
<dd>Affichez la sortie au format JSON. </dd>
</dl>

## bx schematics environment delete
{: #environment-delete notoc}

Supprimez votre configuration d'environnement dans {{site.data.keyword.Bluemix_notm}}. Cette commande est recommandée uniquement pour les environnements dans lesquels aucune ressource n'est en cours d'exécution. Si vous supprimez un environnement comportant des ressources en cours d'exécution, vous devrez gérer chaque ressource dans les tableaux de bord de service individuels. 

```
bx schematics environment delete --id ID_ENVIRONNEMENT [--force]
```
{: codeblock}

### Paramètres 

<dl>
<dt>--id ID_ENVIRONNEMENT </dt>
<dd>Identificateur unique de l'environnement. Vous pouvez extraire cette valeur en exécutant <code>bx schematics environment list</code>.</dd>
<dt>--force</dt>
<dd>Forcez la progression de la commande sans confirmation (oui ou non). </dd>
</dl>

## bx schematics environment list
{: #environment-list notoc}

Procédez à l'extraction de la liste de tous les environnements existants sur votre compte {{site.data.keyword.Bluemix_notm}}. 

```
bx schematics environment list [--count VALEUR] [--offset VALEUR] [--json]
```
{: codeblock}

### Paramètres 
<dl>
<dt>--count VALEUR </dt>
<dd>Limitez le nombre d'environnements dans votre retour. </dd>
<dt>--offset VALEUR </dt>
<dd>Décalage dans la liste d'environnements. </dd>
<dt>--json</dt>
<dd>Affichez la sortie au format JSON. </dd>
</dl>

## bx schematics environment show
{: #environment-show notoc}

Procédez à l'extraction de détails sur un environnement existant.

```
bx schematics environment show --id ID_ENVIRONNEMENT [--json]
```
{: codeblock}

### Paramètres 
<dl>
<dt>--id ID_ENVIRONNEMENT </dt>
<dd>Identificateur unique de l'environnement. Vous pouvez extraire cette valeur en exécutant <code>bx schematics environment list</code>.</dd>
<dt>--json</dt>
<dd>Affichez la sortie au format JSON. </dd>
</dl>
  
## bx schematics environment update
{: #environment-update notoc}

Mettez à jour les détails d'un environnement existant, comme son nom ou l'adresse URL de GitHub. Pour mettre à jour le nombre de ressources qui sont allouées dans l'environnement, voir [bx schematics action plan](#action-plan).

```
bx schematics environment update --id ID_ENVIRONNEMENT --file NOM_FICHIER [--json]
```
{: codeblock}

### Paramètres 
<dl>
<dt>--id ID_ENVIRONNEMENT </dt>
<dd>Identificateur unique de l'environnement. Vous pouvez extraire cette valeur en exécutant <code>bx schematics environment list</code>.</dd>
<dt>--file NOM_FICHIER </dt>
<dd>Fichier JSON utilisé pour transmettre des détails sur votre environnement.
Voir [bx schematics environment create](#environment-create) pour un exemple de fragment JSON avec des valeurs admises. </dd>
<dt>--json</dt>
<dd>Affichez la sortie au format JSON. </dd>
</dl>

## bx schematics action apply
{: #action-apply notoc}

Déployez votre configuration d'environnement. La commande `apply` analyse et exécute les configurations qui sont stockées dans votre référentiel GitHub. 

```
bx schematics action apply --id ID_ENVIRONNEMENT [--force] [--json]
```
{: codeblock}

### Paramètres 
<dl>
<dt>--id ID_ENVIRONNEMENT </dt>
<dd>Identificateur unique de l'environnement. Vous pouvez extraire cette valeur en exécutant <code>bx schematics environment list</code>.</dd>
<dt>--force</dt>
<dd>Forcez la progression de la commande sans confirmation (oui ou non). </dd>
<dt>--json</dt>
<dd>Affichez la sortie de l'application au format JSON. </dd>
</dl>

## bx schematics action destroy
{: #action-destroy notoc}

Détruisez votre environnement et vos ressources. La commande `destroy` supprime votre environnement, y compris les ressources en cours d'exécution. En général, cette action est utilisée pour les environnements temporaires seulement, comme les environnements d'assurance qualité, afin de garder l'environnement actif pour une durée limitée. Il n'est pas recommandé de détruire des environnements de production. L'action `destroy` est irréversible et doit être utilisée avec précaution. 

```
bx schematics action destroy --id ID_ENVIRONNEMENT [--force] [--json]
```
{: codeblock}

### Paramètres 
<dl>
<dt>--id ID_ENVIRONNEMENT </dt>
<dd>Identificateur unique de l'environnement. Vous pouvez extraire cette valeur en exécutant <code>bx schematics environment list</code>.</dd>
<dt>--force</dt>
<dd>Forcez la progression de la commande sans confirmation (oui ou non). </dd>
<dt>--json</dt>
<dd>Affichez la sortie de la destruction au format JSON. </dd>
</dl>
</dl>

## bx schematics action plan
{: #action-plan notoc}

Comparez votre configuration d'environnement à la configuration déployée. La commande `plan` analyse la configuration dans votre référentiel GitHub et la compare au fichier d'état qui est associé à votre environnement déployé. La sortie du plan indique les ressources qui seront ajoutées ou retirées si vous déployez votre configuration d'environnement avec la commande `apply`.  

```
bx schematics action plan --id ID_ENVIRONNEMENT [--file NOM_FICHIER] [--json]
```
{: codeblock}

### Paramètres 
<dl>
<dt>--id ID_ENVIRONNEMENT </dt>
<dd>Identificateur unique de l'environnement. Vous pouvez extraire cette valeur en exécutant <code>bx schematics environment list</code>.</dd>
<dt>--file NOM_FICHIER </dt>
<dd>Fichier JSON facultatif utilisé pour transmettre des paramètres à l'action de plan. Vous pouvez transmettre le paramètre <code>sourcesha</code> afin de référencer une branche Git spécifique pour la configuration Terraform de l'environnement. La
branche Git doit être spécifiée comme référence principale, par exemple
<code>refs/heads/NOM_BRANCHE</code>. Si
aucun paramètre n'est spécifié, la valeur par défaut est la tête (référence principale)
de la branche maître, c'est-à-dire <code>refs/heads/master</code>.
<p>
<p>Exemple de fragment JSON avec une valeur :
<pre>{
  "sourcesha": "refs/heads/NOM_BRANCHE"
}</pre></dd>
<dt>--json</dt>
<dd>Affichez la sortie du plan au format JSON. </dd>
</dl>

## bx schematics activity list
{: #activity-list notoc}

Répertoriez les données des activités Terraform qui ont été exécutées pour un environnement. 

```
bx schematics activity list --id ID_ENVIRONNEMENT [--count VALEUR] [--offset VALEUR] [--json]
```
{: codeblock}

### Paramètres 
<dl>
<dt>--id ID_ENVIRONNEMENT </dt>
<dd>Identificateur unique de l'environnement. Vous pouvez extraire cette valeur en exécutant <code>bx schematics environment list</code>.</dd>
<dt>--count VALEUR </dt>
<dd>Nombre d'activités à renvoyer. </dd>
<dt>--offset VALEUR </dt>
<dd>Décalage dans la liste.</dd>
<dt>--json</dt>
<dd>Affichez la sortie du plan au format JSON. </dd>
</dl>

## bx schematics activity log
{: #activity-log notoc}

Affichez des journaux d'activité détaillés pour les actions qui sont exécutées pour un environnement. 

```
  bx schematics activity log --id ID_ACTIVITE
  ```
{: codeblock}

### Paramètres 
<dl>
<dt>--id ID_ACTIVITE </dt>
<dd>Indicateur permettant de renvoyer des détails sur une activité spécifique. Vous pouvez extraire une liste d'ID d'activité par environnement avec la commande <code>bx schematics activity list --id ID_ENVIRONNEMENT</code>. </dd>
</dl>

## bx schematics activity planfile
{: #activity-planfile notoc}

Affichez des fichiers de plan pour un environnement. 

```
bx schematics activity planfile --id ID_ACTIVITE
```
{: codeblock}

### Paramètres 
<dl>
<dt>--id ID_ACTIVITE </dt>
<dd>Indicateur permettant de renvoyer des détails sur une activité spécifique. Vous pouvez extraire une liste d'ID d'activité par environnement avec la commande <code>bx schematics activity list --id ID_ENVIRONNEMENT</code>. </dd>
</dl>

## bx schematics activity show
{: #activity-show notoc}

Procédez à l'extraction de détails sur une activité spécifique qui a été exécutée pour un environnement. 

```
bx schematics activity show --id ID_ACTIVITE [--json]
```
{: codeblock}

### Paramètres 
<dl>
<dt>--id ID_ACTIVITE </dt>
<dd>Indicateur permettant de renvoyer des détails sur une activité spécifique. Vous pouvez extraire une liste d'ID d'activité par environnement avec la commande <code>bx schematics activity list --id ID_ENVIRONNEMENT</code>. </dd>
<dt>--json</dt>
<dd>Affichez la sortie du plan au format JSON. </dd>
</dl>
