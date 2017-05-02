---

copyright:
  years: 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Plug-in do SDK Generator
{: #sdk-cli}

O plug-in do {{site.data.keyword.IBM}} SDK Generator pode ser instalado no [{{site.data.keyword.Bluemix_notm}} CLI ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](/docs/cli/reference/bluemix_cli/index.html).

Como um desenvolvedor no {{site.data.keyword.Bluemix_notm}}, é possível usar esse plug-in para gerar os SDKs de sua definição de API de REST compatível com a [Especificação da Open API ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.openapis.org/). À medida que você faz mudanças na definição de API de REST, é possível usar esse plug-in para gerar novamente apenas o SDK, em vez de gerar novamente o projeto inteiro.

Também será possível ver se os apps Cloud Foundry em um determinado espaço possuírem definições de API de REST que são válidas para geração de SDK. Finalmente, é possível usar o plug-in do {{site.data.keyword.IBM_notm}} SDK Generator para validar quaisquer definições de API de REST para assegurar-se de que obedeçam aos requisitos do gerador de SDK.

Esse plug-in do {{site.data.keyword.IBM_notm}} SDK Generator permite integrar facilmente seus serviços de backend ao app com um SDK gerado. Quando ocorrer uma mudança em uma API de REST, será possível gerar novamente o SDK e substituir o antigo para um upgrade ininterrupto de SDK. Também será possível integrar a CLI a um pipeline devops e assegurar-se de que o SDK esteja sempre consistente com a especificação de API sempre que o app for construído.

A definição de API de REST deve ser válida e hospedada em um end point do servidor em tempo real ou em um arquivo local no sistema. Se a definição de API de REST for hospedada, a URL relativa deverá ser definida na variável de ambiente `OPENAPI_SPEC`.


## Requisitos
{: #prereqs}

Assegure-se de satisfazer os requisitos a seguir.

* Você tem uma conta do [{{site.data.keyword.Bluemix_notm}} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](http://bluemix.net)
* Uma definição de API válida que é adequada à especificação de [Open API ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.openapis.org/)


## Instalação
{: #installation}

1. [Instale o {{site.data.keyword.Bluemix}} CLI ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](http://clis.ng.bluemix.net/ui/home.html).

2. [Instale o plug-in ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](/docs/cli/reference/bluemix_cli/index.html#install_plug-in).

	```
	bx plugin install sdk-gen -r Bluemix
	```
	{: codeblock}


## Comandos
{: #commands}

Use os comandos a seguir para gerar um SDK, validar os arquivos de definição da Open API ou listar apps do Cloud Foundry.


### Gerando um SDK
{: #gen}

Use `bluemix sdk generate [arguments...][command options]`.


#### Argumentos
{: #gen-args}

* `APP_NAME` - o nome do app Cloud Foundry em seu espaço atual
* `OPENAPI_DOC_LOCATION` - uma URL ou um caminho de arquivo relativo para a definição de API de REST bruta JSON ou Yaml
* `GENERATED_SDK_NAME` (opcional) - o nome do SDK gerado


#### opções
{: #gen-options}

* `PLATFORM` (necessário)
   * `--android` - gerar um SDK do Android
   * `--ios` - gerar um SDK do iOS Swift
   * `--swift` - gerar um SDK do servidor Swift
* `--output "YOUR_RELATIVE_PATH"` (opcional) - coloca o SDK gerado no diretório especificado por `YOUR_RELATIVE_PATH` (será sobrescrito se o SDK existente estiver presente)
* `--unzip` (opcional) - extrai o SDK gerado (será sobrescrito se artefatos SDK existentes estiverem presentes)


#### Uso
{: #gen-usage}

Para gerar um SDK de um app Cloud Foundry que está em execução no {{site.data.keyword.Bluemix_notm}}, é possível usar o nome do app como um parâmetro para a CLI. O comando a seguir usa o nome do app como o `SDK_Name`.

```
bluemix sdk generate [APP_NAME] [PLATFORM]
```
{: codeblock}

Para gerar um SDK de uma URL para um arquivo de definição de Open API ou um arquivo JSON ou Yaml local, use o comando a seguir.

```
bluemix sdk generate [OPENAPI_DOC_LOCATION] [SDK_Name] [Platform]
```
{: codeblock}


### Validando definições da Open API
{: #validating}

Use `bluemix sdk validate [argument]`.


#### Argumentos
{: #val-args}

* `APP_NAME` - o nome do app Cloud Foundry em seu espaço atual
* `OPENAPI_DOC_LOCATION` - uma URL ou um caminho de arquivo relativo para a definição de API de REST bruta JSON ou Yaml


#### Uso
{: #val-usage}

Para validar uma especificação de API do app Cloud Foundry que está em execução no {{site.data.keyword.Bluemix_notm}}, é possível usar o nome do app como um parâmetro para a CLI.

```
bluemix sdk validate [APP_NAME]
```
{: codeblock}

Para validar um SDK da URL para um documento de especificação de API ou um arquivo JSON ou Yaml local, use o comando a seguir.

```
bluemix sdk validate [OPENAPI_DOC_LOCATION]
```
{: codeblock}



### Listar apps (Cloud Foundry)
{: #list-apps}

Use `bluemix sdk list [argument][option]` para listar apps e validar especificações de API. Deve-se ter a variável de ambiente `OPENAPI_SPEC` configurada para o caminho da URL relativa que hospeda sua especificação.


#### Argumentos
{: #list-args}

* `SPACE_NAME` (opcional) - o nome do espaço do Cloud Foundry em sua organização atual na qual você deseja procurar apps. Se não fornecido, o espaço atual será procurado.


#### opções
{: #list-options}

* `--url` (opcional) - para exibir uma URL completamente formada para a definição de Open API para cada app na lista


#### Uso
{: #list-usage}

Para listar apps no espaço atual, use o comando a seguir.

```
bluemix sdk list
```
{: codeblock}

Para listar apps no espaço atual e exibir a URL de especificação de API, use o comando a seguir.

```
bluemix sdk list --url
```
{: codeblock}

Para listar apps em um espaço específico, use o comando a seguir.

```
bluemix sdk list [SPACE_NAME]
```
{: codeblock}

Para listar apps em um espaço específico e exibir a URL de especificação de API, use o comando a seguir.

```
bluemix sdk list [SPACE_NAME] --url
```
{: codeblock}
