{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .pre}


# IBM Bluemix Runtime for Swift
{: #swift_runtime}
Última atualização: 19 de setembro de 2016
{: .last-updated}

O Runtime for Swift on {{site.data.keyword.Bluemix}} é desenvolvido com o [IBM Bluemix buildpack for Swift](https://github.com/IBM-Swift/swift-buildpack)
(ou seja, swift_buildpack).
Esse buildpack fornece um ambiente de tempo de execução para aplicativos Swift.
{: shortdesc}

## Aplicativo iniciador
{: #starter_application}

O {{site.data.keyword.Bluemix}} fornece um [aplicativo iniciador](https://github.com/IBM-Swift/Kitura-Starter-Bluemix)
Swift baseado em Kitura. O aplicativo iniciador Kitura é um aplicativo Swift simples que pode
ser usado para aprender sobre os tipos de aplicativos de servidores que podem ser desenvolvidos
usando a linguagem de programação Swift. Esse aplicativo de amostra cria um servidor HTTP Kitura
que retorna conteúdo HTML para o cliente.

**Nota:** o aplicativo iniciador Kitura é destinado a ser usado para
propósitos educacionais. É possível experimentar com o aplicativo iniciador ao fazer aprimoramentos
e enviar essas mudanças por push para o ambiente do {{site.data.keyword.Bluemix}}. Veja [Usando os aplicativos iniciadores](../../cfapps/starter_app_usage.html) para
obter ajuda com o uso do aplicativo iniciador.

## Renomeando o seu aplicativo
{: #renaming_your_app}

Se você deseja renomear o seu aplicativo, seja a partir do Kitura Starter ou de uma forma mais geral, há algumas mudanças que precisam ser abordadas. Isso evitará confusões e garantirá uma implementação sem erros.

- Renomeie a pasta do projeto do Aplicativo para corresponder ao nome do seu aplicativo.
- `Package.swift` - mude as entradas a seguir:
    - `name` - deve corresponder ao nome do aplicativo
    - `targets[Target(name:)]` - deve corresponder ao nome do aplicativo
- `manifest.yml` - mude as entradas a seguir;
    - `name` - deve corresponder ao nome do aplicativo
    - `host` - representa o segmento do host primário da URL do aplicativo
- `Procfile` - o valor para `web` deve corresponder ao nome de diretório do aplicativo. Esse é o comando executado após a compilação iniciar o aplicativo da web.


## Versões de runtime
{: #runtime_versions}

Por padrão, o Runtime for Swift (swift_buildpack) hospedado no {{site.data.keyword.Bluemix}} usa a versão de disponibilidade geral mais recente dos binários Swift. Essa é a única versão
da Swift diretamente suportada pela IBM e é a versão recomendada a usar em seu aplicativo. É possível
determinar essa versão suportada ao examinar as [informações de liberação
mais recentes](https://github.com/IBM-Swift/swift-buildpack/releases) do swift_buildpack. O buildpack pode listar outras versões da Swift,
conforme mostrado em seu arquivo [manifest.yml](https://github.com/IBM-Swift/swift-buildpack/blob/master/manifest.yml). Essas versões comuns, mas não suportadas, da Swift são pré-armazenadas em cache dentro do buildpack,
que fornece tempo de provisionamento reduzido.

Se você desejar usar uma versão diferente da Swift no {{site.data.keyword.Bluemix}}
para o seu aplicativo, será possível especificar a versão com um arquivo `.swift-version`
na raiz do seu repositório. Esse arquivo `.swift-version` define qual versão
da Swift deve ser usada pelo swift_buildpack.

```
$ cat .swift-version
3.0
```
{: pre}

Como há atualizações frequentes da linguagem Swift, é necessário incluir sempre um arquivo `.swift-version` para que o seu aplicativo seja "fixado" à versão da Swift
com a qual seu aplicativo é conhecido por funcionar.

Observe que é possível especificar qualquer versão válida da Swift em seu arquivo
`.swift-version`. Essas versões alternativas devem corresponder à nomenclatura
e são obtidas diretamente do endereço [Swift.org](https://swift.org/download/). 
Embora o uso de uma versão que não seja de cache leve mais tempo para ser provisionado, não há diferença de desempenho de tempo de execução do seu aplicativo Swift.

O swift_buildpack padrão no {{site.data.keyword.Bluemix}} será usado se o diretório-raiz
do seu aplicativo contiver um arquivo `Package.swift`. Se você desejar usar um
buildpack alternativo, deverá especificar isso ao incluir uma entrada `buildpack: {buildpackUrl}` no arquivo manifest.yml do seu aplicativo. Como alternativa, é possível definir isso no momento da implementação, usando o argumento do comando `cf push -b {buildpackUrl}`.


## Ambientes do desenvolvedor

Os desenvolvedores têm várias opções ao criar aplicativos do lado do servidor com a Swift. Os desenvolvedores que estão usando um dispositivo MacOS da Apple podem preferir usar o IDE Xcode, embora isso
não seja um requisito. Os aplicativos baseados em Swift que serão implementados e executados no
{{site.data.keyword.Bluemix}} poderão usar qualquer editor de programação ou IDE. O destaque
e o linting da sintaxe para Swift estão disponíveis para muitos editores populares. A ferramenta de
linha de comandos Swift REPL incluída nos binários do endereço [Swift.org](https://swift.org/),
permite a compilação local e o teste antes da implementação no {{site.data.keyword.Bluemix}}.

Para usuários do MaxOS, é possível usar o [IBM Cloud Tools for Swift](http://cloudtools.bluemix.net/) que simplifica a criação, a implementação, o gerenciamento e o controle dos aplicativos Swift do lado do servidor em execução no {{site.data.keyword.Bluemix}}.  


## Integração aprimorada

Trabalhar com a [estrutura da web Kitura](http://ibm-swift.github.io/Kitura/)
fornece uma grande quantidade de recursos. A Kitura é modular por natureza e em breve você desejará
ampliar a sua funcionalidade com pacotes de SDKs para fornecer recursos como autenticação, acesso a serviços baseados no Watson e uma ampla variedade de bancos de dados. A Kitura fornece suporte direto para muitos bancos de dados, embora outros projetos de software livre também forneçam SDKs para muitas plataformas de banco de dados. A seguir está uma lista incompleta de SDKs fornecidos pela Kitura para trabalhar com recursos externos.

- [IBM Watson](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/swift-watson-sdk)
- [IBM DB2 e DashDB](https://swiftpkgs.ng.bluemix.net/package/IBM-DTeam/swift-for-db2)
- [IBM Cloudant e Couchbase](https://swiftpkgs.ng.bluemix.net/package/cloudant/swift-cloudant)
- [IBM ObjectStorage](https://swiftpkgs.ng.bluemix.net/package/ibm-bluemix-mobile-services/bluemix-objectstorage-serversdk-swift)
- [Apache Cassandra](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/Kassandra)
- [Aphid MQTT](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/Aphid)

Para localizar mais pacotes Swift para incluir em seu aplicativo, acesse o [IBM Swift Package Catalog](https://swiftpkgs.ng.bluemix.net/) e execute uma procura em seu serviço ou banco de dados de destino. O Package Catalog fornece uma maneira fácil de localizar pacotes que podem ser incluídos em seus aplicativos Swift. Os pacotes podem ser incluídos em um aplicativo Swift ao incluir a URL do Git do pacote e os detalhes da versão no arquivo `Package.swift` do aplicativo. Para obter mais detalhes sobre o gerenciamento de pacotes, consulte a seção
[Package Manager do endereço Swift.org](https://swift.org/package-manager/).


## Informações relacionadas

Também há outras ferramentas on-line disponíveis para o desenvolvedor da Swift na IBM.
- [IBM Swift DevCenter](https://developer.ibm.com/swift/) - site de entrada principal para todas as informações do IBM Swift. É possível localizar informações sobre nossas ofertas, blogs, eventos sociais, documentação e mais.
- [IBM Swift Sandbox](https://swiftlang.ng.bluemix.net/) - esse site fornece um ambiente para que você teste fragmentos de código da Swift de maneira rápida e fácil com relação a várias versões da Swift e até mesmo em diferentes plataformas de tempo de execução Swift. Também é possível salvar e compartilhar amostras de código com outras pessoas, bem como explorar exemplos populares fornecidos por outros usuários.


# links relacionados
{: #rellinks}
## geral
{: #general}
* [IBM Swift DevCenter](https://developer.ibm.com/swift/)
* [IBM Cloud Tools for Swift](http://cloudtools.bluemix.net/)
* [IBM Swift Package Catalog](https://swiftpkgs.ng.bluemix.net/)
* [IBM Swift Sandbox](https://swiftlang.ng.bluemix.net/)
* [Documentação e APIs da Kitura](http://ibm-swift.github.io/Kitura/)
* [Aplicativo Kitura Starter para Bluemix](https://github.com/IBM-Swift/Kitura-Starter-Bluemix)
* [IBM Bluemix buildpack for Swift](https://github.com/IBM-Swift/swift-buildpack)
* [Notas sobre a liberação
do IBM Bluemix buildpack for Swift](https://github.com/IBM-Swift/swift-buildpack/releases)
* [Swift.org](https://swift.org/)
* [Documentação da linguagem Swift](https://swift.org/documentation)
