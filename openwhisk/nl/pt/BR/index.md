---

copyright:
  years: 2016, 2017
lastupdated: "2016-09-09"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Introdução ao {{site.data.keyword.openwhisk_short}}


O {{site.data.keyword.openwhisk}} é um serviço de cálculo distribuído, orientado para eventos também referido como Cálculo sem servidor ou como Função como um serviço (FaaS), o
{{site.data.keyword.openwhisk_short}} executa uma lógica de aplicativo em resposta a eventos ou chamadas diretas a partir de aplicativos da web ou móveis sobre HTTP. Os eventos
podem ser fornecidos a partir de serviços do Bluemix, como o Cloudant e a partir de
fontes externas. Os desenvolvedores podem focar a composição da lógica do aplicativo e a criação de ações que são executadas sob demanda. A
taxa de execução de ações sempre corresponde à taxa de eventos, resultando em ajuste de
escala e resiliência inerentes, além de utilização ideal. Você paga somente o que você usar e não precisa gerenciar um servidor. Também é possível obter o [código-fonte](https://github.com/openwhisk/openwhisk) e você mesmo executar o sistema.
{: shortdesc}

Para obter mais detalhes sobre como o {{site.data.keyword.openwhisk_short}} funciona, consulte [Sobre o {{site.data.keyword.openwhisk_short}}](./openwhisk_about.html).

É possível usar o Navegador ou a CLI para desenvolver os seus aplicativos {{site.data.keyword.openwhisk_short}}.
Ambos têm recursos semelhantes para desenvolver aplicativos; a CLI fornece mais controle sobre a sua implementação e as operações.


## Desenvolver em seu navegador
{: #openwhisk_start_editor}

Teste o {{site.data.keyword.openwhisk_short}} e seu [Navegador](https://console.{DomainName}/openwhisk/editor){: new_window} para
criar ações, automatizar ações usando acionadores e explorar pacotes públicos. 
Visite a página [saiba mais](https://console.{DomainName}/openwhisk/learn){: new_window} para um tour rápido da Interface com o Usuário do OpenWhisk.

## Configurando a CLI do {{site.data.keyword.openwhisk_short}}
{: #openwhisk_start_configure_cli}

É possível usar a interface da linha de comandos (CLI) do {{site.data.keyword.openwhisk_short}} para configurar o namespace e a chave de autorização.
Acesse [Configurar CLI](https://new-console.{DomainName}/openwhisk/cli){: new_window} e siga as instruções para instalá-la.

### Configure a CLI para usar um proxy HTTPS
{: #openwhisk_configure_https_proxy_cli}

A CLI pode ser configurada para usar um proxy HTTPS. Para configurar um proxy HTTPS, uma variável de ambiente chamada `HTTPS_PROXY` deve
 ser criada. A variável deve ser configurada para o endereço do proxy HTTPS e a sua porta usando o formato a seguir:
`{PROXY IP}:{PROXY PORT}`.

Após o {{site.data.keyword.openwhisk_short}} ser configurado com a CLI,
será possível iniciá-lo a partir da linha de comandos.

## Usando o CLI do {{site.data.keyword.openwhisk_short}}
{: #openwhisk_start_using_cli}

Depois de ter [configurado seu ambiente](https://new-console.{DomainName}/openwhisk/cli){: new_window}, é possível começar a usar a CLI do {{site.data.keyword.openwhisk_short}} para executar o seguinte:

* Executar os fragmentos de código ou ações no {{site.data.keyword.openwhisk_short}}. Consulte [Criando e chamando ações](./openwhisk_actions.html).
* Usar acionadores e regras para ativar suas ações para responder a eventos. Consulte [Criando acionadores e regras](./openwhisk_triggers_rules.html).
* Aprender como pacotes empacotam ações e configuram origens de eventos externos. Consulte [Usando e criando pacotes](./openwhisk_packages.html).
* Explorar o catálogo de pacotes e aprimorar seus aplicativos com serviços externos, como uma [Origem de eventos do Cloudant](./openwhisk_catalog.html#openwhisk_catalog_cloudant). Consulte [Usando serviços ativados pelo {{site.data.keyword.openwhisk_short}}](./openwhisk_catalog.html).


## Usando o {{site.data.keyword.openwhisk_short}} a partir de um app do iOS
{: #openwhisk_start_using_ios}

É possível usar o {{site.data.keyword.openwhisk_short}} a partir de seu app móvel do iOS ou do Apple Watch usando o SDK do iOS do {{site.data.keyword.openwhisk_short}}. Para obter mais detalhes, consulte a [documentação do iOS](./openwhisk_mobile_sdk.html).

## Usando APIs REST com o {{site.data.keyword.openwhisk_short}}
{: #openwhisk_start_using_restapi}

Após seu ambiente do {{site.data.keyword.openwhisk_short}} ser ativado, é possível usar o {{site.data.keyword.openwhisk_short}} com seus apps da web ou apps móveis com chamadas API REST.
Para obter mais detalhes sobre as APIs para ações, ativações, pacotes, regras e
acionadores, consulte a
[documentação
da API do {{site.data.keyword.openwhisk_short}}](https://new-console.{DomainName}/apidocs/98).

## Exemplo Hello World do {{site.data.keyword.openwhisk_short}}
{: #openwhisk_start_hello_world}
Para iniciar o uso do {{site.data.keyword.openwhisk_short}}, tente o exemplo de código JavaScript a seguir.

```
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

    ```
    {
        "payload": "Hello, World!"
    }
    ```
    {: screen}

    ```
    wsk action invoke hello --blocking --result --param name Fred
    ```
    {: pre}  

    Estas
saídas de comando:

    ```
    {
        "payload": "Hello, Fred!"
    }
    ```
    {: screen}

Também é possível usar os recursos acionados por eventos no {{site.data.keyword.openwhisk_short}} para chamar essa ação em resposta a eventos. Siga o [exemplo de serviço de alarme](./openwhisk_packages.html#openwhisk_packages_trigger) para configurar uma origem de eventos para chamar a ação `hello` toda vez que um evento periódico for gerado.


## Detalhes do Sistema
{: #openwhisk_system_details}

É possível localizar informações adicionais sobre o {{site.data.keyword.openwhisk_short}} nos tópicos a seguir:

* [Nomes de entidades](./openwhisk_reference.html#openwhisk_entities)
* [Semântica de ação](./openwhisk_reference.html#openwhisk_semantics)
* [Limites
](./openwhisk_reference.html#openwhisk_syslimits)
* [REST API
](https://new-console.{DomainName}/apidocs/98)

# Links Relacionados
{: #rellinks notoc}

## Referência de API
{: #api}
* [Documentação da API REST](./openwhisk_reference.html#openwhisk_ref_restapi)
* [API REST](https://new-console.{DomainName}/apidocs/98){:new_window}

## Links Relacionados
{: #general}
* [Descobrir: {{site.data.keyword.openwhisk_short}}](http://www.ibm.com/cloud-computing/bluemix/openwhisk/){:new_window}
* [{{site.data.keyword.openwhisk_short}} no IBM developerWorks](https://developer.ibm.com/openwhisk/){:new_window}
