---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-09"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Criação de Log e Rastreio
{: #logging_tracing}

## Arquivos de log
{: #log_files}

Os logs padrão do Liberty, tais como messages.log ou o diretório ffdc, estão disponíveis no IBM Bluemix no diretório de logs de cada instância do aplicativo. Esses logs podem ser acessados a partir do console do IBM Bluemix ou usando os comandos cf logs e cf files.
Por exemplo, para ver o arquivo messages.log, execute o comando:
```
    $ cf files <yourappname> logs/messages.log
```
{: codeblock}

O nível de
log e outras opções de rastreio podem ser configurados por meio do arquivo de configuração do Liberty. Para obter mais informações, consulte [Perfil do Liberty: rastreio e criação de log](http://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/rwlp_logging.html?cp=SSAW57_8.5.5%2F3-17-0-0). O rastreio também pode ser ajustado em uma instância do aplicativo em execução usando o console do IBM Bluemix.

## Usando os recursos de rastreio e de dump
{: #using_trace_and_dump}

Na interface com o usuário do IBM Bluemix, existem recursos de rastreio e de dump.
* Use o Rastreio para visualizar e atualizar o traceSpecification de criação de log do Liberty em instâncias do aplicativo em execução.
* Use o Dump para criar dumps de encadeamento e de heap em instâncias do aplicativo em execução.

Para executar essa ação, selecione um aplicativo Liberty na interface com o usuário. Na categoria Tempo de execução na navegação, é possível abrir os detalhes da instância. Selecione uma instância ou diversas instâncias. No menu Ações, é possível escolher TRACE ou DUMP.

## Download de arquivos de dump
{: #download_dumps}

<strong>Pré-requisito:  </strong>
* [Instalar CLI do CF](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html)
* [Instale o plug-in Diego
Enabler](https://github.com/cloudfoundry-incubator/Diego-Enabler) se seu aplicativo for executado no Diego

<strong>Se seu aplicativo for executado no DEA, use as seguintes etapas:</strong>
  
1. get app_guid
```
$ cf app <app_name> --guid
```

2. Download do arquivo de dump
```
$ cf curl /v2/apps/<app_guid>/instances/<instance_id>/files/dumps/<dump_file_name> --output <local_dump_file_name>
```

<strong>Se seu aplicativo for executado no Diego, use as seguintes etapas:</strong>
  
1. get app_guid
```
$ cf app <app_name> --guid
```

2. get app_ssh_endpoint(host and port) and app_ssh_host_key_fingerprint
```
$ cf curl /v2/info
```

3. get ssh-code for scp command
```
$ cf ssh-code
```

4. arquivo de dump remoto scp para local, use código ssh quando uma senha for solicitada
```
$ scp -P <app_ssh_endpoint_port> -o User=cf:<app_guid>/<instance_id> <app_ssh_endpoint_host>:/home/vcap/dumps/<dump_file_name> <local_dump_file_name>
```

Consulte [Acessando
aplicativos com SSH](https://docs.cloudfoundry.org/devguide/deploy-apps/ssh-apps.html) para obter mais detalhes


# rellinks
{: #rellinks}
## geral
{: #general}
* [Tempo de execução do Liberty](index.html)
* [Visão geral do perfil do Liberty](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)

