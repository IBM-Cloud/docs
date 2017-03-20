---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Criação de log de aplicativo de tempo de execução por meio de apps CF
{: #logging_writing_to_log_from_cf_app}

No {{site.data.keyword.Bluemix}}, para persistir dados do log para um app Cloud Foundry e seu tempo de execução, deve-se gravar seus logs para STDOUT e STDERR.
{:shortdesc}

No {{site.data.keyword.Bluemix}}, os registros de log STDOUT e STDERR são coletados automaticamente:

* O STDOUT (saída padrão) fornece informações gerais.  
* O STDERR (erro padrão) fornece informações que incluem mensagens de erro e outros avisos de diagnóstico. 

O Loggregator seleciona automaticamente os dados de saída padrão e erro padrão. O Loggregator é o componente que encaminha os logs de dentro do Cloud Foundry. 

Por exemplo, 

Para um **app Liberty Cloud Foundry**, o console.log padrão para o servidor Liberty é selecionado automaticamente pelo loggregator. 

* O console.log contém o STDOUT e o STDERR redirecionados do processo da JVM. A saída de console conterá os principais eventos e erros se você usar a configuração consoleLogLevel padrão. A saída de console também conterá quaisquer mensagens que forem gravadas nos fluxos system.out e system.err se você usar a configuração copySystemStreams padrão. A saída de console sempre contém mensagens que são gravadas diretamente pelo processo da JVM, como saída -verbose:gc. É possível ajustar o nível de criação de log do Liberty por meio do server.xml.
* O consoleLogLevel configura o nível de filtro do manipulador console.log. Ao configurar o consoleLogLevel como INFO, você configura todas as mensagens INFO, AUDIT, WARNING e ERROR para serem gravadas no arquivo console.log. **Nota:** as entradas de log FINE, FINER, FINEST são gravadas somente no arquivo trace.log.

Para obter mais informações sobre os aplicativos Liberty for Java™, veja [Perfil Liberty: criação de log e rastreio](http://www-01.ibm.com/support/knowledgecenter/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/rwlp_logging.html).

Para um **app Node.js Cloud Foundry**, é possível usar o módulo de criação de log do console integrado para configurar a criação de log para o tempo de execução no {{site.data.keyword.Bluemix}}. É possível colocar mensagens no stdout e stderr:

* O console.log('message') enviará a mensagem para o fluxo STDOUT
* O console.error('error_message') enviará o erro para o fluxo STDERR

Para obter mais informações sobre os aplicativos Node.js, veja [Como efetuar login no node.js](http://docs.nodejitsu.com/articles/intermediate/how-to-log).


Para obter mais informações sobre **aplicativos Ruby on Rails**, veja [O criador de logs](http://guides.rubyonrails.org/debugging_rails_applications.html#the-logger).

A tabela a seguir lista o mapeamento entre alguns logs de tempos de execução de aplicativo e os logs que são selecionados automaticamente pelo Loggregator:

| **Tempo de execução** |    **STDOUT**     | **STDERR** |
|-----------------|-------------------|-------------------|
| Liberty | system.out | system.err |
| Node.js | console.log, console.info | console.error, console.warn |
| Ruby | stdout| stderr |
{: caption="Table 1. Mapping between some application runtimes logs and the logs that are picked automatically by Loggregator" caption-side="top"}

