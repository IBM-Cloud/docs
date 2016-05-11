---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Criação de Log e Rastreio
{: #logging_tracing}

*Última atualização: 23 de março de 2016*

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
* Use o Dump para criar e manipular dumps de encadeamento e de heap em instâncias do aplicativo em execução.

Para executar essa ação, selecione um aplicativo Liberty na interface com o usuário. Em Tempo de execução na navegação à esquerda, é possível abrir os detalhes da instância. Selecione uma instância ou diversas instâncias. No menu Ações, é possível escolher TRACE ou DUMP.

# rellinks
## geral
* [Tempo de execução do Liberty](index.html)
* [Visão geral do perfil do Liberty](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
