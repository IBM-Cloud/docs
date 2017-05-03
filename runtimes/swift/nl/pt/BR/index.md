---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# IBM Bluemix Runtime for Swift
{: #swift_runtime}

O Runtime for Swift on {{site.data.keyword.Bluemix}} é desenvolvido com o [IBM Bluemix buildpack for Swift](https://github.com/IBM-Swift/swift-buildpack)
(ou seja, swift_buildpack).
Esse buildpack fornece um ambiente de tempo de execução completo para aplicativos Swift.
{: shortdesc}

## Aplicativo iniciador
{: #starter_application}

O {{site.data.keyword.Bluemix}} fornece um [aplicativo
iniciador](https://github.com/IBM-Bluemix/Kitura-Starter) Swift baseado no Kitura. O app iniciador Kitura é um app Swift
simples que pode ser usado para saber mais sobre os tipos de aplicativos de servidor que
é possível desenvolver usando a linguagem de programação Swift. Esse app de amostra
cria um servidor HTTP Kitura básico que retorna conteúdo HTML para o cliente.

**Nota:** o aplicativo iniciador Kitura é destinado a ser usado para
propósitos educacionais. É possível experimentar o app iniciador, fazendo aprimoramentos e
enviando essas mudanças por push para o ambiente {{site.data.keyword.Bluemix}}. Consulte [Usando os aplicativos iniciadores](../../cfapps/starter_app_usage.html) para obter ajuda sobre o uso
do aplicativo iniciador.

## Renomeando seu app
{: #renaming_your_app}

Se desejar renomear seu aplicativo, a partir do iniciador do Kitura ou em geral, haverá algumas
mudanças que precisarão ser feitas. Isso evitará confusão e assegurará uma
implementação sem erros.

- Renomeie a pasta do projeto do aplicativo para corresponder ao nome de seu app.
- `Package.swift` - Mude as entradas a seguir:
    - `name` - deve corresponder ao nome do app.
    - `targets[Target(name:)]` - deve corresponder ao nome do aplicativo
- `manifest.yml` - mude as entradas a seguir:
    - `name` - deve corresponder ao nome do app.
    - `Comando` - o nome do executável para iniciar seu aplicativo (deve corresponder ao
nome especificado no arquivo Package.swift).

## Versões de tempo de execução
{: #runtime_versions}

Por padrão, o Runtime for Swift (swift_buildpack) hospedado no {{site.data.keyword.Bluemix}} usa a versão de disponibilidade geral mais recente dos binários Swift. Essa é a única versão do Swift diretamente suportada pela IBM, sendo a versão recomendada para uso em seu app. É possível determinar essa versão suportada examinando as [informações sobre a liberação mais recentes](https://github.com/IBM-Swift/swift-buildpack/releases) do swift_buildpack. O buildpack pode listar outras versões do Swift conforme mostradas em seu arquivo [manifest.yml](https://github.com/IBM-Swift/swift-buildpack/blob/master/manifest.yml). Essas versões comuns, mas não suportadas, do Swift são pré-armazenadas em cache dentro do buildpack, que fornecem tempo de provisão reduzido.

Se você desejar usar uma versão diferente do Swift no {{site.data.keyword.Bluemix}} para seu aplicativo, poderá especificar a versão com um arquivo `.swift-version` na raiz do repositório. Esse arquivo `.swift-version` define qual versão do Swift deve ser usada pelo swift_buildpack.

```
$ cat .swift-version
3.0
```
{: pre}

Como há atualizações frequentes de idioma do Swift, sempre será necessário incluir um arquivo `.swift-version` para que seu app seja "fixado" à versão do Swift com a
qual sabe-se que seu aplicativo funciona.

Observe que é possível especificar qualquer versão válida do Swift em seu arquivo
`.swift-version`. Essas versões alternativas devem corresponder à nomenclatura e serem puxadas diretamente de [Swift.org ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://swift.org/download/). Embora o uso de uma versão
não em cache levará um pouco mais de tempo para provisionar, não há diferença de
desempenho de tempo de execução de seu app Swift.

O swift_buildpack padrão no {{site.data.keyword.Bluemix}} será usado se o
diretório-raiz do seu app contiver um arquivo `Package.swift`.  Se
você desejar usar um buildpack alternativo, deverá especificar isso
incluindo uma entrada
`buildpack: {buildpackUrl}` no arquivo manifest.yml do seu app. Como
alternativa, é possível definir isso no momento da implementação, usando o
argumento de comando `cf push -b {buildpackUrl}`.


## Ambientes do desenvolvedor

Os desenvolvedores têm diversas opções ao criar aplicativos do lado do servidor com
o Swift. Aqueles que usam um dispositivo MacOS da Apple podem preferir usar o Xcode IDE,
embora este não seja um requisito.  Apps baseados no Swift que serão implementados e
executados no {{site.data.keyword.Bluemix}} podem usar qualquer editor de
programação ou IDE.  O destaque e a claridade da sintaxe para Swift estão disponíveis para
muitos editores populares. A ferramenta de linha de comandos REPL do Swift incluída nos binários de [Swift.org ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://swift.org/) permite compilação local e teste antes da implementação no {{site.data.keyword.Bluemix}}.

Para usuários do MaxOS, é possível usar o [IBM
Cloud Tools for Swift](http://cloudtools.bluemix.net/) que simplifica a criação, a implementação, o gerenciamento e o
controle de apps Swift do lado do servidor em execução no {{site.data.keyword.Bluemix}}.  


## Integração Aprimorada

O trabalho com a [estrutura da web Kitura](http://ibm-swift.github.io/Kitura/) fornece uma grande negociação de recursos. O Kitura é modular por natureza e você logo irá querer estender sua funcionalidade com SDKs empacotados, para fornecer recursos como autenticação, acesso a serviços baseados no Watson e uma ampla variedade de bancos de dados.  O Kitura fornece suporte para muitos bancos de dados diretamente, enquanto outros projetos de software livre também fornecem SDKs para muitas plataformas de banco de dados. A seguir está uma lista incompleta de SDKs fornecidos pela Kitura para trabalhar com recursos externos.

- [IBM Watson](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/swift-watson-sdk)
- [IBM DB2 e DashDB](https://swiftpkgs.ng.bluemix.net/package/IBM-DTeam/swift-for-db2)
- [IBM Cloudant and CouchDB](https://swiftpkgs.ng.bluemix.net/package/cloudant/swift-cloudant)
- [IBM ObjectStorage](https://swiftpkgs.ng.bluemix.net/package/ibm-bluemix-mobile-services/bluemix-objectstorage-serversdk-swift)
- [Apache Cassandra](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/Kassandra)
- [Aphid MQTT](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/Aphid)

Para saber mais sobre pacotes do Swift a serem incluídos em seu aplicativo, acesse o [Catálogo de pacotes do IBM Swift](https://swiftpkgs.ng.bluemix.net/) e execute uma procura no seu serviço ou banco de dados de destino. O Catálogo de pacotes oferece uma maneira fácil de localizar pacotes que podem ser incluídos nos aplicativos Swift. Os pacotes podem ser incluídos em um aplicativo Swift incluindo a URL do Git e os detalhes da versão do pacote no arquivo `Package.swift` do app. Para obter mais detalhes sobre gerenciamento de pacote, consulte a [seção Package Manager do Swift.org](https://swift.org/package-manager/).


## Informações Relacionadas

Existem também outras ferramentas on-line disponíveis na IBM para o desenvolvedor do Swift.
- [IBM Swift DevCenter](https://developer.ibm.com/swift/) -
site de entrada principal para todas as informações do IBM Swift. É possível encontrar informações sobre nossas ofertas, blogs, eventos sociais, documentação e muito mais.
- [IBM Swift Sandbox](https://swiftlang.ng.bluemix.net/) - esse
site fornece um ambiente para que você teste de maneira rápida e fácil nossos fragmentos
de código do Swift com relação a diversas versões do Swift, mesmo em diferentes
plataformas de tempo de execução do Swift. É possível também salvar e compartilhar
amostras de código com outros, bem como explorar exemplos populares fornecidos por outros.


# rellinks
{: #rellinks notoc}
## geral
{: #general notoc}
* [IBM Swift DevCenter](https://developer.ibm.com/swift/)
* [IBM Cloud Tools for Swift](http://cloudtools.bluemix.net/)
* [Catálogo de pacotes do IBM Swift](https://swiftpkgs.ng.bluemix.net/)
* [IBM Swift Sandbox](https://swiftlang.ng.bluemix.net/)
* [Documentação e APIs do Kitura](http://ibm-swift.github.io/Kitura/)
* [App Starter Kitura para Bluemix](https://github.com/IBM-Bluemix/Kitura-Starter)
* [IBM Bluemix buildpack for Swift](https://github.com/IBM-Swift/swift-buildpack)
* [Notas sobre a liberação
do IBM Bluemix buildpack for Swift](https://github.com/IBM-Swift/swift-buildpack/releases)
* [Swift.org ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://swift.org/)
* [Documentação da linguagem Swift ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://swift.org/documentation)
