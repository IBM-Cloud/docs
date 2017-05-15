---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-25"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Introdução ao {{site.data.keyword.openwhisk_short}}


O {{site.data.keyword.openwhisk}} é um serviço de cálculo distribuído, orientado para eventos também referido como Cálculo sem servidor ou como Função como um serviço (FaaS), o
{{site.data.keyword.openwhisk_short}} executa uma lógica de aplicativo em resposta a eventos ou chamadas diretas a partir de aplicativos da web ou móveis sobre HTTP. Os eventos
podem ser fornecidos a partir de serviços do Bluemix, como o Cloudant e a partir de
fontes externas. Os desenvolvedores podem focar a composição da lógica do aplicativo e a criação de ações que são executadas sob demanda.
Os benefícios desse novo paradigma são que você não provisiona explicitamente os servidores e se preocupa com o ajuste automático de escala ou se preocupa com a alta disponibilidade, atualizações, manutenção e pagamento por horas de tempo do processador quando o servidor está em execução, mas não está atendendo solicitações.
Seu código é executado sempre que há uma chamada HTTP, mudança de estado do banco de dados ou outro tipo de evento que aciona a execução do código.
Você é cobrado por milissegundo de tempo de execução (arredondado para os 100 ms mais próximos), não por hora de utilização da VM, independentemente se essa VM estava executando trabalho útil ou não.
{: shortdesc}

Esse modelo de programação é uma correspondência perfeita para microsserviços, dispositivos móveis, IoT e muitos outros apps – você obtém ajuste automático de escala inerente e balanceamento de carga prontos para utilização, sem precisar configurar manualmente clusters, balanceadores de carga, plug-ins http, etc. Se por acaso você executar no {{site.data.keyword.openwhisk}}, também obterá um benefício de administração zero, o que significa que todo o hardware, rede e software serão mantidos pela IBM. Tudo o que você precisa fazer é fornecer o código que deseja executar e concedê-lo ao {{site.data.keyword.openwhisk}}. O resto é “mágica”. Uma boa introdução para o modelo de programação Serverless está disponível no [blog de Martin Fowler](https://martinfowler.com/articles/serverless.html).

Também é possível obter o [Código-fonte do Apache OpenWhisk](https://github.com/openwhisk/openwhisk) e executar o sistema sozinho.

Para obter mais detalhes sobre como o {{site.data.keyword.openwhisk_short}} funciona, consulte [Sobre o {{site.data.keyword.openwhisk_short}}](./openwhisk_about.html).

É possível usar o Navegador ou a CLI para desenvolver os seus aplicativos {{site.data.keyword.openwhisk_short}}.
Ambos têm recursos semelhantes para desenvolver aplicativos; a CLI fornece mais controle sobre a sua implementação e as operações.

## Desenvolver em seu navegador
{: #openwhisk_start_editor}

Teste o {{site.data.keyword.openwhisk_short}} e seu [Navegador](https://console.{DomainName}/openwhisk/editor) para
criar ações, automatizar ações usando acionadores e explorar pacotes públicos. 
Visite a página [saiba mais](https://console.{DomainName}/openwhisk/learn) para um tour rápido da Interface com o Usuário do OpenWhisk.

## Desenvolver usando a CLI
{: #openwhisk_start_configure_cli}

É possível usar a interface da linha de comandos (CLI) do {{site.data.keyword.openwhisk_short}} para configurar o namespace e a chave de autorização.
Acesse [Configurar CLI](https://console.{DomainName}/openwhisk/cli) e siga as instruções para instalá-la.

## Visão geral
{: #openwhisk_start_overview}
- [Como funciona o OpenWhisk](./openwhisk_about.html)
- [Casos de uso comuns para aplicativos Serverless](./openwhisk_use_cases.html)
- [Configurando e usando a CLI do OpenWhisk](./openwhisk_cli.html)
- [Usando o OpenWhisk por meio de um app iOS](./openwhisk_mobile_sdk.html)
- [Artigos, amostras e
tutoriais](https://github.com/openwhisk/openwhisk-external-resources)
- [FAQ do Apache OpenWhisk](http://openwhisk.org/faq)
- [Venda](https://console.ng.bluemix.net/openwhisk/learn/pricing)

## Gabarito de Programação
{: #openwhisk_start_programming}
- [Detalhes do Sistema](./openwhisk_reference.html)
- [Catálogo de serviços fornecidos pelo OpenWhisk](./openwhisk_catalog.html)
- [Ações](./openwhisk_actions.html)
- [Acionadores e regras](./openwhisk_triggers_rules.html)
- [Feeds](./openwhisk_feeds.html)
- [Pacotes](./openwhisk_packages.html)
- [Anotações](./openwhisk_annotations.html)
- [Ações da web](./openwhisk_webactions.html)
- [Gateway de API](./openwhisk_apigateway.html)
- [Nomes de entidades](./openwhisk_reference.html#openwhisk_entities)
- [Semântica de ação](./openwhisk_reference.html#openwhisk_semantics)
- [Limites
](./openwhisk_reference.html#openwhisk_syslimits)

## Exemplo Hello World do {{site.data.keyword.openwhisk_short}}
{: #openwhisk_start_hello_world}
Para iniciar o uso do {{site.data.keyword.openwhisk_short}}, tente o exemplo de código JavaScript a seguir.

```javascript
/**
 * Hello world como uma ação OpenWhisk.
 */
function main(params) {
    var name = params.name || 'World';
    return {payload:  'Hello, ' + name + '!'};
}
```
{: codeblock}

Para usar esse exemplo, siga estas etapas:

1. Salve o código em um arquivo. Por exemplo, *hello.js*.

2. Na linha de comandos da CLI do {{site.data.keyword.openwhisk_short}}, crie a ação inserindo este comando:

    ```
    wsk action create hello hello.js
    ```
    {: pre}

3. Em seguida, chame a ação inserindo os comandos a seguir.

    ```
    wsk action invoke hello --blocking --result
    ```
    {: pre}  

    Estas
saídas de comando:

    ```json
     {
        "payload": "Hello, World!"
    }
    ```
    
    ```
    wsk action invoke hello --blocking --result --param name Fred
    ```
    {: pre}  

    Estas
saídas de comando:

    ```json
     {
        "payload": "Hello, Fred!"
    }
    ```

Também é possível usar os recursos acionados por eventos no {{site.data.keyword.openwhisk_short}} para chamar essa ação em resposta a eventos. Siga o [exemplo de serviço de alarme](./openwhisk_packages.html#openwhisk_packages_trigger) para configurar uma origem de eventos para chamar a ação `hello` toda vez que um evento periódico for gerado.

Uma lista completa de
[Tutoriais
e Amostras do OpenWhisk pode ser localizada aqui](https://github.com/openwhisk/openwhisk-external-resources#sample-applications). Além das amostras, esse repositório contém links para
artigos, apresentações, podcasts, vídeos e outros recursos relacionados
ao {{site.data.keyword.openwhisk_short}}.

## Referência de API
{: #openwhisk_start_api notoc}
* [Documentação da API REST](./openwhisk_reference.html#openwhisk_ref_restapi)
* [REST API
](https://console.{DomainName}/apidocs/98)

## Links Relacionados
{: #general notoc}
* [Descobrir: {{site.data.keyword.openwhisk_short}}](http://www.ibm.com/cloud-computing/bluemix/openwhisk/)
* [{{site.data.keyword.openwhisk_short}} no IBM developerWorks](https://developer.ibm.com/openwhisk/)
* [Website do projeto Apache {{site.data.keyword.openwhisk_short}}](http://openwhisk.org)
