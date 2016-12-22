---

copyright:
  years: 2015, 2016
lastupdated: "2016-12-01"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Gerenciando apps Liberty e Node.js
{: #app_management}


App Management é um conjunto de utilitários de desenvolvimento e depuração que podem ser ativados para
seus aplicativos Liberty e Node.js no {{site.data.keyword.Bluemix}}.
{:shortdesc}

## Utilitários do App Management
{: #Utilities}

### Esses utilitários suportam Liberty e Node.js
{: #liberty_and_node_utilities}

#### proxy
{: #proxy}

O *proxy* fornece gerenciamento de aplicativo mínimo entre o seu aplicativo e o {{site.data.keyword.Bluemix_notm}}.

Quando ativado, o buildpack inicia um agente de proxy que está localizado entre o tempo de execução e o contêiner do aplicativo. O utilitário *proxy* manipula todas as solicitações recebidas pelo aplicativo. Com base no tipo de solicitação, ele executa uma ação do App Management ou encaminha a solicitação para seu aplicativo. *proxy* permite a ativação da maioria dos outros utilitários do App Management. Ao ativar o *proxy*, o contêiner de seu aplicativo continuará ativo mesmo se o aplicativo travar. O agente de proxy também permite atualizações incrementais de arquivos, que ativa o modo "Live Edit" para aplicativos Node.js.

#### devconsole
{: #devconsole}

O utilitário do console de desenvolvimento (*devconsole*) está acessível na URL a seguir:
```
  http://<yourappname>.mybluemix.net/bluemix-debug/manage
```

Usando o console de desenvolvimento, os usuários podem reiniciar, parar ou suspender seus aplicativos. Os usuários também podem ativar ou acessar os utilitários shell e inspetor.

Para o Node versão 6.3.0 ou superior o console de desenvolvimento fornece um botão de reinício para o seu aplicativo e acesso ao utilitário shell.  Consulte a
discussão do *inspetor* para obter mais informações.

O utilitário devconsole também inicia o *proxy*.

#### hc
{: #hc}

O agente do Health Center (*hc*) permite que o seu aplicativo seja monitorado pelo cliente do Health Center.

O Health Center suporta a análise do desempenho dos aplicativos Liberty e Node.js usando o IBM Monitoring and Diagnostic Tools. Para obter mais informações, consulte [Como analisar o desempenho de apps Liberty Java ou Node.js no {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/2015/07/03/how-to-analyze-performance-in-bluemix/){:new_window}.</p></li>

#### shell
{: #shell}

O utilitário *shell* ativa o shell baseado na web. Ele é acessível a partir do utilitário *devconsole* ou acessando a URL a
seguir:

```
  http://<yourappname>.mybluemix.net/bluemix-debug/shell
```

Uma janela do terminal é exibida com acesso de shell em seu aplicativo após você acessar o utilitário *shell*. É possível fazer tudo o que for suportado em um shell regular, como editar arquivos, verificar o uso de memória ou executar comandos de diagnóstico.

O utilitário *shell* também inicia o *proxy*.

### Esses utilitários suportam apenas o Liberty
{: #liberty_utilities}

#### depuração
{: #debug}

O utilitário *depuração* coloca o aplicativo Liberty no modo de depuração e permite que clientes como o IBM Eclipse Tools for
{{site.data.keyword.Bluemix_notm}} estabeleçam uma sessão de depuração remota com o aplicativo.

Para obter mais informações, consulte [Depuração remota](/docs/manageapps/eclipsetools/eclipsetools.html#remotedebug).

O utilitário *debug* também inicia o *proxy*.

#### jmx
{: #jmx}

O utilitário *jmx* ativa o Conector de REST do JMX para permitir que um cliente JMX remoto gerencie o aplicativo usando credenciais do
usuário do {{site.data.keyword.Bluemix_notm}}.

Para obter mais informações sobre como configurar um conector JMX, consulte [Configurando uma conexão JMX segura com o perfil Liberty.](https://www-01.ibm.com/support/knowledgecenter/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/twlp_admin_restconnector.html){:new_window}.

O utilitário *jmx* não inicia o proxy.

### Esses utilitários suportam apenas o Node.js
{: #node_utilities}

#### inspetor
{: #inspector}

Para as versões do Node.js anteriores à 6.3.0, o *inspetor* ativa a interface com o depurador do inspetor do nó que está acessível a partir do
utilitário *devconsole* ou em *https://myApp.mybluemix.net/bluemix-debug/inspector.*

O processo do *inspetor* é executado em seu contêiner de aplicativo. Use esse utilitário para criar perfis de uso da CPU, incluir pontos de interrupção e depurar código, tudo enquanto seu aplicativo estiver em execução no {{site.data.keyword.Bluemix_notm}}. Para obter mais informações sobre o módulo do inspetor do nó, consulte [node-inspector no GitHub](https://github.com/node-inspector/node-inspector){:new_window}.

O utilitário *inspector* também inicia o *proxy*.

Para as versões do Node.js 6.3.0 e superiores, o *inspetor* utiliza a
[V8 Inspector Integration for
Node.js](https://nodejs.org/dist/latest-v6.x/docs/api/debugger.html#debugger_v8_inspector_integration_for_node_js){:new_window}. Em logs de seu app você encontrará uma URL que pode ser usada para conectar suas DevTools do Chrome em seu app. As mensagens de log
serão semelhantes à seguinte:

```
  2016-11-30T16:40:56.03-0500 [APP/0]      OUT Starting app with 'node-hc --inspect=9229  app.js '
  2016-11-30T16:40:56.17-0500 [APP/0]      ERR Debugger listening on port 9229.
  2016-11-30T16:40:56.17-0500 [APP/0]      ERR To start debugging, open the following URL in Chrome:
  2016-11-30T16:40:56.17-0500 [APP/0]      ERR     chrome-devtools://devtools/remote/serve_file...
```

O *devconsole* **não** mostrará um link para o *inspetor* neste cenário, pois a URL não existe.

O *proxy* não roteará o tráfego para o *inspetor* neste cenário. Será necessário criar um túnel de SSH para o seu app para que a URL
de DevTools do Chrome funcione. Para criar o túnel de SSH, use o comando 'cf ssh' de uma maneira semelhante à seguinte:

```
  cf ssh -N -T -L <port>:127.0.0.1:<hostport> <appName>
```

Nesse comando *hostport* deve ser o valor de porta da mensagem de log "Depurador em escuta na porta xxxx" e *port* é
qualquer porta disponível no sistema da qual o comando "cf ssh" é emitido.

#### rastreamento
{: #trace}

O utilitário de *rastreio* permite que você configure dinamicamente os níveis de rastreio se o seu aplicativo estiver usando os módulos de criação
de log *log4js*, *ibmbluemix* ou *bunyan*.

**Nota**: versões de dependência suportadas:
* log4js:(0.6.0 - 0.6.24)
* bunyan: (1.0.0, 1.0.1, 1.1.0 - 1.1.3, 1.2.0 - 1.2.3, 1.3.0 - 1.3.5)
* ibmbluemix: (1.0.0-20140707-1250)-(1.0.0-20150409-1328)

Acesse a página Detalhes da instância no console da web do {{site.data.keyword.Bluemix_notm}} e selecione **Ações** para ver a interface com o usuário.

O utilitário *trace* não está disponível quando o aplicativo foi iniciado usando a opção "-b buildpack".

O utilitário *trace* não inicia o *proxy*.

##  Como configurar o App Management
{: #configure}

Para ativar os utilitários do App Management, configure a variável de ambiente *BLUEMIX_APP_MGMT_ENABLE*
e remonte seu aplicativo. É possível ativar diversos utilitários separando-os com um “+”.

Por exemplo, para ativar os utilitários *devconsole* e *shell*, execute o comando a seguir:

```
cf set-env myApp BLUEMIX_APP_MGMT_ENABLE devconsole+shell
```

Remonte o seu aplicativo após você configurar a variável de ambiente:

```
cf restage myApp
```

Se não deseja que os utilitários do App Management sejam instalados com seu aplicativo, configure
a variável de ambiente *BLUEMIX_APP_MGMT_INSTALL* para 'false' e remonte seu aplicativo.

Por
exemplo:

```
cf set-env myApp BLUEMIX_APP_MGMT_INSTALL false
cf restage myApp
```

## Restrições
{: #restrictions}

* O App Management suporta apenas aplicativos de instância única.
* Mudanças feitas no aplicativo usando o App Management são temporárias e serão perdidas após a saída desse modo. Este modo destina-se somente ao uso de
desenvolvimento provisório e não deve ser usado como um ambiente de produção
devido ao desempenho.
* A maioria dos utilitários do App Management não funcionará se você configurar seu comando inicial no arquivo manifest.yml (comando) ou CF CLI (-c). Esses métodos são substituições de buildpack e são antipadrões para iniciar aplicativos Node.js. Para obter melhores resultados, configure o comando inicial no arquivo package.json ou Procfile.

## Modo de desenvolvimento para Eclipse Tools
{: #devmode}

Modo de desenvolvimento é um recurso do [Eclipse Tools for {{site.data.keyword.Bluemix_notm}}](/docs/manageapps/eclipsetools/eclipsetools.html#eclipsetools) que fornece aos desenvolvedores a capacidade de trabalhar com seus aplicativos enquanto eles estão em execução na nuvem.

Ao trabalhar com seus aplicativos no {{site.data.keyword.Bluemix_notm}}, os desenvolvedores podem achar que não podem
executar atividades normais de desenvolvimento como eles o fazem em um ambiente local. Para resolver esse problema,
o modo de desenvolvimento fornece, por meio do Eclipse Tools, uma maneira para você trabalhar na nuvem enquanto está em uma
área de trabalho segura provisória.

O modo de desenvolvimento é suportado para aplicativos Liberty e Node.js. Com o modo de desenvolvimento
ativado para seu aplicativo Liberty ou Node.js, é possível atualizar arquivos de aplicativos incrementalmente
sem precisar que enviar seu aplicativo por push. É possível também estabelecer uma sessão de depuração com seu
aplicativo. O modo de desenvolvimento para aplicativos Liberty é equivalente e ativar os utilitários
debug e jmx do App Management. Para aplicativos Node.js, é equivalente a ativar os utilitários *devconsole*, *inspector* e *shell*.
