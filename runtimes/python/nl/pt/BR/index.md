---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-25"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Python
{: #python_runtime}

O tempo de execução Python no {{site.data.keyword.Bluemix}} foi desenvolvido pelo python_buildpack.
O python_buildpack fornece um ambiente de tempo de execução completo para os apps Python 2 e Python 3.
{: shortdesc}

O python_buildpack será usado se o diretório-raiz de seu app contiver um arquivo requirements.txt ou um arquivo setup.py.

## Aplicativo iniciador
{: #starter_application}

O {{site.data.keyword.Bluemix}} fornece um aplicativo iniciador do Python.  O aplicativo iniciador do Python é um app Python simples que fornece um modelo
que pode ser usado por seu app. É possível experimentar o app iniciador, fazendo e enviando mudanças por push para o ambiente
{{site.data.keyword.Bluemix}}.  Consulte [Usando os aplicativos iniciadores](/docs/cfapps/starter_app_usage.html) para obter ajuda sobre o uso
do aplicativo iniciador.

## Versões de tempo de execução
{: #runtime_versions}

É possível especificar a versão do Python a ser usada por seu app, configurando python-versionnumber no arquivo runtime.txt
na raiz de seu aplicativo. Por exemplo:

```
python-3.5.0
```
{: codeblock}

Quando uma versão não é especificada, a versão 2.7.11 é escolhida por padrão.

### Versões disponíveis:
{: #available_versions}

As seguintes versões do Python estão disponíveis no
[buildpack Python](https://github.com/cloudfoundry/python-buildpack/releases/tag/v1.5.5) atualmente instalado no {{site.data.keyword.Bluemix}}:

* 2.7.10
* 2.7.11
* 3.3.5
* 3.3.6
* 3.4.3
* 3.4.4
* 3.5.0
* 3.5.1

Se seu aplicativo requerer uma versão do Python não listada, é possível usar o
[buildback Python](https://github.com/cloudfoundry/python-buildpack) externo para implementar o app.

# rellinks
{: #rellinks notoc}
## geral
{: #general notoc}
* [Buildpack do Cloud Foundry para Python](https://github.com/cloudfoundry/python-buildpack)
