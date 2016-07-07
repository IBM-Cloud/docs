---

copyright:
  years: 2015-2016

---

<!-- Attribute definitions -->
{:codeblock: .codeblock}

# Introdução à amostra Hello Bluemix for Android
{: #gettingstarted-android}
*Última atualização: 27 de maio de 2016*
{: .last-updated}  

Se desejar iniciar com um novo aplicativo Android, é possível usar o app HelloWorld. Esse app demonstra como se conectar ao backend do {{site.data.keyword.Bluemix}} a partir de um app móvel sem autenticação. O app já possui o SDK instalado. Quando você estiver pronto, poderá obter as bibliotecas específicas que deseja usar em seu app.

1. Crie seu backend móvel em {{site.data.keyword.Bluemix_notm}}.
    1. Na seção Modelos do catálogo do {{site.data.keyword.Bluemix_notm}}, clique em MobileFirst Services Starter.
    2. Insira um nome e um host para seu app e clique em **Criar**.
    3. Clique em **Concluir**.
2. Obtenha o projeto a partir do GitHub. Opcionalmente, é possível usar o comando git clone para obter o projeto. Em seu
computador, abra o terminal e, em seguida, insira o comando a seguir:
    ```
    git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloworld.git
    ```

3. Inicialize o projeto substituindo &lt;APPLICATION_ROUTE&gt; e &lt;APPLICATION_ID&gt; pela rota e pelo GUID do aplicativo no bloco `try` na função `BMSClient.getInstance().initialize()`:
```
// inicializar o SDK com o ID e a rota do aplicativo IBM Bluemix
BMSClient.getInstance().initialize(this, "<APPLICATION_ROUTE>", "<APPLICATION_ID>");
```
4. Execute a amostra em seu ambiente de desenvolvimento.
Na barra de ferramentas do Android Studio, clique no botão **Executar** e selecione um simulador.
5. No simulador, clique em **Executar ping no
                {{site.data.keyword.Bluemix_notm}}**. O app de amostra envia uma solicitação Get para o tempo de execução de `Node.js` no {{site.data.keyword.Bluemix_notm}}. Se a
solicitação for bem-sucedida, a conexão será verificada e o texto no
simulador será atualizado.

  **Nota:** o código de tempo de execução de `Node.js` é fornecido no modelo MobileFirst Services Starter. 
Se o aplicativo backend não tiver sido criado com o modelo do
MobileFirst Services Starter, o aplicativo não será conectado com
êxito.

  Quando você se conectar com sucesso ao {{site.data.keyword.Bluemix_notm}} a partir do app móvel no Android Studio, a mensagem a seguir será exibida:

  `Oba! você está conectado`
  {: screen}

  ![Aplicativo Hello World conectado com sucesso ao {{site.data.keyword.Bluemix_notm}}](images/yayconnected.jpg "Figura 1. Aplicativo Hello World conectado com sucesso ao Bluemix")

  Se a conexão falhar, você verá:
  `Que pena. Algo saiu errado`
  {: screen}

  ![Aplicativo Hello World não conectado ao Bluemix](images/bummer_android.jpg "Figura 2. Aplicativo Hello World não conectado ao Bluemix")

  É possível solucionar problemas da falha de conexão da
maneira a
seguir:
   * Verifique se você colou corretamente os valores de
rota e GUID.
   * Revise o log de depuração para obter mais informações.


## Próximas etapas:
{: #next}
Para obter informações sobre como obter o SDK e o integrar ao app móvel, consulte as informações sobre como configurar os serviços Bluemix.
   * [Mobile Client Access](../../services/mobileaccess/index.html)
   * [Enviar por push](../../services/mobilepush/index.html)

# rellinks

## exemplos
   * [Amostra de Hello Bluemix](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloworld)

## sdk
   * [SDK principal](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)

## interface de programação de aplicativos
   * [API do Núcleo](https://www.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)
