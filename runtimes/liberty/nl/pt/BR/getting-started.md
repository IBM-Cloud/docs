---

copyright:
  years: 2017
lastupdated: "2017-03-17"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# Introdução ao Liberty no Bluemix

* {: download} Parabéns, você implementou um aplicativo de amostra Hello World no {{site.data.keyword.Bluemix}}! Para iniciar, siga este guia passo a passo. Ou <a class="xref" href="http://bluemix.net" target="_blank" title="(Fazer download de código de amostra)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="Fazer download de código do aplicativo" />faça download do código de amostra</a> e explore você mesmo.

Seguindo esse guia, você configurará um ambiente de desenvolvimento, implementará um app localmente e no {{site.data.keyword.Bluemix}} e integrará um serviço de banco de dados do {{site.data.keyword.Bluemix}} em seu app.

## Pré-requisito
{: #prereqs}

Você precisará das contas e ferramentas a seguir:
* [Conta do {{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net/registration/)
* [Cloud Foundry CLI ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Eclipse IDE for Java EE Developers ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/neon2){: new_window}
* [Git ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://git-scm.com/downloads){: new_window}
* [Maven ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://maven.apache.org/download.cgi){: new_window}

Para desenvolver no Eclipse com o {{site.data.keyword.eclipsetoolsfull}}, também será necessário [fazer download das ferramentas. ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix){: new_window}

## 1. Clone o app de amostra
{: #clone}

Primeiro, clone o repositório GitHub do app de amostra.
  ```bash
git clone https://github.com/IBM-Bluemix/get-started-java
  ```
  {: pre}


## 2. Execute o app localmente usando a linha de comandos
{: #run_locally}

Use Maven para construir seu código-fonte e execute o app resultante.

1. Na linha de comandos, mude o diretório para onde o app de amostra está localizado.

  ```
cd get-started-java
  ```
  {: pre}

1. Use Maven para instalar as dependências e construir o arquivo .war.

  ```
mvn clean install
  ```
  {: pre}

1. Execute o app localmente no Liberty.
  ```
mvn install liberty:run-server
  ```
  {: pre}

Quando você vir a mensagem *O servidor defaultServer está pronto para executar um planeta mais inteligente*, visualize seu app em: http://localhost:9080/GetStartedJava.

Para parar o app, pressione *Ctrl-C* na mesma janela de linha de comandos em que o app foi iniciado.

## 3. Prepare o app para implementação
{: #prepare}

Para implementar no {{site.data.keyword.Bluemix_notm}}, poderá ser útil configurar um arquivo manifest.yml. O manifest.yml inclui informações básicas sobre seu app, como o nome, quanta memória alocar para cada instância e a rota. Nós fornecemos um arquivo manifest.yml de amostra no diretório `get-started-java`.

Abra o arquivo manifest.yml e mude o `nome` de `GetStartedJava` para o nome de seu app, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
  applications:
   - name: GetStartedJava
     random-route: true
     path: target/GetStartedJava.war
     memory: 512M
     instances: 1
  ```
  {: codeblock}

Nesse arquivo manifest.yml, **random-route: true** gera uma rota aleatória para seu app para evitar que sua rota colida com outras. Se você optar por isso, será possível substituir **random-route: true** por **host: myChosenHostName**, fornecendo um nome de host de sua preferência. [Saiba mais...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## 4. Implemente no {{site.data.keyword.Bluemix_notm}}
{: #deploy}

Implemente seu app em uma das regiões do Bluemix a seguir. Para obter uma latência ideal, escolha uma região mais próxima de seus usuários.

|Região          |Terminal de API                             |
|:---------------|:-------------------------------|
| SUL dos EUA       |https://api.ng.bluemix.net     |
| United Kingdom | https://api.eu-gb.bluemix.net  |
| Sydney         | https://api.au-syd.bluemix.net |

1. Configure o terminal de API substituindo `<API-endpoint>` pelo terminal de sua região.
  ```
cf api <API-endpoint>
  ```
  {: pre}

1. Efetue login em sua conta do {{site.data.keyword.Bluemix_notm}}.
  ```
cf login
  ```
  {: pre}

1. No diretório `get-started-java`, envie seu aplicativo por push para o {{site.data.keyword.Bluemix_notm}}.
  ```
cf push
  ```
  {: pre}

A implementação de seu aplicativo pode levar alguns minutos. Quando a implementação for concluída, você verá uma mensagem informando que o app está em execução. Visualize o app na URL listada na saída do comando push ou visualize o status de implementação do app e a URL, executando o comando a seguir:
  ```
cf apps
  ```
  {: pre}

É possível solucionar problemas de erros no processo de implementação usando o comando `cf logs <Your-App-Name> --recent`.
{: tip}  

## 5. Desenvolvendo usando o Eclipse
{: #eclipse}

O {{site.data.keyword.eclipsetoolsfull}} fornece plug-ins que podem ser instalados em um ambiente existente do Eclipse para ajudar na integração de seu ambiente de desenvolvimento integrado (IDE) com o {{site.data.keyword.Bluemix_notm}}.

1. Certifique-se de que tenha o [IBM Eclipse Tools for Bluemix](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix).

2. Importe a amostra `get-started-java` para o Eclipse acessando **Arquivo > Importar > Maven > Projetos existentes do Maven**.

3. Crie uma definição de servidor Liberty. As etapas a seguir farão download de um novo servidor Liberty.
  - Na visualização **Janela > Mostrar visualização > Servidores**, clique com o botão direito e selecione **Novo > Servidor**.
  - Selecione **IBM > WebSphere Application Server Liberty**.
  - Selecione **Instalar de um archive ou um repositório**.
  - Quando solicitado, insira um caminho de destino em uma nova pasta (/Users/username/liberty) na qual você deseja instalar o Liberty.
  - Selecione **Fazer download e instalar um novo ambiente de tempo de execução do ibm.com**.
  - Selecione **WAS Liberty com Java EE 7 Web Profile**.
  - Continue o assistente com opções padrão para concluir.

4. Execute seu aplicativo localmente no Liberty.
  - Mude o navegador da web para o padrão do sistema acessando **Janela > Navegador da web > navegador da web do sistema padrão**.
  - Clique com o botão direito na amostra `GetStartedJava` e selecione **Executar como > Executar no servidor**.
  - Localize e selecione o servidor Liberty localhost e clique em **Concluir**.

  Em alguns segundos, seu aplicativo estará em execução em http://localhost:9080/GetStartedJava.

5. Atualize o código:
  - Abra `src/main/webapp/index.html` e atualize o título de `<h1>Bem-vindo.</h1>` para `<h1>Bem-vindo Jane.</h1>`.
  - Salve suas mudanças. O Liberty assimilará suas mudanças automaticamente.
  - Atualize seu navegador (http://localhost:9080/GetStartedJava) para ver as mudanças.

6. Envie suas mudanças por push para o {{site.data.keyword.Bluemix_notm}}:
  - No diretório `get-started-java`, na linha de comandos, reconstrua o arquivo .war.
    ```
mvn clean install
    ```
    {: pre}
  - Envie seu aplicativo por push para {{site.data.keyword.Bluemix_notm}}.
    ```
cf push
    ```
    {: pre}

Agora você executou seu código localmente e na nuvem!

## 6. Inclua um banco de dados
{: #add_database}

Em seguida, vamos incluir um banco de dados NoSQL nesse aplicativo e configurar o aplicativo para que ele possa ser executado localmente e no {{site.data.keyword.Bluemix_notm}}.

1. Em seu navegador, efetue login no {{site.data.keyword.Bluemix_notm}} e acesse o Painel. Selecione seu aplicativo clicando em seu nome na coluna **Nome**.
2. Clique em **Conexões** e, em seguida, em **Conectar novo**.
3. Na seção **Dados e Analytics**, selecione **Cloudant NoSQL DB** e, em seguida, crie o serviço.
4. Selecione **Remontar** quando solicitado. O {{site.data.keyword.Bluemix_notm}} reiniciará o aplicativo e fornecerá as credenciais do banco de dados para ele usando a variável de ambiente `VCAP_SERVICES`. Essa variável de ambiente ficará disponível para o aplicativo somente quando ele estiver em execução no {{site.data.keyword.Bluemix_notm}}.

As variáveis de ambiente permitem separar as configurações de implementação do seu código-fonte. Por exemplo, em vez de codificar permanentemente uma senha do banco de dados, é possível armazená-la em uma variável de ambiente que seja referenciada em seu código-fonte. [Saiba mais...](/docs/manageapps/depapps.html#app_env)
{: tip}

## 7. Use o banco de dados
{: #use_database}
Vamos agora atualizar seu código local para apontar para esse banco de dados. Vamos armazenar as credenciais dos serviços em um arquivo de propriedades. Esse arquivo será usado SOMENTE quando o aplicativo estiver sendo executado localmente. Ao executar no {{site.data.keyword.Bluemix_notm}}, as credenciais serão lidas por meio da variável de ambiente `VCAP_SERVICES`.

1. No Eclipse, abra o arquivo src/main/resources/cloudant.properties:
  ```
  cloudant_url=
  ```
  {: pre}

2. Em seu navegador, acesse o {{site.data.keyword.Bluemix_notm}} e selecione **Aplicativos > _your app_ > Conexões > Cloudant > Visualizar credenciais**.

3. Copie e cole apenas a `URL` das credenciais no campo `URL` do arquivo `cloudant.properties` e salve as mudanças.
  ```
  cloudant_url=https://123456789 ... bluemix.cloudant.com
  ```
  {:pre}

4. Reinicie o servidor Liberty no Eclipse por meio da visualização `Servidores`.

  Atualize seu navegador em http://localhost:9080/GetStartedJava/. Os nomes que você inserir no app serão agora incluídos no banco de dados.

  Seu app local e o app {{site.data.keyword.Bluemix_notm}} estão compartilhando o banco de dados. Os nomes que você incluir de qualquer um dos apps aparecerão em ambos quando os navegadores forem atualizados.


Lembre-se, se você não precisar do app em tempo real no {{site.data.keyword.Bluemix_notm}}, pare-o para não incorrer em encargos inesperados.
{: tip}  
