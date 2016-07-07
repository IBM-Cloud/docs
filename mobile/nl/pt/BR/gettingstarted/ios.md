---

copyright:
  years: 2015-2016

---

<!-- Attribute definitions -->
{:codeblock: .codeblock}

# Introdução à amostra Hello Bluemix for iOS
{: #gettingstarted-android}
*Última atualização: 1 de junho de 2016*
{: .last-updated}  

Se desejar iniciar com um novo app iOS, é possível usar o app HelloWorld. Esse app demonstra como se conectar ao backend do {{site.data.keyword.Bluemix}} a partir de um app móvel sem autenticação. O app já possui o SDK instalado. Quando você estiver pronto, poderá obter as bibliotecas específicas que deseja usar em seu app.

1. Crie seu backend móvel em {{site.data.keyword.Bluemix_notm}}.
    1. Na seção Modelos do catálogo do {{site.data.keyword.Bluemix_notm}}, clique em MobileFirst Services Starter.
    2. Insira um nome e um host para seu app e clique em **Criar**.
    3. Clique em **Concluir**.
2. Obtenha o projeto a partir do GitHub. Opcionalmente, é possível usar o comando git clone para obter o projeto. Em seu
computador, abra o terminal e, em seguida, insira o comando a seguir:
    ```
    git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloworld.git
    ```

3. Inicialize o projeto. Para inicializar o SDK, copie o código a seguir para o método `didFinishLaunchingWithOptions` no Aplicativo delegado.

	###Ojbective-C
	{: initializeobjc}

	**Importante**: embora o Objective-C SDK permaneça totalmente suportado e ainda seja considerado o SDK primário para o {{site.data.keyword.Bluemix}} Mobile Services, ele está planejado para ser descontinuado posteriormente este ano em favor do novo Swift SDK.

	O Objective-C SDK relata dados de monitoramento para o Monitoring Console do serviço {{site.data.keyword.amashort}}. Se você depende das funções de monitoramento do serviço {{site.data.keyword.amashort}}, continue a usar o Objective-C SDK.

	```
	// inicializar o SDK com o ID e a rota do aplicativo IBM Bluemix
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:@"<insert route>" backendGUID:@"<insertGUID>"];
return YES;
	```

	###Swift
	{: initializeswift}
	```
	// inicializar o SDK com o ID e a rota do aplicativo IBM Bluemix
IMFClient.sharedInstance().initializeWithBackendRoute("<insert route>", backendGUID: "<insertGUID>")
return true
	```

4. Execute a amostra em seu ambiente de desenvolvimento. No Xcode, clique em **Produto&gt;Executar**. Um simulador do iOS é iniciado.
5. No simulador, clique em **Executar ping no
                {{site.data.keyword.Bluemix_notm}}**. O app de amostra obtém o cabeçalho de autorização a partir do serviço Mobile Client Access. Se o ping for bem-sucedido, o texto no simulador será atualizado.

  Quando você se conectar com sucesso ao {{site.data.keyword.Bluemix_notm}} a partir do app móvel em Xcode, a mensagem a seguir será exibida:

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
		####Objective-C
		{: #objcvals}
		```
		[imfClient initializeWithBackendRoute:@"https://hellotest.mybluemix.net"
  backendGUID:@"9d48d73a-0878-4254-test-bdcbe6c79c31"];
		```

		####Swift
		{: #swiftvals}
		```
		IMFClient.sharedInstance().initializeWithBackendRoute("https://hellotest.mybluemix.net", backendGUID: "9d48d73a-0878-4254-test-bdcbe6c79c31")
		```

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
