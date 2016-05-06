{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .pre}


# Tempo de execução do Swift
{: #swift_runtime}
*Última atualização: 19 de fevereiro de 2016*

O tempo de execução do Swift no {{site.data.keyword.Bluemix}} foi desenvolvido pelo swift_buildpack.
O swift_buildpack fornece um ambiente de tempo de execução completo para apps Swift.
{: shortdesc}

O swift_buildpack será usado se o diretório-raiz de seu app contiver um arquivo Package.swift.

## Aplicativo iniciador
{: #starter_application}

O {{site.data.keyword.Bluemix}} fornece um aplicativo iniciador do Swift. O app iniciador do Swift é um app Swift simples que pode ser usado para aprender sobre os tipos de aplicativos do servidor que é possível desenvolver usando a linguagem de programação Swift. Esse app de amostra cria um servidor básico que retorna uma saudação HTML ao cliente.  

**Nota:** esse app iniciador não é um aplicativo pronto para produção.  Em vez disso, ele destina-se a ser usado para propósitos educacionais.  É possível experimentar o app iniciador, fazendo e enviando mudanças por push para o
ambiente {{site.data.keyword.Bluemix}}. Consulte [Usando os aplicativos iniciadores](../../cfapps/starter_app_usage.html) para obter ajuda sobre o uso
do aplicativo iniciador.

## Versões de tempo de execução
{: #runtime_versions}

É possível especificar a versão do Swift a ser usada por seu app com um arquivo `.swift`-version na raiz de seu repositório:

```
cat .swift-version
swift-DEVELOPMENT-SNAPSHOT-2016-02-03-a
```
{: pre}

Para obter uma lista completa das versões suportadas do Swift, consulte o arquivo [manifest.yml](https://github.com/cloudfoundry-community/swift-buildpack/blob/master/manifest.yml) do buildpack.

Para obter detalhes sobre a versão atual do buildpack do Swift que está instalado no {{site.data.keyword.Bluemix}}, consulte as [informações sobre a liberação](https://github.com/cloudfoundry-community/swift-buildpack/releases/tag/v1.0.3) do buildpack.

Como há frequentes mudanças de idioma do Swift, é necessário incluir um arquivo .swift-version para que seu app fique "fixado" à versão do Swift com a qual sabe-se que o aplicativo trabalha.

# rellinks
## geral
* [Buildpack do Cloud Foundry para o Swift](https://github.com/cloudfoundry-community/swift-buildpack)
* [Documentação de idioma do Swift](https://swift.org/)
