---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Monitorando o Liberty no Bluemix com o JConsole
{: #jconsole}

*Última atualização: 23 de março de 2016*

## As etapas para monitorar o tempo de execução do Bluemix Liberty com o JConsole são as seguintes:
{: #steps_to_monitor}

1. Envie por push seu aplicativo em um pacote do servidor que contenha um server.xml apropriado.
2. Inicie o app JConsole com as propriedades de sistema adequadas na linha de comandos.
3. Forneça a URL adequada do processo remoto, o Nome do usuário e a Senha para o JConsole.

### Enviar por push o pacote do servidor
{: #push_server_package}

Envie por push o pacote do servidor que contém seu aplicativo, limitando-o a uma instância única. Seu arquivo server.xml deve conter os recursos `monitor-1.0` e `restConnector-1.0`. Ele também deve conter um elemento basicRegistry e um elemento administrator-role.
```xml
       <featureManager>
           <feature>jsp-2.2</feature>
           <feature>monitor-1.0</feature>
           <feature>restConnector-1.0</feature>
       </featureManager>

       <basicRegistry>
           <user name="jconuser" password="jconpassw0rd"/>
       </basicRegistry>

       <administrator-role>
           <user>jconuser</user>
       </administrator-role>
```
{: #codeblock}

   * Nota: a senha deve ser codificada com a ferramenta securityUtility fornecida pelo Liberty.

### Iniciar o app JConsole
{: #start_jconsole_app}

JConsole é incluído com sua instalação Java. Para iniciar o app JConsole, acesse &lt;java-home&gt;/bin e execute o comando a seguir:
```
    $ jconsole -J-Djava.class.path=<java-home>/lib/jconsole.jar;<liberty-home>/wlp/clients/restConnector.jar
```
{: #codeblock}

Talvez você tenha de passar parâmetros adicionais para configurar o armazenamento confiável Java. Os parâmetros a seguir devem funcionar na maioria dos casos:
```
    -J-Djavax.net.ssl.trustStore=<java-home>/jre/lib/security/cacerts -J-Djavax.net.ssl.trustStorePassword=changeit -J-Djavax.net.ssl.trustStoreType=jks
```
{: #codeblock}

### Concluir a conexão
{: #start_jconsole_app}
  * Preencha o campo Processo remoto com a URL a seguir:
    * service:jmx:rest://&lt;appName&gt;.mybluemix.net:443/IBMJMXConnectorREST.
  *  Além disso, preencha os campos Nome do usuário e Senha com um usuário e uma senha da função de administrador a partir do arquivo server.xml.
  * Clique em Conectar.

Quando a conexão for bem-sucedida, o
JConsole iniciará o monitoramento.

Se a conexão falhar, é possível produzir logs para ajudar a diagnosticar o problema.
Primeiramente, tente coletar o rastreio do lado do cliente incluindo **
-J-Djava.util.logging.config.file=c:/tmp/logging.properties** no comando jconsole.
Aqui está um arquivo de propriedade de criação de log de amostra:
```
    handlers= java.util.logging.FileHandler
    .level=INFO java.util.logging.FileHandler.pattern = /tmp/jmxtrace.log
    java.util.logging.FileHandler.limit = 50000
    java.util.logging.FileHandler.count = 1
    java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
    javax.management.level=FINEST
    javax.management.remote.level=FINER
    com.ibm.level=FINEST
```
{: #codeblock}

Também é possível incluir <b>&dash;J&dash;Djavax.net.debug=ssl</b> no comando jconsole. Isso produz o rastreio de diagnóstico SSL em uma janela de saída separada do JConsole.  Por último, é possível ativar o rastreio no lado do servidor, incluindo o seguinte em seu arquivo server.xml:
```
    <logging traceSpecification="com.ibm.ws.jmx.*=all"/>
```
{: codeblock}

# rellinks
## geral
* [Tempo de execução do Liberty](index.html)
* [Visão geral do perfil do Liberty](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
