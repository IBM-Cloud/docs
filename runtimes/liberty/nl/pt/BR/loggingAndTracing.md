---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Criação de Log e Rastreio
{: #logging_tracing}

## Arquivos de log
{: #log_files}

Os logs padrão do Liberty, como `messages.log` ou o diretório `ffdc`, estão disponíveis no IBM Bluemix no diretório `logs` de cada instância do aplicativo. Esses logs podem ser acessados por meio do console do IBM Bluemix ou usando o CF CLI. Por exemplo:

* Para acessar os logs recentes de um app, execute o comando a seguir:

  ```
  $ cf logs --recent <appname>
  ```
  {: codeblock}

* Para ver o arquivo `messages.log` de um app em execução em um nó DEA, execute o comando a seguir:

  ```
  $ cf files <appname> logs/messages.log
  ```
  {: codeblock}

* Para ver o arquivo `messages.log` de um app em execução em uma célula do Diego, execute o comando a seguir:

  ```
  $ cf ssh <appname> -c "cat logs/messages.log"
  ```
  {: codeblock}

O nível de
log e outras opções de rastreio podem ser configurados por meio do arquivo de configuração do Liberty. Para obter mais informações, consulte [Perfil do Liberty: rastreio e criação de log](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html). O rastreio também pode ser ajustado em uma instância do aplicativo em execução usando o console do IBM Bluemix.

## Usando os recursos de rastreio e de dump
{: #using_trace_and_dump}

A configuração de rastreio do Liberty pode ser ajustada para um aplicativo em execução diretamente do console do IBM Bluemix. O console também fornece capacidade para solicitar e fazer download de dumps de encadeamento e de heap. Para ajustar a configuração de rastreio ou solicitar um dump, selecione um aplicativo Liberty no console do Bluemix e escolha o menu `Tempo de execução` na navegação. Na visualização `Tempo de execução`, selecione uma instância e pressione o botão *RASTREIO* ou *DUMP*. Se estiver ajustando o nível de rastreio, veja [Perfil do Liberty: rastreio e criação de log](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html) para obter os detalhes da sintaxe da especificação de rastreio.

### Diego: acionando dumps por meio de SSH

Para um aplicativo em execução em uma célula do Diego, também é possível acionar um dump de encadeamento e de heap por meio do CF CLI usando o recurso SSH. Por exemplo:

```
$ cf ssh <appname> -c "pkill -3 java"
```
{: codeblock}

Veja a documentação abaixo para obter detalhes sobre o download dos arquivos de dump gerados.

## Fazer download de arquivos de dump
{: #download_dumps}

Por padrão, os vários arquivos de dump são colocados no diretório `dumps` do contêiner de aplicativo.

### Aplicativo DEA

Para um aplicativo em execução em um nó DEA, use a funcionalidade "cf files" para visualizar e fazer download dos arquivos de dump.

* Para ver os dumps gerados, execute o comando a seguir:

  ```
  $ cf files <appname> dumps
  ```
  {: codeblock}

* Para fazer download de um arquivo de dump, execute os comandos a seguir:

    1. Obter o GUID do aplicativo

      ```
      $ cf app <appname> --guid
      ```
      {: codeblock}

    2. Fazer download do arquivo de dump

      ```
      $ cf curl /v2/apps/<app_guid>/instances/<instance_id>/files/dumps/<dump_file_name> --output <local_dump_file_name>
      ```
      {: codeblock}

### Aplicativo Diego

Para um aplicativo em execução em uma célula do Diego, use a funcionalidade "cf ssh" para visualizar e fazer download dos arquivos de dump.

* Para ver os dumps gerados, execute o comando a seguir:

  ```
  $ cf ssh <appname> -c "ls -l dumps"
  ```
  {: codeblock}

* Para fazer download de um arquivo de dump, execute o comando a seguir:

  ```
  $ cf ssh <appname> -i <instance_id> -c "cat dumps/<dump_file_name>" > <local_dump_file_name>
  ```
  {: codeblock}

Também é possível usar `scp` e outras ferramentas semelhantes para visualizar e fazer download dos arquivos de dump. Consulte [Acessando apps com SSH ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.cloudfoundry.org/devguide/deploy-apps/ssh-apps.html) para obter mais informações.

# rellinks
{: #rellinks notoc}
## geral
{: #general notoc}
* [Tempo de execução do Liberty](index.html)
* [Visão geral do perfil Liberty](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
