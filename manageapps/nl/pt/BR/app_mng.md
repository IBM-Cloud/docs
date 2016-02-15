{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#App Management
{: #app_management}

*Última atualização: 8 de dezembro de 2015*

App Management é um conjunto de utilitários de desenvolvimento e depuração que podem ser ativados para
seus aplicativos Liberty e Node.js no {{site.data.keyword.Bluemix}}.
{:shortdesc}

##Utilitários do App Management
{: #Utilities}

Esses utilitários suportam Liberty e Node.js.

  1. *proxy*: gerenciamento mínimo do aplicativo que serve como um proxy entre seu aplicativo e o {{site.data.keyword.Bluemix_notm}}.

    Quando ativado, o buildpack inicia um agente de proxy que está localizado entre o tempo de execução e o contêiner do aplicativo. O utilitário *proxy* manipula todas as solicitações recebidas pelo aplicativo. Com base no tipo de solicitação, ele executa uma ação do App Management ou encaminha a solicitação para seu aplicativo. *proxy* permite a ativação da maioria dos outros utilitários do App Management. Ao ativar o *proxy*, o contêiner de seu aplicativo continuará ativo mesmo se o aplicativo travar. O agente de proxy também permite atualizações incrementais de arquivos, que ativa o modo "Live Edit" para aplicativos Node.js.
	
  2. *devconsole*: ativa o utilitário do console de desenvolvimento que está acessível na URL a seguir:
    ```
    http://<yourappname>.mybluemix.net/bluemix-debug/manage
    ```
	
    Usando o console de desenvolvimento, os usuários podem reiniciar, parar ou suspender seus aplicativos. Os usuários também podem ativar ou acessar os utilitários shell e inspetor.

    O utilitário devconsole também inicia o *proxy*.
	
  3. *hc*: agente do Health Center que permite que seu aplicativo seja monitorado pelo cliente Health Center.

    O Health Center suporta a análise do desempenho dos aplicativos Liberty e Node.js usando o IBM Monitoring and Diagnostic Tools. Para obter mais informações, consulte [Como analisar o desempenho de apps Liberty Java ou Node.js no {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/2015/07/03/how-to-analyze-performance-in-bluemix/){:new_window}.</p></li>
	
  4. *shell*: ativa um shell baseado na web que é acessível a partir do utilitário devconsole ou acessando a URL a seguir:
    ```
    http://<yourappname>.mybluemix.net/bluemix-debug/shell
    ```
	
    Uma janela do terminal é exibida com acesso de shell em seu aplicativo após o acesso ao utilitário shell. É possível fazer tudo o que for suportado em um shell regular, como editar arquivos, verificar o uso de memória ou executar comandos de diagnóstico.
	
    O utilitário *shell* também inicia o *proxy*.

Esses utilitários suportam apenas o Liberty.

  1. *debug*: alterna o aplicativo Liberty para o modo de depuração e permite que clientes, como o IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}, estabeleça uma sessão de depuração remota com o aplicativo.
  
   Para obter mais informações, consulte [Depuração remota](../manageapps/eclipsetools/eclipsetools.html#remotedebug).
   
   O utilitário *debug* também inicia o *proxy*.
   
  2. *jmx*: ativa o Conector JMX REST para permitir que um cliente JMX remoto gerencie o aplicativo usando credenciais do usuário do {{site.data.keyword.Bluemix_notm}}.
  
  Para obter mais informações sobre como configurar um conector JMX, consulte [Configurando uma conexão JMX segura com o perfil Liberty.](https://www-01.ibm.com/support/knowledgecenter/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/twlp_admin_restconnector.html){:new_window}.
  
  O utilitário *jmx* não inicia o proxy.

Esses utilitários suportam apenas o Node.js.

  1. *inspector*: ativa a interface com o depurador do inspetor do nó que está acessível a partir do utilitário *devconsole* ou em *https://myApp.mybluemix.net/bluemix-debug/inspector.*
  
  O processo do inspector é executado no contêiner do aplicativo. Use esse utilitário para criar perfis de uso da CPU, incluir pontos de interrupção e depurar código, tudo enquanto seu aplicativo estiver em execução no {{site.data.keyword.Bluemix_notm}}. Para obter mais informações sobre o módulo do inspetor do nó, consulte [node-inspector no GitHub](https://github.com/node-inspector/node-inspector){:new_window}.
  
  O utilitário *inspector* também inicia o *proxy*.
  
  2. *strongpm*: ativa o uso de [StrongLoop Arc](https://strongloop.com/node-js/arc){:new_window} para analisar o aplicativo Node.js com utilitários como: [StrongLoop Metrics, Profiling e Tracing](https://strongloop.com/node-js/devops-tools/){:new_window}.
  
  **NOTA:** deve-se usar uma versão 0.12 de engines.node para usar o utilitário **strongpm**. A versão engines.node é especificada no arquivo package.json. Por
exemplo:
  
  ```
  "engines":{"node":"0.12"}
  ```
    
  O utilitário *strongpm* também inicia o *proxy*.
  
  Execute as etapas a seguir para configurar seu aplicativo Node.js com o [StrongLoop Arc](https://strongloop.com/node-js/arc){:new_window}.

    1. Configure a variável de ambiente *strongpm* BlUEMIX_APP_MGMT_ENABLE e remonte seu aplicativo.
    
	```
    cf set-env <appname> BLUEMIX_APP_MGMT_ENABLE strongpm
    cf restage <appname>
    ```
	
    2. Na linha de comandos do Cloud Foundry, inclua uma rota em seu aplicativo, onde a rota tiver "-pm" anexado ao nome do aplicativo, como <appname>-pm.mybluemix.net.
    
	```
    cf map-route <appname> ng.bluemix.net -n <appname>-pm
    ```
	
    3. Instale o [módulo StrongLoop npm](https://www.npmjs.com/package/strongloop){:new_window} na estação de trabalho local.
    
	```
    npm install -g strongloop
    ```
	
    4. Crie uma conta no [website do StrongLoop](https://strongloop.com/register/){:new_window}.
    5. Ative Arc em sua estação de trabalho local e efetue login com a conta criada.
    
	```
    slc arc
    ```
	
    6. Navegue para a visualização Process Manager no Arc. Insira a rota recém-criada com a porta 80 no Process Manager. Pressione o botão Ativar. Consulte a [documentação completa sobre como usar Arc](https://docs.strongloop.com/display){:new_window} para obter mais detalhes.
	
  3. *trace*: irá configurar dinamicamente os níveis de rastreio se seu aplicativo estiver usando os módulos de criação de log *log4js*, *ibmbluemix* ou *bunyan*.
  
  **Nota**: versões de dependência suportadas:

    * log4js:(0.6.0 - 0.6.24)
    * bunyan: (1.0.0, 1.0.1, 1.1.0 - 1.1.3, 1.2.0 - 1.2.3, 1.3.0 - 1.3.5)
    * ibmbluemix: (1.0.0-20140707-1250)-(1.0.0-20150409-1328)
  
  Acesse a página Detalhes da instância no console da web do {{site.data.keyword.Bluemix_notm}} e selecione **Ações** para ver a interface com o usuário.

  O utilitário *trace* não inicia o *proxy*.

##Como configurar o App Management
{: #configure}

Para ativar os utilitários do App Management, configure a variável de ambiente *BLUEMIX_APP_MGMT_ENABLE*
e remonte seu aplicativo. É possível ativar diversos utilitários separando-os com um “+”.

Por exemplo, para ativar os utilitários devconsole e *shell*, execute o comando a seguir:

```
cf set-env myApp BLUEMIX_APP_MGMT_ENABLE devconsole+shell
```

Não se esqueça de remontar seu aplicativo depois de configurar a variável de ambiente:

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

##Restrictions
{: #restrictions}

* O App Management suporta apenas aplicativos de instância única.
* Mudanças feitas no aplicativo usando o App Management são temporárias e serão perdidas após a saída desse modo. Este modo destina-se somente ao uso de
desenvolvimento provisório e não deve ser usado como um ambiente de produção
devido ao desempenho.
* A maioria dos utilitários do App Management não funcionará se você configurar seu comando inicial no arquivo manifest.yml (comando) ou CF CLI (-c). Esses métodos são substituições de buildpack e são antipadrões para iniciar aplicativos Node.js. Para obter melhores resultados, configure o comando inicial no arquivo package.json ou Procfile.

##Modo de desenvolvimento para Eclipse Tools
{: #devmode}

Modo de desenvolvimento é um recurso do [Eclipse Tools for {{site.data.keyword.Bluemix_notm}}](../manageapps/eclipsetools/eclipsetools.html#eclipsetools) que fornece aos desenvolvedores a capacidade de trabalhar com seus aplicativos enquanto eles estão em execução na nuvem.

Ao trabalhar com seus aplicativos no {{site.data.keyword.Bluemix_notm}}, os desenvolvedores podem achar que não podem
executar atividades normais de desenvolvimento como eles o fazem em um ambiente local. Para resolver esse problema,
o modo de desenvolvimento fornece, por meio do Eclipse Tools, uma maneira para você trabalhar na nuvem enquanto está em uma
área de trabalho segura provisória.

O modo de desenvolvimento é suportado para aplicativos Liberty e Node.js. Com o modo de desenvolvimento
ativado para seu aplicativo Liberty ou Node.js, é possível atualizar arquivos de aplicativos incrementalmente
sem precisar que enviar seu aplicativo por push. É possível também estabelecer uma sessão de depuração com seu
aplicativo. O modo de desenvolvimento para aplicativos Liberty é equivalente e ativar os utilitários
debug e jmx do App Management. Para aplicativos Node.js, é equivalente a ativar os utilitários *devconsole*, *inspector* e *shell*.
