---

copyright:
  years: 2017
lastupdated: "2017-02-07"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Usando o Oracle JRE
{: #using_oraacle_jre}

Será possível executar o aplicativo Liberty no Bluemix com o Oracle JRE se você escolher essa opção.  Para isso, deve-se
* hospedar o JRE em um local a partir do qual o buildpack possa fazer download dele,
* hospedar um arquivo `index.yml` que forneça o local do JRE do host e
* configurar seu aplicativo para usar esse JRE.

## Hospedando o JRE e o index.yml
{: #hosting_jre}

O arquivo do Oracle JRE deve ser hospedado em um servidor da web e o buildpack do Liberty deve estar apto a fazer o download dele a partir desse servidor. É possível hospedá-lo no próprio Bluemix, usando qualquer um dos recursos do servidor disponível ou hospedá-lo em algum local publicamente disponível.  O servidor deve ser configurado com um arquivo `index.yml` que especifique detalhes sobre o arquivo JRE. Conclua as etapas a seguir para hospedar o JRE e o arquivo `index.yml`:
  1. Adquira o Oracle JRE.  Observe que o JRE deve ser a versão para uso em um OS Unix de 64 bits e deve ser um arquivo `tar.gz`.
  2. Hospede o arquivo JRE em um local a partir do qual o buildpack do Liberty possa fazer download dele. 
  3. Assegure-se de fornecer um arquivo `index.yml` no local de hosting. O arquivo `index.yml` deve conter uma entrada que consista no ID da versão do Oracle JRE seguido por dois-pontos (:) e a URL completa do local desse arquivo JRE. O formato do `index.yml` é:
```
   ---
   jre_version: https://hostingLocation/jreName.tar.gz
```
{: codeblock}

    * Por exemplo:
    ```
       ---
       1.8.0_91: https://myHostingApp.ng.bluemix.net/jre-8u91-fcs-bin-b14-linux-x64-01_apr_2016.tar.gz
    ```

## Configure o app
{: #configure_app}

Duas variáveis de ambiente devem ser configuradas no aplicativo Liberty. A *JBP_CONFIG_OPENJDK* deve ser configurada para especificar o local do arquivo `index.yml` e a variável de ambiente *JVM* deve ser configurada como *openjdk* para configurar o buildpack para usar um JRE alternativo.

Para a variável JBP_CONFIG_OPENJDK, o valor é
```
   'repository_root: "https://locationToIndexYml"'
```
{: codeblock}

Para configurar isso, é possível emitir um comando como:
```
   $ cf se myApp JBP_CONFIG_OPENJDK 'repository_root: https://myHostingApp.ng.bluemix.net'
```
{: codeblock}

Observe que a URL *repository_root* não inclui `index.yml`, mas para bem antes de seu local.

Para configurar a variável de ambiente JVM, emita um comando como:
```
   $ cf se myApp JVM 'openjdk'
```
{: codeblock}

**Nota**: deve-se remontar seu aplicativo depois de configurar as variáveis de ambiente.

## Confirmation
{: #confirmation}

Para confirmar se o JRE esperado está sendo usado, procure no log de preparação uma mensagem semelhante à seguinte:
```
   -----> Downloading OpenJdk 1.8.0_91 from https://myHostingApp.ng.bluemix.net/jre-8u91-fcs-bin-b14-linux-x64-01_apr_2016.tar.gz (6.2s)
```
{: codeblock}

# rellinks
{: #rellinks notoc}
## geral
{: #general notoc}
* [Tempo de execução do Liberty](index.html)
* [Visão geral do perfil Liberty](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
