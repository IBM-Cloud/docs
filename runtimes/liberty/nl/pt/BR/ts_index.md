---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-07"

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Resolução de problemas do Liberty for Java
{: #ts}


A seguir estão as respostas para perguntas comuns de resolução de problemas sobre o uso do Liberty for
Java no {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## O aplicativo falha ao começar a aceitar conexões
{: #health_check_timeout}


Um aplicativo Liberty falha ao iniciar com o erro "Falha ao começar a aceitar conexões". Por exemplo, o
erro nos logs pode ser semelhante ao seguinte:
{: tsSymptoms}

```
   2016-11-14T14:44:58.45+0000 [API/0]      OUT App instance exited with guid 21ac63eb-9595-428a-94c7-b0b02aaf77cc payload: {"cc_partition"=>"default", "droplet"=>"21ac63eb-9595-428a-94c7-b0b02aaf77cc", "version"=>"b2772438-92de-4d47-b680-ea772ac2288a", "instance"=>"f4799c8c89214bbd8067883c3ffe23e0", "index"=>0, "reason"=>"CRASHED", "exit_status"=>255, "exit_description"=>"failed to accept connections within health check timeout", "crash_timestamp"=>1479134698} 2016-11-14T14:45:07.50+0000 [DEA/4]      ERR Instance (index 0) failed to start accepting connections
```
{: #codeblock}

O Bluemix executa uma verificação de funcionamento no aplicativo para ver se ele iniciou com sucesso. A verificação de funcionamento testa se o aplicativo está atendendo na porta designada ao aplicativo. O tempo limite padrão para essa verificação é de 60 segundos e alguns aplicativos podem demorar mais de 60 segundos para iniciar. Há vários motivos pelos quais o aplicativo pode levar mais tempo para iniciar. Por exemplo, a ligação de serviços como o [Monitoring and Analytics](/docs/services/monana/index.html#gettingstartedtemplate) ou o [New Relic](/docs/runtimes/liberty/newRelic.html) ou [ativar o depurador](/docs/manageapps/app_mng.html#debug) aumentará o tempo de inicialização. O aplicativo também pode executar etapas de inicialização que podem levar muito tempo para serem concluídas.
{: tsCauses}

Primeiro, examine nos logs se há quaisquer erros óbvios que possam causar falha do aplicativo
Liberty. Se não forem encontrados erros óbvios, tente o seguinte:
{: tsResolve}

### **Aumente o tempo limite de verificação de funcionamento. **

* Ao implementar o aplicativo usando o comando
"cf push", especifique um tempo limite de início de aplicativo maior usando a opção "t". Por exemplo:

        $ cf push myApp -t 180
        {: #codeblock}

* O tempo limite de verificação de funcionamento também pode ser especificado no arquivo manifest.yml. Por exemplo:

        ---
           ...
           timeout: 180
        {: #codeblock}

### **Desative o recurso appstate. **

O recurso appstate é integrado com o processo de verificação de
funcionamento do Bluemix para assegurar que o aplicativo Liberty seja totalmente inicializado antes que o
aplicativo possa receber as solicitações de HTTP. Quando o aplicativo estiver totalmente inicializado, o recurso appstate não terá mais efeito. O efeito colateral deste recurso é que alguns aplicativos
podem levar mais tempo para inicializar. Para desativar o recurso appstate, configure a propriedade de
ambiente a seguir em seu aplicativo e remonte o aplicativo:

```
$ cf set-env myApp JBP_CONFIG_LIBERTY “app_state: false”
```
{: #codeblock}

### **Considere a refatoração do aplicativo. **

Se seu aplicativo levar muito tempo para inicializar, poderá
ser necessário refatorar o aplicativo para executar inicialização lenta e/ou assíncrona.

### **Implementar com a opção "no-route".**

1. Implemente seu aplicativo com a opção “--no-route”. Isso desativará a verificação de funcionamento da porta. Por exemplo:

        $ cf push myApp –no-route
        {: #codeblock}

2. Quando o aplicativo for inicializado, mapeie uma rota para o aplicativo. Por exemplo:

        $ cf map-route myApp mybluemix.net
        {: #codeblock}

## Erros de SSL com gateway IBM
{: #ssl_handshake_failure}


Os erros a seguir são visíveis nos logs e o aplicativo poderá falhar ao iniciar:
{: tsSymptoms}

```
    2016-11-03T12:32:44.82-0200 [App/0]      ERR java.security.cert.CertPathValidatorException: Certificate chaining error 2016-11-03T12:32:44.83-0200 [App/0]      ERR [ERROR   ] CWPKI0022E: SSL HANDSHAKE FAILURE:  A signer with SubjectDN CN=*.gateway.prd.na.ca.ibmserviceengage.com, O=International Business Machines Corp., L=Armonk, ST=New York, C=US was sent from the target host.  O assinante poderá precisar ser incluído no armazenamento confiável local
/home/vcap/app/wlp/usr/servers/defaultServer/resources/security/key.jks,
localizado no alias de configuração SSL defaultSSLConfig. The extended error message from the SSL handshake exception is: PKIX path building failed: java.security.cert.CertPathBuilderException: PKIXCertPathBuilderImpl could not build a valid CertPath.; internal cause is: 2016-11-03T12:32:44.83-0200 [App/0]      ERR java.security.cert.CertPathValidatorException: The certificate issued by CN=DigiCert Global Root CA, OU=www.digicert.com, O=DigiCert Inc, C=US is not trusted; internal cause is: 2016-11-03T12:32:44.83-0200 [App/0]      ERR java.security.cert.CertPathValidatorException: Certificate chaining error
```
{: codeblock}

Os erros podem ser gerados quando o serviço de Monitoramento e Analítica for ligado a um aplicativo
Liberty e o aplicativo Liberty for implementado como um diretório do servidor ou como um servidor empacotado que
contém server.xml que configura o recurso ssl-1.0 do Liberty. A ligação do serviço de Monitoramento
e Analítica ao aplicativo Liberty faz com que o tempo de execução se conecte ao serviço por meio
de uma conexão segura. Esta conexão segura é estabelecida usando as configurações de SSL padrão. Como as
configurações de SSL padrão são especificadas no server.xml do Liberty, o armazenamento confiável configurado
pode não confiar no certificado utilizado pelo serviço de Monitoramento e Analítica.
{: tsCauses}

Modifique a configuração para usar o armazenamento confiável da JVM com uma das opções a seguir. Certifique-se de remontar seu aplicativo depois de fazer a mudança.
{: tsResolve}

### Atualizar o server.xml do Liberty

Atualize o server.xml para usar o arquivo cacerts da JVM como o armazenamento confiável. Inclua o seguinte no seu server.xml:

        <ssl id="defaultSSLConfig" trustStoreRef="defaultTrustStore"/>
        <keyStore id="defaultTrustStoretore" location="${java.home}/lib/security/cacerts"/>
        {: codeblock}

### Atualizar o armazenamento confiável configurado

Modifique o armazenamento confiável configurado para confiar na autoridade de certificação raiz DigitCert.
  1. Faça download da autoridade de certificação raiz DigiCert de https://www.digicert.com/CACerts/DigiCertGlobalRootCA.crt.
  2. Supondo que resources/security/key.jks seja usado como o armazenamento confiável, importe a autoridade de certificação para a chave usando o utilitário keytool de Java:

            $ keytool -importcert --storepass <keyStorePassword> -keystore &lt;path&gt;/resources/security/key.jks -file DigiCertGlobalRootCA.crt
            {: codeblock}
