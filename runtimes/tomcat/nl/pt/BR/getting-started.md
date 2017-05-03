---

copyright:
  years: 2017
lastupdated: "2017-04-04"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# Introdução ao Tomcat no Bluemix
{: #getting_started}

* {: download} Parabéns, você implementou um aplicativo de amostra Hello World no {{site.data.keyword.Bluemix}}! Para iniciar, siga este guia passo a passo. Ou <a class="xref" href="http://bluemix.net" target="_blank" title="(Fazer download de código de amostra)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="Fazer download de código do aplicativo" />faça download do código de amostra</a> e explore você mesmo.

Seguindo esse guia, você configurará um ambiente de desenvolvimento, implementará um app localmente e no {{site.data.keyword.Bluemix}} e integrará um serviço de banco de dados do {{site.data.keyword.Bluemix}} em seu app.

## Pré-requisito
{: #prereqs}

Você precisará do seguinte:
* [Conta do {{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net/registration/)
* [Cloud Foundry CLI ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Eclipse IDE for Java EE Developers ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/neon2){: new_window}
* [Git ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://git-scm.com/downloads){: new_window}
* [Maven ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://maven.apache.org/download.cgi){: new_window}
* [Apache Tomcat versão 8.0.41 ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://tomcat.apache.org/download-80.cgi#8.0.41 ){: new_window}


## 1. Clone o app de amostra
{: #clone}

Agora você está pronto para começar a trabalhar com o app Tomcat de amostra. Clone o repositório e mude para o diretório no qual o app de amostra está localizado.
```
git clone https://github.com/IBM-Bluemix/get-started-tomcat
```
{: pre}

```
cd get-started-tomcat
```
{: pre}

Examine os arquivos no diretório *get-started-tomcat* para familiarizar-se com o conteúdo.

## 2. Execute o app localmente
{: #run_locally}

Deve-se instalar as dependências e construir um arquivo .war conforme definido no arquivo pom.xml para executar o app.

Instale as dependências.

```
mvn clean install  
```
{: pre}


Copie GetStartedTomcat.war do diretório `target` para o diretório `tomcat-install-dir` `webapps`.

Execute o app.  
```
<tomcat-install-dir>/bin/startup.bat|.sh
```
{: screen}

Visualize seu app em: http://localhost:8080/GetStartedTomcat/

Use `shutdown.bat|.sh` para parar seu app. Observe que poderá ser necessário fornecer a permissão de execução aos comandos.
{: tip}

## 3. Prepare o app para implementação do {{site.data.keyword.Bluemix_notm}}
{: #prepare}

Para implementar no {{site.data.keyword.Bluemix_notm}}, poderá ser útil configurar um arquivo manifest.yml. O manifest.yml inclui informações básicas sobre seu app, como o nome, quanta memória alocar para cada instância e a rota. Nós fornecemos um arquivo manifest.yml de amostra no diretório `get-started-tomcat`.

Abra o arquivo manifest.yml e mude o `nome` de `GetStartedTomcat` para o nome de seu app, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
  applications:
  - name: GetStartedTomcat
    random-route: true
    memory: 256M
    path: target/TomcatHelloWorldApp.war
    buildpack: java_buildpack
  ```
  {: codeblock}

Nesse arquivo manifest.yml, **random-route: true** gera uma rota aleatória para seu app para evitar que sua rota colida com outras. Se você optar por isso, será possível substituir **random-route: true** por **host: myChosenHostName**, fornecendo um nome de host de sua preferência. [Saiba mais...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## 4. Implemente o app
{: #deploy}

É possível usar a CLI do Cloud Foundry para implementar apps.

Escolha seu terminal de API

```
cf api <API-endpoint>
```
{:pre}

Substitua o *API-endpoint* no comando por um terminal de API da lista a seguir.

|URL                             |Região          |
|:-------------------------------|:---------------|
| https://api.ng.bluemix.net     | SUL dos EUA       |
| https://api.eu-gb.bluemix.net  | United Kingdom |
| https://api.au-syd.bluemix.net | Sydney         |


Efetue login em sua conta do {{site.data.keyword.Bluemix_notm}}:

```
cf login
```
{: pre}

No diretório *get-started-tomcat*, envie seu app por push para o {{site.data.keyword.Bluemix_notm}}
```
cf push
```
{: pre}

Isso pode levar aproximadamente dois minutos. Se houver um erro no processo de implementação, será
possível usar o comando `cf logs <Your-App-Name> --recent` para
solucionar problemas.

Quando a implementação for concluída, você deverá ver uma mensagem indicando que o app está em execução. Visualize o app na URL listada na saída do comando push. Também é possível emitir o comando
  ```
cf apps
  ```
  {: pre}
para visualizar o status dos apps e ver a URL.

## 6. Desenvolvendo no Eclipse
{: #developing_in_eclipse}

O IBM® Eclipse Tools for {{site.data.keyword.Bluemix}} fornece plug-ins que podem ser instalados em um ambiente existente do Eclipse para ajudar na integração de seu ambiente de desenvolvimento integrado (IDE) do desenvolvedor com o {{site.data.keyword.Bluemix_notm}}.

Faça download e instale o [IBM Eclipse Tools for Bluemix](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix).

Importe essa amostra para o Eclipse usando a opção `Arquivo` -> `Importar` -> `Maven` -> `Projetos existentes do Maven`.

Crie uma definição de servidor Tomcat:
  - Na visualização `Servidores`, clique com o botão direito -> `Novo` -> `Servidor`.
  - Selecione `Apache` -> `Servidor Tomcat v8.0`.
  - Escolha o `tomcat-install-dir`.
  - Continue o assistente com opções padrão para Concluir.

Execute seu aplicativo localmente no servidor Apache.
  - Clique com o botão direito na amostra `GetStartedTomcat` e selecione a opção `Executar como` -> `Executar no servidor`.
  - Localize e selecione o servidor Tomcat localhost e pressione Concluir.
  - Em alguns segundos, seu aplicativo deverá estar em execução em http://localhost:8080/TomcatHelloWorldApp/

Crie uma definição de servidor {{site.data.keyword.Bluemix_notm}}:
  - Na visualização `Servidores`, clique com o botão direito -> `Novo` -> `Servidor`.
  - Selecione `IBM` -> `IBM Bluemix` e siga as etapas do assistente.
  - Insira suas credenciais e clique em `Avançar`
  - Selecione sua `organização` e `espaço` e clique em `Concluir`

Execute seu aplicativo no {{site.data.keyword.Bluemix_notm}}:
  - Clique com o botão direito na amostra `GetStartedTomcat` e selecione a opção `Executar como` -> `Executar no servidor`.
  - Localize e selecione o `IBM Bluemix` e pressione Concluir.
  - Um assistente fornecerá instruções com as opções de implementação. Certifique-se de escolher um `Nome` exclusivo para seu aplicativo.
  - Em alguns minutos, seu aplicativo deverá estar em execução na URL escolhida.

Agora você executou seu código localmente e na nuvem!

## 7. Inclua um banco de dados
{: #add_database}

Em seguida, vamos incluir um banco de dados NoSQL nesse aplicativo e configurar o aplicativo para que ele possa ser executado localmente e no Bluemix.

1. Efetue login no {{site.data.keyword.Bluemix_notm}} em seu navegador. Procure o `Painel`. Selecione seu aplicativo clicando em seu nome na coluna `Nome`.
2. Clique em `Conexões` e, em seguida, em `Conectar novo`.
2. Na seção `Dados e Analytics`, selecione `Cloudant NoSQL DB` e `Criar` o serviço.
3. Selecione `Remontar` quando solicitado. O {{site.data.keyword.Bluemix_notm}} reiniciará o aplicativo e fornecerá as credenciais do banco de dados para ele usando a variável de ambiente `VCAP_SERVICES`. Essa variável de ambiente ficará disponível para o aplicativo somente quando ele estiver em execução no {{site.data.keyword.Bluemix_notm}}.

As variáveis de ambiente permitem separar as configurações de implementação do seu código-fonte. Por exemplo, em vez de codificar permanentemente uma senha do banco de dados, é possível armazená-la em uma variável de ambiente que seja referenciada em seu código-fonte. [Saiba mais...](/docs/manageapps/depapps.html#app_env)
{: tip}

## 8. Use o banco de dados
{: #use_database}
Vamos agora atualizar seu código local para apontar para esse banco de dados. Vamos armazenar as credenciais dos serviços em um arquivo de propriedades. Esse arquivo será usado SOMENTE quando o aplicativo estiver sendo executado localmente. Ao executar no {{site.data.keyword.Bluemix_notm}}, as credenciais serão lidas por meio da variável de ambiente VCAP_SERVICES.

1. Abra o Eclipse e o arquivo src/main/resources/cloudant.properties:
  ```
  cloudant_url=
  ```
  {: pre}

2. Em seu navegador, abra a UI do {{site.data.keyword.Bluemix_notm}}, selecione seu App -> Conexões -> Cloudant -> Visualizar credenciais

3. Copie e cole apenas a `URL` das credenciais no campo `URL` do arquivo `cloudant.properties` e salve as mudanças. O resultado será algo como:
  ```
  cloudant_url=https://123456789 ... bluemix.cloudant.com
  ```

4. Reinicie o servidor Tomcat no Eclipse por meio da visualização `Servidores`.

  Atualize a visualização do navegador em: http://localhost:8080/GetStartedTomcat/. Os nomes que você inserir no app serão agora incluídos no banco de dados.

  Seu app local e o app {{site.data.keyword.Bluemix_notm}} estão compartilhando o banco de dados. Visualize o app {{site.data.keyword.Bluemix_notm}} na URL listada na saída do comando push acima. Os nomes que você incluir de qualquer um dos apps deverão aparecer em ambos quando os navegadores forem atualizados.

Lembre-se, se você não precisar do app em tempo real no {{site.data.keyword.Bluemix_notm}}, pare-o para não incorrer em encargos inesperados.
{: tip}  
