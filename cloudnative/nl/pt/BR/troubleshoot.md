---

copyright:
  years: 2017
lastupdated: "2017-04-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# Resolução de problema
{: #ts}

Alguns problemas conhecidos com a {{site.data.keyword.dev_cli_notm}} são documentados, junto a suas soluções alternativas.
{:shortdesc}

<!-- Add a headings and paragraphs about troubleshooting for your service, or a list of known issues and workarounds. -->

## Problemas conhecidos
{: #knownissues}

As seções a seguir descrevem os problemas conhecidos e as possíveis resoluções.


### Erro "Hostname is taken" ao criar um projeto com um padrão não móvel
{: #hostname}

Será possível ver o erro a seguir se você usar a {{site.data.keyword.dev_cli_short}} para criar um projeto por meio dos padrões Web App, BFF ou Microservice:

```
The hostname <myHostname> is taken.
```
{: codeblock}


#### Causa
{: #hostname-cause}
   
Esse erro deve-se a um token de login expirado.


#### Resolução
{: #hostname-resolution}

Efetue login novamente.

```
bx login
```
{: codeblock}


### Falhas gerais com a {{site.data.keyword.dev_cli_short}}
{: #general}

Será possível ver o erro a seguir se você usar os comandos create, delete, list ou code da {{site.data.keyword.dev_cli_short}}:

```
Failed to <command> project.
```
{: codeblock}


#### Causa
{: #general-cause}
   
Esse erro deve-se a um token de login expirado.


#### Resolução
{: #general-resolution}

Efetue login novamente.

```
bx login
```
{: codeblock}


### Erro do broker de serviço ao incluir o recurso {{site.data.keyword.objectstorageshort}}
{: #os}

Será possível ver o erro a seguir se você usar a {{site.data.keyword.dev_cli_short}} para criar dois projetos com o recurso {{site.data.keyword.objectstorageshort}}:

```
FAILED
Service broker error: {"description"=>"You can not create this Object Storage instance. Each organization using the Object Storage service is limited to one instance of the Free plan."}
```
{: codeblock}


#### Causa
{: #os-cause}
   
Esse erro ocorre porque o serviço {{site.data.keyword.objectstorageshort}} fornece somente uma instância do plano Free {{site.data.keyword.objectstorageshort}}.


#### Resolução
{: #os-resolution}

É solicitado que você escolha um plano diferente para evitar esse erro.


### Falha ao obter o código durante a criação do projeto
{: #code}

Será possível ver o erro a seguir se você usar a {{site.data.keyword.dev_cli_short}} para criar um projeto:
	
```
FAILED                            
Project created, but could not get code
https://console.ng.bluemix.net/developer/projects/b22165f3-cbc6-4f73-876f-e33cbec199d4/code
```
{: codeblock}
	

#### Causa
{: #code-cause}

Esse erro deve-se a um tempo limite interno.
	

#### Resolução
{: #code-resolution}

É possível obter o código de uma das maneiras a seguir:

* Execute o comando a seguir usando a CLI:

   ```
   bx dev code <your-project-name>
   ```
   {: codeblock}

   Substitua `<your-project-name>` pelo nome do projeto que você especificou durante a criação do projeto.

* Use o {{site.data.keyword.dev_console}}.

	1. Selecione seu [projeto ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://console.{DomainName}/developer/projects) no {{site.data.keyword.dev_console}} e clique em **Obter o código**.

	2. Clique em **Gerar código**.

	3. Depois que o código for gerado, clique em **Fazer download do código**.


### Erro ao executar `bx dev run` para projetos Node.js
{: #node}

Será possível ver o erro a seguir se você estiver executando `bx dev run` com a {{site.data.keyword.dev_cli_short}} para projetos Node.js Web ou BFF:

```
module.js:597
  return process.dlopen(module, path._makeLong(filename));
                 ^

Error: /app/node_modules/bluemix-autoscaling-agent/node_modules/appmetrics/appmetrics.node: invalid ELF header
    at Error (native)
    at Object.Module._extensions..node (module.js:597:18)
    at Module.load (module.js:487:32)
    at tryModuleLoad (module.js:446:12)

    at Function.Module._load (module.js:438:3)
    at Module.require (module.js:497:17)
    at require (internal/module.js:20:19)
    at Object.<anonymous> (/app/node_modules/bluemix-autoscaling-agent/node_modules/appmetrics/index.js:25:13)
    at Module._compile (module.js:570:32)
    at Object.Module._extensions..js (module.js:579:10)
```
{: codeblock}


#### Causa
{: #node-cause}
   
Esse erro é causado pelo módulo `appmetrics` estar instalado em uma arquitetura diferente. Módulos npm nativos que estão instalados em uma arquitetura não funcionam em outra. As imagens incluídas do Docker baseiam-se no kernel Linux.


#### Resolução
{: #node-resolution}

Exclua a pasta `node_modules` e execute `bx dev run` novamente.


<!--
## Troubleshooting techniques
{: #tstechniques}
-->

<!-- Add a heading and content for how to get help and support. Use this template for beta and GA services:  -->


## Obtendo Ajuda e Suporte
{: #gettinghelp}

Se você tiver problemas ou perguntas sobre o {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} ou o {{site.data.keyword.dev_cli_notm}}, será possível obter ajuda procurando informações ou fazendo perguntas por meio de um fórum. Também é possível abrir um chamado de suporte.

Ao fazer uma pergunta nos fóruns, identifique sua pergunta para que ela seja vista pelas equipes de desenvolvimento do {{site.data.keyword.Bluemix_notm}}.

<!--Insert the appropriate Stack Overflow tag for your service for <service_keyword> in URL and text below:  -->

Se tiver questões técnicas sobre como desenvolver ou implementar um app com o {{site.data.keyword.dev_console}} ou a {{site.data.keyword.dev_cli_notm}}:

* Poste sua pergunta no [Stack Overflow ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](http://stackoverflow.com/search?q=bluemix-dev-services+ibm-bluemix) e marque-a com `bluemix-dev-services` e `ibm-bluemix`.
* Poste sua pergunta no [Slack ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](http://ibm-cloud-tech.slack.com/) no canal `bluemix-dev-services`. [Inscreva-se ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](http://ibm.biz/IBMCloudNativeSlack) hoje.


<!--Insert the appropriate dW Answers tag for your service for <service_keyword> in URL below:  -->
<!--
* For questions about the service and getting started instructions, use the [IBM developerWorks dW Answers ![External link icon](../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/answers/topics/bluemix-dev-services/?smartspace=bluemix) forum. Include the  "bluemix-dev-services" and "bluemix" tags.
* -->

Consulte [Obtendo ajuda![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](/docs/support/index.html#getting-help) para obter mais detalhes sobre o uso dos fóruns.

Para obter informações sobre como abrir um chamado de suporte da {{site.data.keyword.IBM}} ou sobre os níveis de suporte e as severidades dos chamados, veja [Entrando em contato com o suporte ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](/docs/support/index.html#contacting-support).

<!--Add a heading and content for how to get help. (Support not available for experimental.) Use this template for experimental services:  -->

