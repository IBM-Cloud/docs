---

copyright:
  years: 2016
lastupdated: "2016-11-17"
---
<!-- Copyright info at top of file: REQUIRED
    The copyright info is YAML content that must occur at the top of the MD file, before attributes are listed.
    It must be surrounded by 3 dashes.
    The value "years" can contain just one year or a two years separated by a comma. (years: 2014, 2016)
    Indentation as per the previous template must be preserved.
-->

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Propriedades e recursos do ambiente
{: #deliverypipeline_environment}

É possível usar as propriedades e os recursos pré-instalados do ambiente para interagir com o serviço IBM&reg; Bluemix&reg; {{site.data.keyword.deliverypipeline}}. Por exemplo, você poderá incorporá-los em um script de tarefa ou comando de teste.
{:shortdesc}

É possível incluir suas próprias propriedades do ambiente em um estágio a partir
de sua guia **PROPRIEDADES DO AMBIENTE**. As propriedades do ambiente
estão disponíveis a cada tarefa de um estágio.

É possível incluir quatro tipos de propriedades na guia Propriedades do ambiente:
* **Texto**: uma chave de propriedade com um valor de linha única.
* **Área de texto**: uma chave de propriedade com um valor multilinhas.
* **Seguro**: uma chave de propriedade com um valor de linha única. O valor é exibido como asteriscos.
* **Propriedades**: um arquivo no repositório do projeto. Esse
arquivo pode conter diversas propriedades. Cada propriedade deve estar em sua própria
linha. Para separar os pares de chave/valor, use o sinal de igual (=).


As propriedades e recursos a seguir estão disponíveis, por padrão, em ambientes de pipeline.

<!--##Contents
* [Environment properties](#env)
    * [General purpose properties](#gen)
    * [Runtime and tool properties](#runtime)
    * [Deployment properties](#deployment)
* [Pre-installed resources](#resources)
    * [Runtimes and tools](#tools)
    * [Node modules](#node)-->

## Propriedades do ambiente
{: #deliverypipeline_envprop}

### Propriedades gerais do propósito

| Propriedade do ambiente | Descrição |
|-------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| ARCHIVE_DIR | O diretório no qual arquivar ou fazer download de archives. |
| BUILD_ID | O ID exclusivo para a execução da tarefa atual.  |
| BUILD_DISPLAY_NAME | O valor BUILD_ID, prefixado com "#". |
| BUILD_NUMBER | O ID de estágio incremental que é mostrado na UI do pipeline.  |
| GIT_BRANCH | A ramificação Git que a tarefa usa como entrada. Essa propriedade está disponível somente em tarefas que usam um repositório Git como entrada. |
| GIT_COMMIT | A confirmação Git que a tarefa usa como entrada. Essa propriedade está disponível somente em tarefas que usam um repositório Git como entrada. |
| GIT_PREVIOUS_COMMIT | O valor de confirmação Git da última execução bem-sucedida da tarefa. Essa propriedade está disponível somente em tarefas que usam um repositório Git como entrada. |
| GIT_URL | A URL de repositório Git que a tarefa usa como entrada. Essa propriedade está disponível somente em tarefas que usam um repositório Git como entrada. |
| IDS_JOB_ID | O ID exclusivo da configuração da tarefa. |
| IDS_JOB_NAME | O nome da configuração da tarefa. |
| IDS_OUTPUT_PROPS | Nomes de suas propriedades do ambiente de estágio separados por vírgula. |
| IDS_PROJECT_NAME | O nome do projeto, exemplo <code>Owner - Project Name</code>. |
| IDS_STAGE_NAME | O nome do estágio atual. |
| IDS_URL | A URL para o pipeline atual. |
| IDS_VERSION | O número da construção que está sendo implementada ou o identificador do SCM. Essa propriedade está disponível somente para tarefas de implementação.
| JOB_NAME | O ID exclusivo da tarefa no contexto do pipeline atual. |
| PIPELINE_STAGE_INPUT_JOB_ID | O ID da tarefa que é a entrada para o estágio atual. |
| PIPELINE_STAGE_INPUT_REV | A revisão da entrada para o estágio atual. |
| PIPELINE_INITIAL_STAGE_EXECUTION_ID | O ID exclusivo para a execução do pipeline. |
| TASK_ID | O ID exclusivo da execução atual da tarefa. |
| TMPDIR | Uma localização de diretório em que os arquivos temporários são armazenados. |
| WORKSPACE | O caminho para o diretório atualmente em funcionamento. |

### Propriedades de tempo de execução e ferramentas

| Propriedade do ambiente | Descrição |
|-------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| ANT_HOME | O caminho para o Apache Ant 1.9.2. |
| GRADLE_HOME | O caminho para o Gradle 1.11. |
| JAVA_HOME | O caminho para o IBM&reg; Java&trade; 7. |
| JAVA7_HOME | O caminho para o IBM Java 7. |
| JAVA8_HOME | O caminho para o IBM Java 8. |
| MAVEN_HOME | O caminho para o Apache Maven 3.2.1. |
| NODE_HOME | O caminho para o Node.js 0.10.29. |

### Propriedades de implementação

| Propriedade do ambiente | Descrição |
|-------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| CF_APP | Para implementações, o nome do app a ser implementado. Essa propriedade é necessária para implementação e pode ser especificada no próprio script, na interface de configuração da tarefa de implementação ou no arquivo `manifest.yml` do projeto. |
| CF_ORG | Para implementações, o nome da organização (org) a ser implementada. |
| CF_ORGANIZATION_ID | Para implementações, o ID da organização a ser implementada. |
| CF_SPACE | Para implementações, o nome do espaço a ser implementado. |
| CF_SPACE_ID | Para implementações, o ID do espaço a ser implementado.  |
| CF_TARGET_URL | Para implementações, a URL do IBM Bluemix&reg; ou do Cloud Foundry. |
| IDS_VERSION | Para implementações, a versão do app que está sendo implementado ou o identificador de origem. |

## Recursos pré-instalados
{: #deliverypipeline_resources}

Vários tempos de execução, ferramentas e módulos do Node são pré-instalados em cada pipeline.

### Tempos de execução e ferramentas

*Observação:* todos os links estão no diretório inicial.

| Recurso | Nome de link | Caminho |
|----------|-----------|-----------|
|Apache Ant 1.9.2|ant |/opt/IBM/ant |
|Cloud Foundry CLI 6.14 |cf | /opt/IBM/cf |
|Gradle 1.12|gradle |/opt/IBM/gradle |
|Gradle 2.9 |gradle2 |/opt/IBM/gradle2 |
|IBM Java (default)|java |/opt/IBM/java |
|IBM Java 7 x86_64-71 |java7 |/opt/IBM/java7 |
|IBM Java 8 x86_64-80|java8 |/opt/IBM/java8 |
|Apache Maven 3.2.1 |maven |/opt/IBM/maven |
|IBM Node |node |/opt/IBM/node |
|IBM Rational Team Concert&trade; SCM Tools |RTC-SCM-Tools |/opt/IBM/RTC-SCM-Tools |

As versões de 64 bits do IBM Node 0.10, 0.10.48, 0.12, 0.12.17, 4.2, 4.4.5, 4.6.0,
6.2.2 e 6.7.0 estão disponíveis no ambiente do pipeline. Para escolher uma versão, use o comando de exportação.

Por exemplo, para usar o Node 0.12.7, insira este comando:
`export PATH=/opt/IBM/node-v0.12/bin:$PATH`

Para usar o Node 4.2.2, insira este comando:
`export PATH=/opt/IBM/node-v4.2/bin:$PATH`

### Módulos do Node

Os seguintes módulos do Node são instalados globalmente no ambiente do pipeline:

* grunt@0.4.5
* grunt-cli@0.1.13
* grunt-contrib-concat@0.4.0
* grunt-contrib-jshint@0.10.0
* grunt-contrib-nodeunit@0.4.1
* grunt-contrib-qunit@0.5.1
* grunt-contrib-uglify@0.5.0
* grunt-contrib-watch@0.6.1
* karma@0.12.23
* karma-cli@0.0.4
* karma-jasmine@0.1.5
* karma-phantomjs-launcher@0.1.4
* phantomjs@1.9.10
