---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Opções para enviar por push os apps Liberty
{: #options_for_pushing}

*Última atualização: 23 de março de 2016*

O comportamento do servidor Liberty no Bluemix é controlado pelo buildpack do Liberty. Os buildpacks podem fornecer um ambiente de tempo de execução completo para uma classe específica de aplicativos. Eles são a chave para fornecer a portabilidade nas nuvens e para contribuir com uma arquitetura de nuvem aberta. O buildpack do Liberty fornece um contêiner do WebSphere Liberty capaz de executar os aplicativos Java EE 7 e OSGi. Ele suporta estruturas populares como Spring e inclui o IBM JRE. O WebSphere Liberty permite o desenvolvimento rápido de aplicativo que é adequado para a nuvem. O buildpack do Liberty suporta diversos aplicativos que são implementados em um único servidor do Liberty. Como parte da integração do buildpack do Liberty no Bluemix, o buildpack assegura que as variáveis de ambiente para os serviços de ligação sejam mostradas como variáveis de configuração no servidor Liberty.

É possível usar os métodos a seguir para implementar seus aplicativos Liberty no Bluemix.

* Enviando um aplicativo independente por push
* Enviando um diretório de servidor por push
* Enviando um servidor em pacote por push

Importante: quando você implementa um aplicativo com o buildpack do Liberty, especifique um mínimo de 512 M como o limite de memória para seus aplicativos. Para obter mais informações, veja [Limites de memória e o buildpack do Liberty](memoryLimits.html).

## Apps independentes
{: #stand_alone_apps}

Os aplicativos independentes como os arquivos WAR ou EAR podem ser implementados no Liberty no Bluemix.

Para implementar um aplicativo independente, execute o comando cf push com o parâmetro -p que aponta para seu arquivo WAR ou EAR.
Por exemplo:

```
    $ cf push <yourappname> -p myapp.war
```
{: #codeblock}

Quando um aplicativo independente for implementado, uma configuração padrão do Liberty é fornecida ao aplicativo. A configuração padrão permite os recursos do Liberty a seguir:

* beanValidation-1.1
* [cdi-1.2](optionsForPushing.html#cdi12)
* ejbLite-3.2
* el-3.0
* jaxrs-2.0
* jdbc-4.1
* jndi-1.0
* jpa-2.1
* jsf-2.2
* jsonp-1.0
* jsp-2.3
* managedBeans-1.0
* servlet-3.1
* websocket-1.1
* icap:managementConnector-1.0
* appstate-1.0

Esses recursos correspondem aos recursos do Java EE 7 Web Profile. É possível especificar um conjunto diferente de recursos do Liberty configurando a variável de ambiente JBP_CONFIG_LIBERTY. Por exemplo, para ativar somente os recursos jsp-2.3 e websocket-1.1, execute o comando e remonte o aplicativo:

```
    $ cf set-env myapp JBP_CONFIG_LIBERTY "app_archive: {features: [jsp-2.3, websocket-1.1]}"
```
{: #codeblock}

Nota: para obter resultados melhores, configure os recursos do Liberty com a variável de ambiente JBP_CONFIG_LIBERTY ou implemente o aplicativo como um [diretório do servidor](optionsForPushing.html#server_directory) ou [servidor em pacote](optionsForPushing.html#packaged_server) com um arquivo server.xml customizado. Configurar essa variável de ambiente assegura que seu aplicativo use somente o recurso necessário e não seja afetado pelas mudanças do conjunto de recursos padrão do Liberty do buildpack. Se você precisar fornecer configuração Liberty extra além do conjunto de recursos, use o [diretório do servidor](optionsForPushing.html#server_directory) ou a opção [servidor em pacote](optionsForPushing.html#packaged_server) para implementar o seu aplicativo.

Se você implementou um arquivo WAR, o aplicativo da web ficará acessível sob a raiz de contexto conforme configurado no arquivo ibm-web-ext.xml integrado. Se o arquivo ibm-web-ext.xml não existir ou não especificar a raiz de contexto, o aplicativo ficará acessível sob o contexto-raiz. Por exemplo,

```
    http://<yourappname>.mybluemix.net/
```
{: #codeblock}

Se você implementou um arquivo EAR, o aplicativo da Web integrado ficará acessível na raiz do contexto, conforme definido no descritor de implementação do EAR. Por exemplo,

```
    http://<yourappname>.mybluemix.net/acme/
```
{: #codeblock}

O arquivo de configuração server.xml padrão inteiro do Liberty é como a seguir:
```
    <server>
       <featureManager>
          <feature>beanValidation-1.1</feature>
          <feature>cdi-1.2</feature>
          <feature>ejbLite-3.2</feature>
          <feature>el-3.0</feature>
          <feature>jaxrs-2.0</feature>
          <feature>jdbc-4.1</feature>
          <feature>jndi-1.0</feature>
          <feature>jpa-2.1</feature>
          <feature>jsf-2.2</feature>
          <feature>jsonp-1.0</feature>
          <feature>jsp-2.3</feature>
          <feature>managedBeans-1.0</feature>
          <feature>servlet-3.1</feature>
          <feature>websocket-1.1</feature>
          <feature>icap:managementConnector-1.0</feature>
          <feature>appstate-1.0</feature>
       </featureManager>

       <application name='myapp' location='myapp.war' type='war' context-root='/'/>
       <httpEndpoint id='defaultHttpEndpoint' host='*' httpPort='${port}'/>
       <webContainer trustHostHeaderPort='true' extractHostHeaderPort='true'/>
       <include location='runtime-vars.xml'/>
       <logging logDirectory='${application.log.dir}' consoleLogLevel='INFO'/>
       <httpDispatcher enableWelcomePage='false'/>
       <applicationMonitor dropinsEnabled='false' updateTrigger='mbean'/>
       <config updateTrigger='mbean'/>
       <cdi12 enableImplicitBeanArchives='false'/>
       <appstate appName='myapp' markerPath='${home}/../.liberty.state'/>
    </server>
```
{: #codeblock}

### CDI 1.2
{: #cdi12}

Por motivos de desempenho, ao implementar os arquivos WAR e EAR somente, a [varredura de bean archives implícita CDI 1.2](https://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_cdi_behavior.html) fica desativada por padrão. A varredura de archives de beans explícitos pode ser ativada usando a variável de ambiente JBP_CONFIG_LIBERTY.
Por exemplo:

```
    $ cf set-env myapp JBP_CONFIG_LIBERTY "app_archive: { implicit_cdi: true }"
```    
{: #codeblock}

Importante: para que as mudanças da variável de ambiente entrem em vigor, deve-se remontar seu aplicativo:

```
    $ cf restage myapp
```
{: #codeblock}

## Diretório do servidor
{: #server_directory}

Em alguns casos, pode ser necessário fornecer uma configuração do servidor Liberty customizada com seu aplicativo. Essa configuração customizada pode ser necessária quando você implementa um arquivo WAR ou EAR e o arquivo server.xml padrão não tem certas configurações necessárias para seu aplicativo.

Se você instalou o perfil Liberty em sua estação de trabalho e já criou um servidor Liberty com seu aplicativo, é possível enviar o conteúdo desse diretório para o Bluemix.
Por exemplo, se o seu servidor Liberty for nomeado defaultServer, execute o comando:

```
    $ cf push <yourappname> -p wlp/usr/servers/defaultServer
```
{: #codeblock}

Se um perfil Liberty não estiver instalado em sua estação de trabalho, será possível usar as etapas a seguir para criar um diretório do servidor com seu aplicativo:

1. Crie um diretório nomeado defaultServer.
2. Crie um diretório apps no diretório defaultServer.
3. Copie seu arquivo WAR ou EAR no diretório defaultServer/apps.
4. No diretório defaultServer, crie um arquivo server.xml com o conteúdo de exemplo a seguir.  Além disso:
  * Assegure-se de atualizar o local ou o atributo de tipo do elemento do aplicativo para corresponder o nome do arquivo e o tipo do aplicativo.
  * O arquivo server.xml no diagrama mostra um conjunto mínimo de recursos. Pode ser necessário ajustar o conjunto de recursos dependendo das necessidades do aplicativo.

```
    <server>
        <featureManager>
            <feature>jsp-2.3</feature>
        </featureManager>

        <httpEndpoint id="defaultHttpEndpoint" host="*" httpPort="8080" />

        <application name="myapp" context-root="/" type="war" location="myapp.war"/>
    </server>
```
{: #codeblock}

Depois que o diretório do servidor estiver pronto, será possível implementá-lo no Bluemix.

```
    $ cf push <yourappname> -p defaultServer
```
{: #codeblock}

Nota: os aplicativos da Web que são implementados como parte do diretório do servidor são acessíveis sob a [raiz de contexto, conforme determinado pelo perfil Liberty](http://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/twlp_dep_war.html?cp=SSAW57_8.5.5%2F1-3-11-0-5-6). Por exemplo:

```
    http://<yourappname>.mybluemix.net/acme/
```
{: #codeblock}

## Servidor em pacote
{: #packaged_server}

Também é possível enviar por push um arquivo do servidor em pacote para o Bluemix. O arquivo de servidor em pacote é criado usando o comando de pacote do servidor Liberty. Além do aplicativo e dos arquivos de configuração, o arquivo do servidor em pacote pode conter recursos compartilhados e recursos do usuário do Liberty necessários pelo aplicativo.

Para colocar em pacote um servidor Liberty, use o comando ./bin/server package a partir do diretório de instalação do Liberty. Especifique o nome do servidor e inclua a opção '––include=usr'.
Por exemplo, se o servidor Liberty for defaultServer, execute o comando:

```
    $ wlp/bin/server package defaultServer --include=usr
```
{: #codeblock}

Esse comando gera um arquivo serverName.zip no diretório do servidor. É possível então enviar por push esse arquivo compactado para o Bluemix com o comando cf push.
Por exemplo:

```
    $ cf push <yourappname> -p wlp/usr/servers/defaultServer/defaultServer.zip
```
{: #codeblock}

Nota: os aplicativos da web que são implementados como parte do servidor em pacote são acessíveis sob a raiz de contexto, conforme determinado pelo perfil Liberty.

### Modificação do arquivo server.xml
{: #modifications_of_serverxml}

Quando um servidor em pacote ou um diretório do servidor Liberty é enviado por push, o buildpack do Liberty detecta o arquivo server.xml juntamente com seu aplicativo. O buildpack do Liberty faz as modificações a seguir no arquivo server.xml.

* O buildpack assegura que haja exatamente um elemento httpEndpoint no arquivo.
* O buildpack assegura que o atributo httpPort no elemento httpEndpoint aponte para uma variável do sistema chamada ${port}. O buildpack também substitui o atributo host.
* O buildpack configura o atributo logDirectory no elemento de criação de log para apontar para um diretório de log do sistema.
* O buildpack assegura que um arquivo runtime-vars.xml seja mesclado logicamente com seu arquivo server.xml. Especificamente, o buildpack anexa a linha *&lt;include location="runtime-vars.xml" /&gt;* ao seu arquivo server.xml.

### Variáveis referenciáveis
{: #referenceable_variables}

As variáveis a seguir são definidas no arquivo runtime-vars.xml e referenciadas a partir de um arquivo server.xml enviado por push. Todas as variáveis fazem distinção entre maiúsculas e minúsculas.

* ${port}: a porta HTTP em que o servidor Liberty está atendendo.
* ${vcap_console_port}: a porta em que o console vcap está em execução (geralmente igual a ${port}).
* ${vcap_app_port}: a porta em que o servidor app está atendendo (geralmente igual a ${port}).
* ${vcap_console_ip}: o endereço IP do console vcap (geralmente é o endereço IP no qual o servidor Liberty está atendendo).
* ${application_name}: o nome do aplicativo, conforme definido usando as opções no comando cf push.
* ${application_version}: a versão dessa instância do aplicativo, que assume a forma de um UUID, como, por exemplo, b687ea75-49f0-456e-b69d-e36e8a854caa. Esta variável muda à cada envio sucessivo por push do aplicativo que contém uma codificação nova ou muda para os artefatos de aplicativo.
* ${host}: o endereço IP do DEA que está executando o aplicativo (geralmente é o mesmo que ${vcap_console_ip}).
* ${application_uris}: uma matriz de estilo JSON dos terminais que podem ser usados para acessar esse aplicativo. Por exemplo: myapp.mydomain.com.
* ${start}: a data e a hora em que o aplicativo foi iniciado, assumindo uma forma semelhante a 2013-08-22 10:10:18 -0400.

### Acessando informações de serviços ligados
{: #accessing_info_of_bound_services}

Quando desejar ligar um serviço a seu aplicativo, as informações sobre o serviço, como as credenciais de conexão, são incluídas na [Variável de ambiente VCAP_SERVICES](http://docs.run.pivotal.io/devguide/deploy-apps/environment-variable.html#VCAP-SERVICES) que o Cloud Foundry configura para o aplicativo. Para os [serviços automaticamente configurados](autoConfig.html), o buildpack Liberty gera ou atualiza entradas de ligação de serviço no arquivo server.xml. O conteúdo das entradas de ligação de serviço pode estar em um dos formatos a seguir:

* cloud.services.&lt;service-name&gt;.&lt;property&gt;, que descreve as informações como o nome, o tipo e o plano do serviço.
* cloud.services.&lt;service-name&gt;.connection.&lt;property&gt;, que descreve as informações de conexão para o serviço.

O conjunto de informações típico é o seguinte:
* name: o nome do serviço. Por exemplo, mysql-e3abd.
label: o tipo do serviço criado. Por exemplo, mysql-5.5.
* plan: o plano de serviço, conforme indicado pelo identificador exclusivo para esse plano. Por exemplo, 100.
connection.name: um identificador exclusivo para a conexão, que assume a forma de um UUID. Por exemplo, d01af3a5fabeb4d45bb321fe114d652ee.
* connection.hostname: o nome do host do servidor que está executando o serviço. Por exemplo, mysql-server.mydomain.com.
* connection.host: o endereço IP do servidor que está executando o serviço. Por exemplo, 9.37.193.2.
* connection.port: a porta na qual o serviço está atendendo para conexões recebidas. Por exemplo, 3306,3307.
* connection.user: o nome do usuário que é usado para autenticar esse aplicativo para o serviço. O nome do usuário é gerado automaticamente pelo Cloud Foundry. Por exemplo: unHwANpjAG5wT.
* connection.username: um alias para connection.user.
* connection.password: a senha que é usada para autenticar esse aplicativo para o serviço. A senha é gerada automaticamente pelo Cloud Foundry. Por exemplo: pvyCY0YzX9pu5.

Para serviços ligados que não sejam automaticamente configurados pelo buildpack do Liberty, o aplicativo precisa gerenciar o acesso do recurso de backend sozinho.

# rellinks
## geral
* [Tempo de execução do Liberty](index.html)
* [Visão geral do perfil do Liberty](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
