---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# CLI do {{site.data.keyword.openwhisk_short}}

O {{site.data.keyword.openwhisk_short}} oferece uma interface da linha de comandos poderosa que permite o gerenciamento completo de todos os aspectos do sistema.

## Configurando a CLI do {{site.data.keyword.openwhisk_short}} 

É possível usar a interface da linha de comandos (CLI) do {{site.data.keyword.openwhisk_short}} para configurar o namespace e a chave de autorização.
Acesse [Configurar CLI](https://new-console.{DomainName}/openwhisk/cli){: new_window} e siga as instruções para instalá-la.

Há duas propriedades necessárias a serem configuradas para usar a CLI:

1. **Host da API** (nome ou endereço IP) para a implementação do {{site.data.keyword.openwhisk_short}} que você deseja usar.
2. **Chave de autorização** (nome do usuário e senha) que concede acesso à API do {{site.data.keyword.openwhisk_short}}.

Execute o comando a seguir para configurar o host da API:

```
wsk property set --apihost openwhisk.ng.bluemix.net
```
{: pre} 

Se você souber sua chave de autorização, será possível configurar a CLI para usá-la. 

Execute o comando a seguir para configurar a Chave de autorização:

```
wsk property set --auth <authorization_key>
```
{: pre}

**Dica:** a CLI do OpenWhisk armazena as propriedades configuradas em `~/.wskprops`, por padrão. O local desse arquivo pode ser alterado configurando a variável de ambiente `WSK_CONFIG_FILE`. 

Para verificar a configuração da CLI, tente [criar e executar uma ação](./index.html#openwhisk_start_hello_world).

## Usando o CLI do {{site.data.keyword.openwhisk_short}}

Após ter configurado seu ambiente, será possível iniciar o uso da CLI do {{site.data.keyword.openwhisk_short}} para executar o seguinte:

* Executar os fragmentos de código ou ações no {{site.data.keyword.openwhisk_short}}. Consulte [Criando e chamando ações](./openwhisk_actions.html).
* Usar acionadores e regras para ativar suas ações para responder a eventos. Consulte [Criando acionadores e regras](./openwhisk_triggers_rules.html).
* Aprender como pacotes empacotam ações e configuram origens de eventos externos. Consulte [Usando e criando pacotes](./openwhisk_packages.html).
* Explorar o catálogo de pacotes e aprimorar seus aplicativos com serviços externos, como uma [Origem de eventos do Cloudant](./openwhisk_cloudant.html). Veja [Usando serviços ativados pelo OpenWhisk](./openwhisk_catalog.html).

## Configure a CLI para usar um proxy HTTPS

A CLI pode ser configurada para usar um proxy HTTPS. Para configurar um proxy HTTPS, uma variável de ambiente chamada `HTTPS_PROXY` deve ser criada.  A variável deve ser configurada para o endereço do proxy HTTPS e a sua porta usando o formato a seguir:
`{PROXY IP}:{PROXY PORT}`.
