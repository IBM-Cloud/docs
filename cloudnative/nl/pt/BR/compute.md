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

# Cálculo
{: #compute}

Quando você estiver construindo um aplicativo de canal digital nativo de nuvem para web e dispositivo móvel, a melhor prática será ter um Backend for Frontend (BFF) que seja dedicado ao canal digital ou que ofereça o mesmo suporte de integração de dados e lógico para os apps da web e do cliente móvel. Para obter mais informações sobre essa arquitetura, veja [Microsserviços para web e dispositivo móvel ![Ícone de link externo](../icons/launch-glyph.svg)](https://www.ibm.com/devops/method/content/architecture/omnichannelArchitecture).

O diagrama a seguir mostra uma visão geral da arquitetura do BFF.

![Arquitetura do BFF](images/bff-arch.png)

Figura 1: Arquitetura do BFF

O conceito de um BFF é separar a lógica de negócios comum e a lógica de integração dos microsserviços ou dos serviços de nuvem de alto valor do {{site.data.keyword.Bluemix}}.

Com essa arquitetura, é possível implementar e liberar atualizações para seu aplicativo móvel ou da web e implementar novas versões do BFF usando pipelines de entrega contínua com o serviço dev ops.

Se você tiver um BFF para iOS e um BFF separado para Android, as equipes de engenharia que estarão entregando a função para esses apps não serão restringidas a liberar recursos por um planejamento de liberação de API centralizado. Esse é um objetivo comum para arquiteturas de canal de microsserviço e digital - liberar as equipes para liberar função e recursos com frequência, sem estarem fortemente acopladas ao planejamento de liberação de outra equipe.

<!--
## Backend for Frontends (BFF)
{: #bff}

Backend for Frontend patterns, commonly known as BFFs, really help you to focus on exposing business data and services in a form that matches the user interaction requirements. To optimize a user journey to your cloud solution, it may require a different user journey for the mobile application and a richer, more detailed journey for the Web application. With the introduction of voice-controlled devices like the [{{site.data.keyword.conversationfull}} ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/conversation.html) service, the interaction with a user could be controlled by voice. This digital channel will require a very different BFF for managing these voice intent-based interactions.

With {{site.data.keyword.Bluemix_notm}}, you can build a BFF by using polyglot programming approach to define the BFF. IBM recommends using Node, Swift, or Java and running them in a cloud native pattern with either Cloud Foundry, Container services, or serverless.

The BFF will manage the integration with services for data persistence, caching, and integration with high-value services like {{site.data.keyword.ibmwatson}}, {{site.data.keyword.iot_short_notm}}, {{site.data.keyword.weather_short}}, and data analytics like {{site.data.keyword.sparks}}.

The BFF will expose an API most commonly using a REST pattern, but you can design your BFF to work from a messaging architecture using {{site.data.keyword.messagehub}}.
-->


## Integrando um cliente móvel a um Backend for Frontend
{: #integration}

Para ativar a fácil integração entre um cliente móvel e um BFF, o {{site.data.keyword.Bluemix_notm}} suportará a geração de SDK do cliente móvel para iOS e Android nas linguagens Swift e Java, respectivamente. Para ativar esse recurso, deve-se expor a integração do BFF usando um documento de especificação de Open API (Swagger). Esse documento poderá estar no formato de JSON ou YAML.

O gerador de SDK do cliente usa o arquivo de definição de Open API para definir um SDK do desenvolver otimizado pelo cliente que seja fácil de consumir no aplicativo móvel nativo. Ele acelerará a integração de seu BFF para o aplicativo móvel.


## Definindo uma API
{: #definition}

O BFF precisa expor um arquivo de definição de API que seja adequado à especificação de Open API que está em execução em um end point do servidor em tempo real. Para ativar o {{site.data.keyword.Bluemix_notm}} Developer Experience e o {{site.data.keyword.Bluemix_notm}} SDK CLI (Interface da linha de comandos) para descobrir esse terminal, deve-se incluir uma variável de ambiente no aplicativo Cloud Foundry chamada `OPENAPI_SPEC`. Essa variável de ambiente deve referenciar a especificação usando um caminho relativo.

Para incluir a variável de ambiente `OPENAPI_SPEC` no {{site.data.keyword.Bluemix_notm}}, siga estas etapas:

1. Efetue login no [{{site.data.keyword.Bluemix_notm}} ![Ícone de link externo](../icons/launch-glyph.svg)](http://bluemix.net).
2. Selecione um app Cloud Foundry.
3. Selecione **Tempo de execução**.
4. Selecione **Variáveis de ambiente**.
5. Clique em **Incluir** na seção **Definido pelo usuário**.
6. Especifique `OPENAPI_SPEC` para **NOME** e um caminho de URL relativa para seu arquivo de definição de Open API.
7. Clique em **Salvar**.

<!--
To add the `OPENAPI_SPEC` environment variable locally and push your changes to {{site.data.keyword.Bluemix_notm}} with the [Cloud Foundry CLI ![External link icon](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli#getting-started), follow these steps:

1. Open Terminal and navigate to your project directory.
2. Add the following code to the `manifest.yml` file.

   ```
   env:
       "OPENAPI_SPEC": "<relative URL path to your Open API definition file>"
   ```
   {: codeblock}
3. Save your changes to the `manifest.yml` file.
4. Run `cf push` to deploy the changes to {{site.data.keyword.Bluemix_notm}}.
-->

Por exemplo:

```
OPENAPI_SPEC='/explorer/swagger.json'
```
{: codeblock}

Os aplicativos {{site.data.keyword.apiconnect_long}} e Loopback funcionam especialmente bem ao usar essa abordagem. É possível usar o Loopback e o {{site.data.keyword.apiconnect_short}} para definir um modelo persistente e expor a operação CRUD (Create, Read, Update, and Delete) usando o arquivo de definição de Open API.

Também é possível definir operações de lógica de negócios.


### Elementos suportados da especificação de Open API
{: #supported-elements notoc}

A única parte da especificação de Open API que não é totalmente suportada é a estrutura do arquivo. A especificação permite que partes da definição sejam divididas em arquivos diferentes e referenciadas usando o campo json `$ref`. Sua definição inteira deve estar contida em um arquivo.


## Exemplo de Backend for Frontend usando Bluegen
{: #bff-bluegen}

O {{site.data.keyword.Bluemix_notm}} criou um BFF de referência usando o {{site.data.keyword.apiconnect_short}} e o Strongloop, que mapeiam um modelo de produto para um {{site.data.keyword.cloudant}} e uma API de imagem para referenciar imagens no {{site.data.keyword.objectstorageshort}}.

É possível usar esse padrão de BFF para iniciar rapidamente o fornecimento de um BFF totalmente funcional para o {{site.data.keyword.Bluemix_notm}} e usá-lo para ajudar a entender como é fácil integrar um BFF a um projeto móvel e gerar SDKs nativos para iOS e Android no Swift e Java, respectivamente.

Siga as instruções do [LEIA-ME ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-bluemix-mobile-services/backend-for-frontend-node) para criar e instalar um projeto.


## Usando o Backend for Frontend com um projeto do Developer Experience
{: #bff-devex}

O {{site.data.keyword.Bluemix_notm}} Mobile Developer Experience foi projetado para simplificar a definição de um projeto móvel com vários serviços de nuvem associados. É possível incluir facilmente os serviços [{{site.data.keyword.mobilepushshort}} ![Ícone de link externo](../icons/launch-glyph.svg)](/docs/services/mobilepush/index.html), [Analytics ![Ícone de link externo](../icons/launch-glyph.svg)](/docs/services/mobileanalytics/index.html) e Data ou Storage.

O {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} introduziu a capacidade de integrar um BFF a um projeto móvel na página **Cálculo**. É possível incluir instâncias de serviço de Cálculo existentes em seu projeto móvel. Depois se serem incluídas, será possível gerar um SDK nativo para sua opção de linguagem ou gerar o projeto completo e o SDK será integrado ao pacote de origem do projeto na página **Código**. Isso será especialmente útil quando você estiver integrando a BFFs já bem definidos.

Depois de ter transferido seu projeto por download, será possível abri-lo com Xcode ou Android Studio e compilá-lo com o SDK do cliente.


## Utilizando o CLI
{: #cli}

Conforme o BFF estiver sendo desenvolvido, a especificação de API poderá mudar. Para suportar essas mudanças, você tem as duas opções a seguir.

* Gerar novamente o projeto inteiro em uma nova ramificação de GitHub e mesclar as mudanças na ramificação de desenvolvimento.
* Gerar novamente o SDK diretamente usando a ferramenta de linha de comandos (CLI) e atualizar apenas a parte de SDK do projeto móvel.

Para usar a CLI, deve-se [instalá-la](sdk_cli.html#installation).

Use o comando a seguir para listar as ações que podem ser executadas.

```
bluemix sdk
```
{: codeblock}

Use o comando a seguir para listar as instâncias em execução do Cloud Foundry no espaço atual do {{site.data.keyword.Bluemix_notm}}.

```
bluemix sdk list
```
{: codeblock}

Cada app é listado e a API será validada se a variável de ambiente `OPENAPI_SPEC` estiver configurada. Na coluna `VALID`, você verá um visto verde ou um `X` vermelho. Um visto na coluna `VALID` do aplicativo significa que uma definição válida de Open API está presente. Um `X` na coluna `VALID` do aplicativo significa uma de duas coisas:

* uma variável de ambiente `OPENAPI_SPEC` não está definida para o aplicativo OU
* a definição de API não é válida com relação à especificação de Open API

Use o comando a seguir para visualizar a URL completamente formada para a API. A rota e o URI completamente formados para a especificação de API são listados. É possível visualizar a especificação bruta em um navegador, consumi-la diretamente na CLI ou verificar se a variável de ambiente `OPENAPI_SPEC` do BFF está configurada corretamente.

```
bluemix sdk list --url
```
{: codeblock}

Use o comando a seguir para validar o arquivo de definição de Open API do `<AppName>` para determinar se ele pode ser usado para gerar um SDK. O comando localiza `<AppName>` no espaço atual e usa o caminho relativo na variável de ambiente `OPENAPI_SPEC` para localizar a especificação para validação.

```
bluemix sdk validate <AppName>
```
{: codeblock}

Use o comando a seguir para gerar um SDK para a `< Platform>` nativa de sua preferência e colocar um arquivo compactado no diretório atualmente em funcionamento.

```
bluemix sdk generate <AppName> <SDKName> --<Platform>
```
{: codeblock}

O uso da opção `--unzip` extrairá automaticamente o SDK no diretório atualmente em funcionamento. Opcionalmente, será possível especificar o local para extrair o SDK usando a opção `--output`. É possível gerenciar o código-fonte com GitHub e criar uma nova ramificação especificamente para atualizar o SDK. O uso dessa abordagem facilita a visualização das mudanças e a mesclagem no SDK atualizado na ramificação de desenvolvimento.


## Trabalhando com modelos e APIs gerados pelo SDK
{: #models-apis}

Agora que o BFF foi integrado ao app móvel usando um SDK gerado, será possível iniciar o trabalho com ele.

O SDK vem com documentação totalmente gerada nos diretórios `docs` e `source`. É possível abrir o arquivo `README.html` para uma visualização na web dos docs ou abrir o arquivo `README.md` para uma visualização de Redução de preço dos docs. Os docs de Redução de preço são úteis quando você está publicando o SDK no Cocoapods ou no Maven Central.

Na documentação, é possível ver uma lista das APIs geradas. É possível clicar na API para ver um fragmento de código que pode ser colado diretamente no app móvel.
