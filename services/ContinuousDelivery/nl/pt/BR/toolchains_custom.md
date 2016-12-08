---

copyright:
  years: 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Configurando cadeias de ferramentas customizadas (experimental)
{: #toolchains-custom}
Última atualização: 27 de abril de 2016
{: .last-updated}

A criação de uma cadeia de ferramentas customizada pode ajudar a melhorar seu
fluxo de trabalho DevOps. É possível iniciar rapidamente com um dos modelos de cadeia de
ferramentas existente ou customizar um dos modelos para criar uma cadeia de ferramentas
mais customizada a partir da qual iniciar.
{:shortdesc}

Há muitas formas de
[criar
e implementar uma cadeia de ferramentas](https://daily-console.stage1.ng.bluemix.net/docs/toolchains/toolchains_setup.html){: new_window}. Este guia explicará
as etapas para criar uma cadeia de ferramentas customizada que possa ser implementada
usando um botão
[Implementar
no {{site.data.keyword.Bluemix_notm}}](https://daily-console.stage1.ng.bluemix.net/docs/develop/deploy_button.html){: new_window}. Após uma
configuração, você poderá facilmente compartilhar um projeto GitHub com uma cadeia de
ferramentas implementável no {{site.data.keyword.Bluemix_notm}}.


## Introdução
{: #toolchains_custom_gettingstarted}

Para criar uma cadeia de ferramentas customizada, nós começaremos clonando um
modelo de cadeia de ferramentas. A clonagem de um modelo existente dará rapidamente a
você um ponto de partida do qual iniciar sua customização.

1. Usando um cliente Git de sua escolha, insira o comando a seguir para clonar o modelo de [Cadeia de ferramentas simples](https://github.com/open-toolchain/simple-toolchain){: new_window} no GitHub.

 ```
 git clone https://github.com/open-toolchain/simple-toolchain.git
 ```
 {: pre}

 Esse modelo implementa um aplicativo Hello World básico a partir de um único
repositório GitHub e inclui uma cadeia de ferramentas simples que está pré-configurada
para entrega contínua, controle de fonte, rastreamento de problemas e edição on-line.

2. **(Opcional)**: se você preferir iniciar com um modelo de
cadeia de ferramentas mais complexo, poderá começar pela clonagem da
[Cadeia de
ferramentas nativa da nuvem para microsserviços](https://github.com/open-toolchain/toolchain-demo){: new_window}.

 ```
 git clone https://github.com/open-toolchain/toolchain-demo.git
 ```
 {: pre}

 Esse modelo implementa um armazenamento on-line formado por três microsserviços,
cada um contido em seu próprio repositório GitHub. Uma cadeia de ferramentas mais
complexa também está incluída e pré-configurada para entrega contínua, controle de fonte,
implementações azul/verde, teste funcional, rastreamento de problemas, edição on-line e
sistema de mensagens.

Independentemente do modelo escolhido, os princípios descritos neste guia
para a criação de uma cadeia de ferramentas customizada serão semelhantes.

Após a clonagem do modelo, você terá um repositório GitHub básico que tem um
arquivo *Leia-me* e um diretório `.bluemix` que contém
todos os arquivos de configuração necessários para fazer sua cadeia de ferramentas
funcionar. No mínimo, o diretório `.bluemix` deverá conter o seguinte:

* toolchain.yml
* deploy.json
* pipeline.yml

Cada um desses arquivos será explicado nas seções a seguir, com algumas
configurações adicionais que podem precisar ser incluídas à medida que sua cadeia de
ferramentas evolui.

## Entendendo os arquivos de configuração
{: #toolchains_custom_config_files}

Os arquivos de configuração de modelo de cadeia de ferramentas são compostos
principalmente de arquivo de formato YAML. Cada arquivo contém metadados que descrevem
diferentes aspectos da cadeia de ferramentas. Isso inclui informações gerais descritivas
sobre a cadeia de ferramentas, os repositórios GitHub a serem incluídos, os detalhes de
como o código deverá ser construído e onde ele deverá ser implementado, além dos detalhes
de configuração das várias ferramentas que serão incluídas na cadeia. À medida que sua
cadeia de ferramentas se tornar mais complexa, os arquivos de configuração também vão
sendo adequados. É importante que os arquivos permaneçam bem formatados para reduzir o
risco de erros serem introduzidos.

Algumas diretrizes para se ter em mente ao trabalhar em um arquivo YAML:

* Não são permitidas tabulações. Somente espaços devem ser usados.
* Todas as propriedades e listas devem ser recuadas com um ou mais espaços.
* Todas as chaves e propriedades fazem distinção entre maiúsculas e minúsculas.

Para verificar duas vezes seu trabalho, convém usar um validador de YAML simples,
como este [Analisador de
YAML](http://wiki.ess3.net/yaml/){: new_window} para evitar erros desse tipo.

  
## toolchain.yml
{: #toolchains_custom_toolchain_yml}

O arquivo `toolchain.yml` é o ponto central da cadeia de
ferramentas. As especificações de sua cadeia de ferramentas, incluindo repositórios para
pull, serviços a serem incluídos e detalhes de construção, estão todos descritos nesse
arquivo. Para que seu conteúdo faça sentido, ele pode ser dividido em várias seções.

1\. **Informações introdutórias da cadeia de ferramentas:**

 Esta seção fornece detalhes simples sobre sua cadeia de ferramentas que são
apresentados ao usuário na página de criação da cadeia de ferramentas. É necessário incluir um nome
para sua cadeia de ferramentas com uma descrição que explique o propósito dela ou o que
ela fará quando for implementada. Uma imagem também pode ser incluída para exibir um
logotipo ou uma representação visual da cadeia de ferramentas.

 Além de fornecer o conteúdo introdutório para sua cadeia de ferramentas, esta
seção também inclui uma chave chamada `required` que define as
integrações de ferramentas que podem ser configuradas no momento da criação da cadeia de ferramentas na
página. A permissão para que uma ferramenta seja configurada no momento da criação
permite que você crie uma cadeia de ferramentas que possa ser facilmente reutilizada ou
ganhar um novo propósito. Para cada ferramenta que pode ser configurada na página de
criação da cadeia de ferramentas, inclua a chave-pai das ferramentas no arquivo
`toolchain.yml` como propriedade da chave `required`.

 Este snippet mostra um exemplo dessa seção:

 ```
 ---
 name: "Simple Toolchain"
 description: "This Hello World application uses Node.js and includes a toolchain that is preconfigured for continuous delivery, source control, issue tracking, and online editing.\n\nTo get started, click **Create**."
 version: 0.1
 # Generate base64 representation of image at http://www.askapache.com/online-tools/base64-image-converter/
 image: data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAY4AAA...
 required: 
  - deploy
  - hello-world-repo
  ```
 {: codeblock}

 **Nota:** as imagens primeiro devem ser convertidas em uma
representação base 64 usando uma ferramenta como [AskApache](http://www.askapache.com/online-tools/base64-image-converter/).

2\. **Definições do repositório GitHub:**

 Uma cadeia de ferramentas pode fornecer entrega contínua para qualquer número de
repositórios GitHub. Esta seção do arquivo `toolchain.yml` é onde cada
repositório deve ser definido.

 Para iniciar, para cada repositório GitHub que será incluído na cadeia de
ferramentas, inclua uma chave-pai que represente o nome de seu repositório GitHub com as
propriedades a seguir:

| Item | Chave/Propriedade | Valor | Descrição |
|------|--------------|-------|-------------|
| repo-name | principais |  | Nome do repositório |
| service_id | propriedades | <`githubpublic` , `githubprivate`> | Tipo de repositório GitHub |
| parâmetros: | principais |  |  |
| repo_name | propriedades |  | **COMENTÁRIO: como isso deve ser definido** |
| repo_url | propriedades |  | URL do repositório GitHub |
| Tipo | propriedades | <`new` , `fork` , `clone` , `link`> | Como o repositório deve ser criado |
| has_issues | propriedades | <`true` , `false`> | Use o GitHub Issues |

 **Nota:** se você definir diversos repositórios e configurá-los
como `has_issues: true`, uma única instância do rastreador GitHub Issue
será incluída na cadeia de ferramentas que rastreará os problemas de todos os
repositórios que foram configurados como `true`.

 Este snippet mostra um exemplo dessa seção:

 ```
 # Github repos
 hello-world-repo:
   service_id: githubpublic
   parameters:
 	repo_name: "hello-world-{{name}}"
 	repo_url: https://github.com/open-toolchain/node-hello-world
 	type: clone
 	has_issues: true
 ```
 {: codeblock}

3\. **Informações do pipeline:**

 A entrega contínua é tornada possível com o pipeline. Esta seção define os
detalhes de configuração que são usados para construir e implementar o código em cada
repositório GitHub.

 Para iniciar, para cada repositório GitHub que foi definido na cadeia de
ferramentas, inclua uma chave-pai que represente o nome de seu pipeline. A derivação
dessa chave do nome de seu repositório GitHub é uma boa sugestão. Inclua as seguintes propriedades:

| Item | Chave/Propriedade | Valor | Descrição |
|------|--------------|-------|-------------|
| pipeline-name | principais |  | Nome do pipeline |
| service_id | propriedades | <`pipeline`> | Nome do serviço a ser usado |
| parâmetros | principais |  |  |
| nome | propriedades | <`repo_name`> | O mesmo nome definido na seção #Github repos para |
| ui-pipeline | propriedades | <`true` , `false`> |  |
| configuration | principais |  |  |
| conteúdo | propriedades | <`$file(pipeline.yml)`> | Arquivo que estabelece a definição de pipeline |
| env | principais |  |  |
| REPO_NAME | principais | <`repo-name-key`> | O mesmo nome da chave-pai do seu repositório GitHub |
| CF_APP_NAME |  propriedades | <`"{{deploy.parameters.repo-name-key}}"`> | Nome usado pelo Cloud Foundry. Deve incluir o nome da chave-pai do seu repositório GitHub |
| PROD_SPACE_NAME | propriedades | <`"{{deploy.parameters.prod-space}}"`> | Nome do espaço do {{site.data.keyword.Bluemix_notm}} no qual implementar |
| PROD_ORG_NAME | propriedades | <`"{{deploy.parameters.prod-organization}}"`> | Nome da organização {{site.data.keyword.Bluemix_notm}} na qual implementar |
| PROD_REGION_ID | propriedades | <`"{{deploy.parameters.prod-region}}"`> | Nome da região {{site.data.keyword.Bluemix_notm}} na qual implementar |
| execute | propriedades | <`true` , `false`> | Iniciar pipeline após criação |
| services | propriedades | <`repo-name-key`> |  Chave-pai do repositório GitHub |
| oculto | propriedades | <`[form, description]`> |  |

 As informações sobre a criação de um arquivo `pipeline.yml` podem
ser encontradas em uma [seção posterior.](#toolchains_custom_pipeline_yml)

 Este snippet mostra um exemplo dessa seção:

 ```
 # Pipelines
 hello-world-build:
   service_id: pipeline
   parameters:
 	name: "hello-world-{{name}}"
 	ui-pipeline: true
 	configuration: 
 	 content: $file(hello-world.pipeline.yml)
 	 env:
 	  HELLO_WORLD_REPO: "hello-world-repo"
 	  CF_APP_NAME: "{{deploy.parameters.hello-world-name}}"
 	  PROD_SPACE_NAME: "{{deploy.parameters.prod-space}}"
 	  PROD_ORG_NAME: "{{deploy.parameters.prod-organization}}"
 	  PROD_REGION_ID: "{{deploy.parameters.prod-region}}"
 	 execute: true
 	services: ["hello-world-repo"]
   hidden: [form, description]
 ```
 {: codeblock}

4\. **Detalhes da implementação:**

 Como parte do processo de entrega contínua, uma cadeia de ferramentas pode ser
configurada para implementar seu aplicativo em qualquer Região, Organização ou Espaço do
{{site.data.keyword.Bluemix_notm}} que o usuário que está implementando a cadeia
de ferramentas tenha acesso também. Os detalhes específicos de onde implementar seu
aplicativo podem ser selecionados na página de criação da cadeia de ferramentas.  

 ![Definições de configuração do pipeline de entrega](images/deploy_configuration.png)

 Esta seção do arquivo `toolchain.yml` define os estágios do
pipeline que estão disponíveis para serem configurados na página de criação da cadeia de
ferramentas.

 Para iniciar, a chave-pai `deploy` é usada para identificar as
propriedades de configuração de implementação. As propriedades a seguir compõem o
restante da seção:

| Item | Chave/Propriedade | Valor | Descrição |
|------|--------------|-------|-------------|
| Implementação | principais |  | Nome da seção de implementação |
| Esquema | propriedades | <`deploy.json`> | Arquivo que define o layout da IU para configurar os detalhes da implementação |
| service-category | propriedades | <`pipeline`> | Serviço que usará as configurações de implementação |
| parâmetros | principais |  |  |
| prod-region | propriedades | <`"{{region}}"`> | Define a região do {{site.data.keyword.Bluemix_notm}} para o estágio de produção |
| prod-organization | propriedades | <`"{{organization}}"`> | Define a organização do {{site.data.keyword.Bluemix_notm}} para o estágio de produção |
| prod-space | propriedades | <`prod`> | Define o espaço do {{site.data.keyword.Bluemix_notm}} para o estágio de produção |
| github-repo-name | propriedades | <`"{{repo-name-key.parameters.repo_name}}"`> | Variável para passar o nome do repositório GitHub para a página de criação da cadeia de ferramentas |

 As informações sobre a criação de um arquivo `deploy.json` podem
ser encontradas em uma [seção
posterior.](#toolchains_custom_deploy_json)

 O exemplo fornecido a seguir define um único estágio que é implementado em um
ambiente de produção.

 ```
 #Deployment
 deploy:
   schema: deploy.json
   service-category: pipeline
   parameters:
 	prod-region: "{{region}}"
 	prod-organization: "{{organization}}"
 	prod-space: prod
 	hello-world-name: "{{hello-world-repo.parameters.repo_name}}"
 ```
 {: codeblock}

 O exemplo de código pode ser usado na maioria das vezes no estado em que se
encontra e requer pouca modificação somente. Para customizar esta seção, o
`github-repo-name` deve ser atualizado para ficar consistente com o nome
do seu repositório. Os detalhes dentro do arquivo
[`deploy.json`](#toolchains_custom_deploy_json) também
precisarão ser atualizados.

 Para criar um pipeline mais complexo que inclua um estágio dev, QA e Prod, as
propriedades a seguir podem ser substituídas sob a chave `parameters`.

 ```
   parameters:
 	dev-region: "{{region}}"
 	qa-region: "{{region}}"
 	prod-region: "{{region}}"
 	dev-organization: "{{organization}}"
 	qa-organization: "{{organization}}"
 	prod-organization: "{{organization}}"
 	dev-space: dev
 	qa-space: qa
 	prod-space: prod
 ```
 {: codeblock}

5\. **Configurações de ferramentas**

 Após a configuração dos componentes principais de sua cadeia de ferramentas, é
possível começar a incluir outras integrações de ferramentas que ajudarão a incluir
funcionalidade e utilidade adicionais à sua cadeia de ferramentas. Todas as ferramentas
terão uma entrada que deve ser incluída no arquivo `toolchain.yml` e
algumas também exigirão um arquivo de configuração YAML separado que deverá ser criado no
diretório `.bluemix`.

 * **Slack**

	toolchain.yml
	```
	messaging:
	  service_id: slack
	  include: slack.yml
	```
	{: codeblock}
	
	slack.yml
	```
	---
	parameters:
	  api_token: ""
	  channel_name: ""
	```
	{: codeblock}
	
 * **Sauce Labs**

	toolchain.yml
	```
	test:
	  service_id: saucelabs
	  include: saucelabs.yml
	```
	{: codeblock}
	
	saucelabs.yml
	```
	---
	parameters:
	  username: ""
	  key: ""
	```
	{: codeblock}
	
 * **PagerDuty**

	toolchain.yml
	```
	alerting:
	  service_id: pagerduty
	  include: pagerduty.yml
	```
	{: codeblock}

	pagerduty.yml
	```
	---
	parameters:
	  site_name: ""
	  api_key: ""
	  service_name: ""
	  user_email: ""
	  user_phone: ""
	```
	{: codeblock}
	
 * **Eclipse Orion Web IDE**

	toolchain.yml
	```
	webide:
	  service_id: orion
	```
	{: codeblock}


## pipeline.yml
{: #toolchains_custom_pipeline_yml}

O arquivo `pipeline.yml` contém todos os detalhes de configuração
dos estágios de seu pipeline. O arquivo `pipeline.yml` pode ser criado
de duas maneiras.

1. Crie o arquivo `pipeline.yml` manualmente. Os detalhes e a
sintaxe para criar o arquivo `pipeline.yml` podem ser encontrados em
[Compartilhando
pipelines baseados em texto em projetos de amostra de Serviços DevOps](https://new-console.ng.bluemix.net/docs/develop/sharetextpipelines.html){: new_window}.

2. Gere o arquivo `pipeline.yml` a partir de um projeto de Serviços DevOps existente. Para fazer isso,
	
	1. Crie um novo [projeto de Serviços DevOps](https://hub.jazz.net/create){: new_window}.
	
	2. Abra o projeto e clique em **CONSTRUIR E IMPLEMENTAR**
	
	3. Configure todos os estágios necessários para seu pipeline.
	
	4. Na barra de endereço do seu navegador, anexe `/yaml` à URL do projeto e pressione Enter.
	
	5. Salve o arquivo `pipeline.yml` resultante no diretório `.bluemix` em seu repositório GitHub.

Se a sua cadeia de ferramentas contiver mais de um pipeline, forneça nomes
exclusivos para cada arquivo `pipeline.yml`.

Veja a seguir o exemplo de um arquivo `pipeline.yml`:

```
---
stages:
- name: BUILD
  inputs:
  - type: git
	branch: master
	service: ${HELLO_WORLD_REPO}
  triggers:
  - type: commit
  jobs:
  - name: Build
	type: builder
- name: DEPLOY
  inputs:
  - type: job
	stage: BUILD
	job: Build
  triggers:
  - type: stage
  properties:
  - name: CF_APP_NAME
	value: undefined
	type: text
  - name: APP_URL
	value: undefined
	type: text
  jobs:
  - name: Deploy
	type: deployer
	target:
	  region_id: ${PROD_REGION_ID}
	  organization: ${PROD_ORG_NAME}
	  space: ${PROD_SPACE_NAME}
	  application: ${CF_APP_NAME}
	script: |
	  #!/bin/bash
	  # Push app
	  export CF_APP_NAME="$CF_APP"
	  cf push "${CF_APP_NAME}"
	  export APP_URL=http://$(cf app $CF_APP_NAME | grep urls: | awk '{print $2}')
	  # View logs
	  #cf logs "${CF_APP_NAME}" --recent
```
{: codeblock}		


## deploy.json
{: #toolchains_custom_deploy_json}

Na página de criação da cadeia de ferramentas, quando Pipeline de entrega é
selecionado na seção Integrações configuráveis, a seção é ampliada para exibir os itens a
seguir que podem ser configurados para essa ferramenta:

	* O nome dos aplicativos
	* A Região, a Organização e o Espaço nos quais os estágios do pipeline serão implementados também.

![Definições de configuração do
pipeline de entrega](images/deploy_configuration.png)

O layout desta seção na IU é definido pelo esquema `deploy.json`.

Dentro do esquema, as propriedades a seguir deverão ser atualizadas para
corresponder aos detalhes de seu aplicativo:

	* Título
	* Descrição
	* LongDescription
	* Todas as instâncias de `hello-world-name` e os detalhes
associados deverão ser modificados para corresponder aos do seu aplicativo.

Veja a seguir o exemplo de um arquivo `deploy.json`:

```
{
    "$schema": "http://json-schema.org/draft-04/schema#",
    "title": "Hello World Deploy Stage",
    "description": "hello-world simple toolchain",
    "longDescription": "The Delivery Pipeline for Devops Services allows you to automate your continuous deployment setup hello-world.",
    "type": "object",
    "properties": {
        "prod-region": {
            "description": "The bluemix region",
            "type": "string"
        },
        "prod-organization": {
            "description": "The bluemix org",
            "type": "string"
        },
       "prod-space": {
            "description": "The bluemix space",
            "type": "string"
        },
       "hello-world-name": {
            "description": "hello world app name",
            "type": "string"
        }
    },
    "required": ["prod-region", "prod-organization", "prod-space", "hello-world-name"],
    "form": [
       {
          "type": "validator",
          "url": "/devops/setup/bm-helper/helper.html"
       },        
        {
          "type": "text",
          "readonly": false,
          "title": "Hello World App Name",
          "key": "hello-world-name"
        },
        {
            "type": "table",
            "columnCount": 4,
            "widths": ["15%", "28%", "28%", "28%"],
            "items": [
                {
                  "type": "label",
                  "title": ""
                },
                {
                  "type": "label",
                  "title": "Region"
                },
                {
                  "type": "label",
                  "title": "Organization"
                },
                {
                  "type": "label",
                  "title": "Space"
                },
                {
                  "type": "label",
                  "title": "Prod Stage"
                },
                {
                  "type": "select",
                  "key": "prod-region"
                },
                {
                  "type": "select",
                  "key": "prod-organization"
                },
                {
                  "type": "select",
                  "key": "prod-space",
                  "readonly": false
                }
            ]
        }
    ]
}
```
{: codeblock}
