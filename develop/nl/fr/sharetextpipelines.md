---

copyright:
  years: 2015, 2017
lastupdated: "2017-3-16"

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#Partage de pipelines reposant sur du texte dans les exemples de projet {: #share-pipeline}

Dans le cas d'exemples de projet déployés dans {{site.data.keyword.Bluemix_notm}} via le bouton Déployer dans {{site.data.keyword.Bluemix_notm}}, vous pouvez définir des configurations de pipeline sous forme de fichiers YAML. Les pipelines définis sous forme de texte peuvent être partagés pour que les personnes qui dévient votre projet n'aient pas à configurer leurs propres pipelines. Cette fonction est en cours de développement : le format YAML et son implémentation peuvent changer à tout moment. Actuellement, cette fonction n'est disponible que pour les projets avec Git et les référentiels GitHub qui ciblent {{site.data.keyword.Bluemix_notm}}. 
{: shortdesc} 

Le répertoire racine de l'exemple de projet doit contenir un dossier appelé `.bluemix` dans lequel se trouve un fichier `pipeline.yml`.

Lorsqu'un projet est cloné à l'aide du bouton Déployer dans {{site.data.keyword.Bluemix_notm}}, un pipeline basé sur le fichier `pipeline.yml` est créé. 

Exemple : 
``` 
<sample root>
	.bluemix
		pipeline.yml
	<other sample content>
```
{: codeblock} 

Le format de fichier YAML correspond à un document YAML unique qui contient une spécification de pipeline. L'exemple de pipeline suivant génère une application Java avec Ant en une seule étape. Ensuite, dans une autre étape, le pipeline déploie l'application dans {{site.data.keyword.Bluemix_notm}}. 

``` 
---
stages:
- name: Build Stage
  inputs:
  - type: git
    branch: master
  triggers:
  - type: commit
  properties:
  - name: APP_VERSION
    value: '1.0'
    type: text
  jobs:
  - name: Build
    type: builder
    artifact_dir: output
    build_type: ant
    script: |-
      #!/bin/bash
      ant
    enable_tests: true
    test_file_pattern: tests/TEST-*.xml
- name: Deploy Stage
  inputs:
  - type: job
    stage: Build Stage
    job: Build
  triggers:
  - type: stage
  jobs:
  - name: Deploy to dev
    type: deployer
    target:
      url: https://api.ng.bluemix.net
      organization: uateam@ca.ibm.com
      space: dev
      application: JavaSampleUnitTest
    script: |
      cf push "${CF_APP}"
      # View logs
      #cf logs "${CF_APP}" --recent
```
{: codeblock} 

##Syntaxe du fichier YAML {: #yaml-syntax}

N'importe quel pipeline peut être représenté textuellement avec la syntaxe ci-dessous.

Pipeline:
```
---
stages:
<séquence d'étapes>
```
{: codeblock} 

Stage: 
```
---
name: <nom>
[inputs:
	<séquence d'entrées>]
[triggers:
	<séquence de déclencheurs>]
[properties:
	<séquence de propriétés>]
[jobs:
	<séquence de travaux>]
```
{: codeblock} 

Input:
```
type: 'git' | 'job'
[branch: <nom de branche>] ; pour les entrées Git seulement
stage: <nom d'étape>		     ; pour les entrées de travail seulement
job: <nom de travail>			   ; pour les entrées de travail seulement
```
{: codeblock} 

Trigger:
```
type: 'commit' | 'stage'
[enabled: 'true | 'false'] ; true est supposé si la valeur n'est pas spécifiée
```
{: codeblock} 	
	
Property:
```
name: <nom de propriété>
value: <valeur de propriété>
[type: 'text' | 'secure' | 'text_area' | 'file'] ; text est supposé si la valeur n'est pas spécifiée
```
{: codeblock} 

Job:
```
[name: <nom de travail>]
type: 'builder' | 'deployer' | 'tester'
fail_stage: 'true' | 'false'
[extension_id: <ID d'extension>] ; travaux d'extension seulement
[working_dir: <chemin d'accès au répertoire de travail>] ; générateur et testeur seulement
[artifact_dir: chemin de l'artefact>] ; générateur seulement
[build_type: <type de génération>] ; générateur seulement
[script: <script>] ; pas pour les travaux d'extension
[enable_tests: 'true' | 'false'] ; générateur et testeur seulement
[test_file_pattern: <pattern>] ; générateur et testeur seulement
[target: <cible>] ; déployeur et travaux d'extension seulement
*[<nom de propriété d'extension>: <valeur>] ; travaux d'extension seulement
```
{: codeblock} 

Target:
```
url: <url cible>
organization: <nom de l'organisation>
space: <nom de l'espace>
[application: <nom de l'application>]
```
{: codeblock} 

##Travaux d'extension et définitions d'extension {: #extension-jobs} 

Les définitions d'extension définissent l'ensemble de propriétés disponibles pour les travaux d'extension. Un travail est traité comme un travail
d'extension lorsque la propriété `extension_id` est spécifiée. Pour identifier les propriétés disponibles pour une extension,
consultez la documentation associée à l'extension. 

##Interaction avec des pipelines à l'aide d'un fichier YAML {: #pipeline-yaml} 

**VARIABLES D'ENVIRONNEMENT ET RESOLUTION** 
<!-- Formating for this? -->

Avant la création du pipeline à partir d'un fichier `pipeline.yml`, la capacité Déployer dans {{site.data.keyword.Bluemix_notm}} remplace les éventuelles
variables d'environnement figurant dans le fichier par les informations que vous spécifiez dans l'interface {{site.data.keyword.Bluemix_notm}} (par exemple votre organisation). Les valeurs YAML sont substituées uniquement si elles sont composées uniquement d'une variable
d'environnement. 

```
{
  "project_id": "_ljkahfliasdlk",
  "env": {
     "CF_ORGANIZATION" : "user@se.ibm.com"
  },
  "config": {
    "format" : "yaml",
    "content" : "
      ...
        target:
          url: http://api.ng.bluemix.net
          organization: ${CF_ORGANIZATION}
        script: \"echo ${CF_ORGANIZATION}\"                
      ...
    "
  }
}
```
{: codeblock} 

Dans cet exemple, l'organisation cible est résolue avec l'adresse URL cible, et la valeur conservée dans la configuration du
pipeline est l'identificateur global unique de l'organisation. L'occurrence qui figure dans le script de déploiement n'est pas substituée.

L'adresse
URL cible doit être spécifiée en tant que variable d'environnement ou valeur réelle, et les identificateurs globaux uniques ou les noms de l'organisation
et de l'espace doivent être indiqués. Si une valeur est fournie, l'autre est également substituée.

Variable | Description 
---------------- | ---------------- 
CF_TARGET_URL |	Adresse URL cible de Bluemix
CF_ORGANIZATION	| Nom de l'organisation
CF_ORGANIZATION_ID	| Identificateur global unique de l'organisation
CF_SPACE |	Nom de l'espace
CF_SPACE_ID |	Identificateur global unique de l'espace
CF_APP	| Nom de l'application
{: caption="Tableau 1. Variables d'environnement" caption-side="top"}

**GENERATION D'UN FICHIER YAML DEPUIS UN PIPELINE** 

Vous pouvez générer un fichier YAML à partir d'un pipeline. 

Générez le fichier à partir d'un pipeline existant avec une adresse URL au
format suivant :

```
<domain>/pipeline/user/project/yaml
```
{: codeblock} 

Cet appel ne requiert pas d'en-tête accept. Vous pouvez l'utiliser depuis
un navigateur. 

**Remarque :** pour des raisons de sécurité, les valeurs de propriété d'environnement de transfert sécurisé sont omises dans les
fichiers YAML de pipeline générés. 
