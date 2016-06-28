{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .pre}


# Tempo de execução do Swift
{: #swift_runtime}
*Última atualização: 10 de junho de 2016*
{: .last-updated}

O tempo de execução Swift no {{site.data.keyword.Bluemix}} é desenvolvido
com o buildpack do Swift para Bluemix (isto é, swift_buildpack).
O swift_buildpack fornece um ambiente de tempo de execução completo para aplicativos Swift.
{: shortdesc}

O swift_buildpack será usado se o diretório-raiz de seu app contiver um arquivo Package.swift.

## Aplicativo iniciador
{: #starter_application}

O {{site.data.keyword.Bluemix}} fornece um aplicativo iniciador do Swift. O app iniciador do Swift é um app Swift simples que pode ser usado para aprender sobre os tipos de aplicativos do servidor que é possível desenvolver usando a linguagem de programação Swift. Esse app de amostra cria um servidor HTTP básico que retorna conteúdo HTML ao cliente.

**Nota:** esse app iniciador não é um aplicativo pronto para produção.  Em vez disso, ele destina-se a ser usado para propósitos educacionais.  É possível experimentar o app iniciador, fazendo e enviando mudanças por push para o
ambiente {{site.data.keyword.Bluemix}}. Consulte [Usando os aplicativos iniciadores](../../cfapps/starter_app_usage.html) para obter ajuda sobre o uso
do aplicativo iniciador.

## Versões de tempo de execução
{: #runtime_versions}

O swift_buildpack instalado no Bluemix suporta a versão
`DEVELOPMENT-SNAPSHOT-2016-05-03-a` dos binários do Swift. Se você
quiser usar uma versão diferente do Swift no Bluemix para seu aplicativo, será possível
especificar a versão com um arquivo `.swift-version` na raiz do
repositório:

```
cat .swift-version
swift-DEVELOPMENT-SNAPSHOT-2016-04-25-a
```
{: pre}

Além de incluir um arquivo `.swift-version`, você precisaria
incluir o parâmetro `-b https://github.com/IBM-Swift/swift-buildpack` no
comando `cf push`, conforme mostrado abaixo:

```
cf push -b https://github.com/IBM-Swift/swift-buildpack
```

Para obter uma lista completa das versões suportadas do Swift, consulte o arquivo [manifest.yml](https://github.com/IBM-Swift/swift-buildpack/blob/bluemix-buildpack/manifest.yml) do buildpack.

Para obter detalhes sobre a versão atual do buildpack do Swift que está instalado no {{site.data.keyword.Bluemix}}, consulte as [informações sobre a liberação](https://github.com/IBM-Swift/swift-buildpack/releases/tag/1.1.1) do buildpack.

Como há mudanças frequentes de idioma do Swift, será necessário incluir um
arquivo `.swift-version` para que seu app seja "fixado" à versão do Swift com a qual sabe-se que seu aplicativo funciona. Lembre-se também de que se você estiver usando uma versão do Swift diferente de
`DEVELOPMENT-SNAPSHOT-2016-05-03-a`, será necessário especificar o parâmetro `-b https://github.com/IBM-Swift/swift-buildpack` ao enviar seu app por push (conforme mostrado acima).

# rellinks
{: #rellinks}
## geral
{: #general}
* [Buildpack do Swift para Bluemix](https://github.com/IBM-Swift/swift-buildpack)
* [Documentação de idioma do Swift](https://swift.org/)
