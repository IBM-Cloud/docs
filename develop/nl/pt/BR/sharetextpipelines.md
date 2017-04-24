---

copyright:
  years: 2015, 2017
lastupdated: "2017-3-16"

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#Compartilhando pipelines baseados em texto em projetos de amostra {: #share-pipeline}

No caso dos projetos de amostra implementados no {{site.data.keyword.Bluemix_notm}} pelo botão
Implementar no {{site.data.keyword.Bluemix_notm}}, é possível definir as configurações do pipeline
como arquivos YAML. Pipelines definidas como texto podem ser compartilhadas de modo que não
seja necessário para aqueles que trabalham em seu projeto configurar suas próprias
pipelines. Esse recurso está em desenvolvimento: o formato YAML e a implementação podem
mudar a qualquer momento. Atualmente, esse recurso está disponível apenas para projetos
com repositórios Git e GitHub que se destinam ao
{{site.data.keyword.Bluemix_notm}}. 
{: shortdesc} 

No diretório raiz do projeto de amostra, você deve ter uma pasta denominada
`.bluemix` com um arquivo `pipeline.yml`.

Quando um projeto é clonado usando o botão Implementar no {{site.data.keyword.Bluemix_notm}}, um
pipeline que se baseia no arquivo `pipeline.yml` é criado. 

Exemplo: 
``` 
<sample root>
	.bluemix
		pipeline.yml
	<other sample content>
```
{: codeblock} 

O formato de arquivo YAML é um documento YAML único que contém uma
especificação de pipeline. O pipeline de amostra a seguir
constrói um app Java com Ant em um estágio. Em seguida, em outro estágio, o pipeline implementa o
app no {{site.data.keyword.Bluemix_notm}}. 

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

##Sintaxe do arquivo YAML {: #yaml-syntax}

É possível representar textualmente qualquer pipeline usando a sintaxe a
seguir.

Pipeline:
```
---
stages:
<sequence of stages>
```
{: codeblock} 

Estágio: 
```
---
name: <name>
[inputs: 
	<sequence of inputs>] 
[triggers:   
	<sequence of triggers>] 
[properties:   
	<sequence of properties>] 
[jobs:   
	<sequence of jobs>]
```
{: codeblock} 

Entrada:
```
type: 'git' | 'job'
[branch: <branch name>] ;only for Git inputs
stage: <stage name>		  ;only for job inputs
job: <job name>			   	;only for job inputs
```
{: codeblock} 

Acionador:
```
type: 'commit' | 'stage'
[enabled: 'true | 'false'] ;true is assumed if not specified
```
{: codeblock} 	
	
Propriedade:
```
name: <property name>
value: <property value>
[type: 'text' | 'secure' | 'text_area' | 'file'] ;text is assumed if not specified
```
{: codeblock} 

Job:
```
[name: <job name>]
type: 'builder' | 'deployer' | 'tester'
fail_stage: 'true' | 'false'
[extension_id: <extension id>] ;extension jobs only
[working_dir: <working dir path>] ;builder and tester only
[artifact_dir: artifact path>] ;builder only
[build_type: <build type>] ;builder only
[script: <script>] ;not for extension jobs
[enable_tests: 'true' | 'false'] ;builder and tester only
[test_file_pattern: <pattern>] ;builder and tester only
[target: <target>] ;deployer and extension jobs only
*[<extension property name>: <value>] ;extension jobs only
```
{: codeblock} 

Resposta:
```
url: <target url>
organization: <org name>
space: <space name>
[application: <application name>]
```
{: codeblock} 

##Tarefas de extensão e definições de extensão {: #extension-jobs} 

As definições de extensão determinam o conjunto de propriedades disponíveis para
as tarefas de extensão. Uma tarefa é tratada como tarefa de extensão quando a propriedade
`extension_id` está especificada. Para descobrir que propriedades estão
disponíveis para uma extensão, consulte a respectiva documentação. 

##Interagindo com pipelines usando um arquivo YAML {: #pipeline-yaml} 

**VARIÁVEIS DE AMBIENTE E RESOLUÇÃO** 
<!-- Formating for this? -->

Antes de o pipeline ser criado a partir de um arquivo `pipeline.yml`, o recurso Deploy to {{site.data.keyword.Bluemix_notm}} substitui as variáveis de ambiente no arquivo por informações especificadas na interface do {{site.data.keyword.Bluemix_notm}} (por exemplo, sua organização). Os valores YAML
serão substituídos apenas quando compostos unicamente por uma variável de ambiente. 

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

Neste exemplo, a organização de destino é resolvida em relação à URL de
destino e o valor que persiste na configuração do pipeline é o GUID da organização. A
ocorrência no script de implementação não é substituída.

A URL de destino deve ser especificada como uma variável
de ambiente ou um valor real e os GUIDs ou nomes da
organização e espaço devem ser fornecidos. Se um valor for fornecido, o outro
também será substituído.

Variável | Descrição 
---------------- | ---------------- 
CF_TARGET_URL |	URL de destino do Bluemix
CF_ORGANIZATION	| Nome da organização
CF_ORGANIZATION_ID	| GUID da organização
CF_SPACE |	Nome de espaço
CF_SPACE_ID |	GUID do espaço
CF_APP	| Nome do app
{: caption="Table 1. Environment variables" caption-side="top"}

**GERANDO UM ARQUIVO YAML A PARTIR DE UM PIPELINE** 

É possível gerar um arquivo YAML a partir de um pipeline. 

Gere
o arquivo a partir de um pipeline existente com uma URL neste formato:

```
<domain>/pipeline/user/project/yaml
```
{: codeblock} 

Essa
chamada não requer um cabeçalho Accept. Você pode usar a chamada em um navegador. 

**Nota:** Por motivos de segurança, os valores da propriedade de ambiente secure-stage são omitidos nos arquivos YAML do pipeline gerado. 
