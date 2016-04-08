---

copyright:
  years: 2015,2016

---

{:new_window: target=_"blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Introdução ao
{{site.data.keyword.iotrtinsights_full}}
{: #gettingstartedtemplate}
*Última atualização: 11 de fevereiro de 2016*

Com o {{site.data.keyword.iotrtinsights_full}} no Bluemix ({{site.data.keyword.iotrtinsights_short}}), é possível executar a análise em dados em tempo real a partir de seus dispositivos Internet of Things e obter insights sobre seu funcionamento e o estado geral de suas operações.
{:shortdesc}

Para que seja possível começar a usar o {{site.data.keyword.iotrtinsights_short}}, deve-se configurar o serviço {{site.data.keyword.iot_full}} ({{site.data.keyword.iot_short}}) para conectar o mecanismo de análise aos dispositivos. É possível usar um serviço {{site.data.keyword.iot_short}} existente ou criar um novo. Para tê-lo funcionando rapidamente, é possível implementar o aplicativo de telefone Internet of Things e seu serviço {{site.data.keyword.iot_short}} associado em sua organização.

Para ter esse serviço funcionando rapidamente, siga estas etapas:
1. Implemente o serviço {{site.data.keyword.iotrtinsights_short}} em sua organização do Bluemix.
  1. No painel de conta do Bluemix, clique em **Usar serviço ou APIs**.
  2. Localize a seção Internet of Things do catálogo de serviços e selecione **{{site.data.keyword.iotrtinsights_short}}**.
  3. Na página {{site.data.keyword.iotrtinsights_short}}, verifique as seleções de Incluir serviço:  
    - Espaço - Verifique se você está implementando o serviço no mesmo espaço que implementou o serviço {{site.data.keyword.iot_short}}.
    - App - Deixe desvinculado.
    - Nome do serviço – Opcionalmente, mude o nome do serviço para algo que seja fácil de lembrar. Esse nome é exibido no tile IoT {{site.data.keyword.iotrtinsights_short}} no painel do Bluemix.
    - Plano selecionado - Selecione Grátis ou um plano de compra que seja adequado para as suas necessidades.  
    > **Importante:** Com o plano grátis do {{site.data.keyword.iotrtinsights_short}}, é possível implementar somente uma instância do serviço por organização.
  4. Clique em **Usar** para implementar o {{site.data.keyword.iotrtinsights_short}} nos serviços do Bluemix.
2. Opcional: use seu telefone como um dispositivo IoT com o IoT {{site.data.keyword.iotrtinsights_short}}.
Use o aplicativo de telefone Internet of Things para configurar rapidamente seu smartphone para agir como um dispositivo IoT que pode ser usado para verificar o ambiente do {{site.data.keyword.iotrtinsights_short}} e comece a definir a análise em tempo real nos dados. Para obter mais informações sobre o aplicativo de telefone Internet of Things, veja o projeto [Aplicativo de telefone Internet of Things](https://github.com/ibm-messaging/IoT-html5-phone).

  Para criar o aplicativo e conectar seu telefone ao {{site.data.keyword.iot_full}}: 
  1. Clique no botão abaixo para iniciar o processo de implementação:
  [![ícone Implementar no Bluemix.](https://bluemix.net/deploy?repository=https://github.com/ibm-messaging/iot-html5-phone "Implementar o telefone do IoT no Bluemix")(images/deploy_to_bluemix.png "ícone Implementar no Bluemix")]  
  > **Nota:** a implementação do aplicativo de telefone Internet of Things também implementa um serviço {{site.data.keyword.iot_short}} (*iot-phone-iotf-service*) que é ligado automaticamente ao aplicativo de telefone. Inclua esse {{site.data.keyword.iot_short}} como uma origem de dados para testar o aplicativo de telefone Internet of Things. Ele também cria um serviço Cloudant NoSQL DB (*iot-phone-cloudant-cloudantNoSQLDB*) que é usado pelo aplicativo.

  2. Clique em **Aprovar** se você for solicitado a autoaprovar o acesso para o IBM Single Sign On Service (consentimento do OAuth).   
  >**Dica:** se você não tiver uma conta do Bluemix, será possível se inscrever para ativar sua avaliação grátis do Bluemix. 
  2. Mude o campo APP NAME para algo fácil de lembrar, nós chamaremos de *aplicativo de telefone* em todo o restante destas instruções. Esse nome será exibido em um tile do aplicativo no painel do Bluemix e fará parte da URL que você usará quando conectar seu telefone ao {{site.data.keyword.iot_short}}.
  2. Clique em **Implementar**.
  2. Depois que o processo de implementação estiver concluído, você verá uma mensagem 'Sucesso'; retorne ao painel do Bluemix.
  O tile do *aplicativo de telefone* e o tile *iot-phone-iotf-service* serão incluídos em sua conta.
  1. No painel do Bluemix, clique no tile do *aplicativo de telefone*.
  2. Em seu telefone, abra um navegador e acesse a URL Rotas que é exibida sob o nome do aplicativo. Quando solicitado, insira um ID do dispositivo de sua escolha para identificar o telefone como um dispositivo nos painéis {{site.data.keyword.iot_short}} e IoT {{site.data.keyword.iotrtinsights_short}}. 
  3. Clique em **Conectar** para conectar o telefone ao {{site.data.keyword.iot_short}} *iot-phone-iotf-service*.
  A visualização é atualizada para exibir os dados que são enviados a partir de seu telefone para o {{site.data.keyword.iot_short}}. 
2. Crie e configure um serviço Internet of Things.   
> **Dica:** se você implementou o aplicativo de telefone Internet of Things, o *iot-visualization-phone-iotf-service* já estará criado e será possível ignorar esta etapa.   

  1. Efetue login na organização do Bluemix e selecione o espaço no qual você deseja implementar o IoT {{site.data.keyword.iotrtinsights_short}}. 
  2. No Painel do Bluemix, clique em **Usar serviço ou APIs**.
  3. Localize a seção Internet of Things do catálogo de serviços e selecione **Internet of Things**. 
  4. Na página {{site.data.keyword.iot_full}}, verifique as seleções de Incluir serviço e clique em **Usar** para incluir o {{site.data.keyword.iot_short}} nos serviços do Bluemix.
  Após o serviço {{site.data.keyword.iot_short}} ser implementado, você será levado para a página de gerenciamento de serviço. 
3. Localize as chaves da API de conexão.
Se você criou um novo serviço {{site.data.keyword.iot_short}}, agora deve-se criar as chaves de API para conectar os dois serviços. Se você estiver usando um serviço existente, será possível usar as chaves existentes.   
  1. No painel do Bluemix, clique no tile Internet of Things.   
  >**Nota:** se você estiver usando o aplicativo de telefone Internet of Things, clique no tile *iot-phone-iotf-service*.  

  1. Clique em **Ativar painel** para abrir o painel do {{site.data.keyword.iot_full}}.
  2. Navegue para **Acessar > Chaves de API**.
  3. Clique em **Gerar chave de API**.
  3. Anote a Chave de API, o Token de autenticação e o ID da organização que são exibidos na parte superior do painel do {{site.data.keyword.iot_short}}.
  Você usa essas informações no IoT {{site.data.keyword.iotrtinsights_short}} para conectar os serviços.
4. Conecte seu serviço {{site.data.keyword.iot_short}} e o serviço IoT {{site.data.keyword.iotrtinsights_short}}.
  1. No painel do Bluemix, clique no tile IoT {{site.data.keyword.iotrtinsights_short}}.  
  2. Na página de serviço, clique em **Incluir uma origem de dados**.
  2. Na página Gerenciar origens de dados do console do {{site.data.keyword.iotrtinsights_short}}, clique em **Incluir nova origem de dados**.
  3. Forneça à origem de dados um nome descritivo e forneça as informações a seguir que você coletou anteriormente: 
    - ID da Organização
    - Chave de API
    - Token de Autenticação
  4. Clique em ![ícone Criar](images/create.png "ícone Criar") para criar a origem de dados e conectar-se a ela. 
4. Comece a usar o {{site.data.keyword.iotrtinsights_short}}.
Agora é possível começar a usar o {{site.data.keyword.iotrtinsights_short}} incluindo usuários, conectando dispositivos, configurando painéis para visualizar dados relevantes do dispositivo e configurando alertas.
>**Selecionando sua instância do {{site.data.keyword.iotrtinsights_short}}:** se você recebeu acesso para quaisquer instâncias do {{site.data.keyword.iotrtinsights_short}} como um operador ou administrador, será possível alternar rapidamente entre essas instâncias. No console do {{site.data.keyword.iotrtinsights_short}}, clique em seu nome de usuário e selecione a instância que você deseja acessar.   

# rellinks
## amostras
* [Aplicativo de telefone Internet of Things](https://github.com/ibm-messaging/IoT-html5-phone)
* [Receitas de Internet of Things do developerWorks](https://developer.ibm.com/recipes/)
* [Criando apps com o aplicativo iniciador do Internet of Things](https://www.ng.bluemix.net/docs/starters/IoT/iot500.html#iot500)

## interface de programação de aplicativos
* [Documentação da API](https://iotrti-prod.mam.ibmserviceengage.com/apidoc/)

## geral
* [Sobre](iotrtinsights_overview.html)   
* [O que há de novo em Serviços do Bluemix](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category)
* [Introdução ao {{site.data.keyword.iot_full}}](https://www.ng.bluemix.net/docs/services/IoT/index.html)
* [dW Answers no IBM developerWorks](https://developer.ibm.com/answers/topics/iot-real-time/)
