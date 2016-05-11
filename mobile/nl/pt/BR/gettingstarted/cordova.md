---

copyright:
  years: 2015, 2016

---
<!-- Attribute definitions -->
{:codeblock: .codeblock}

# Introdução à amostra de HelloWorld
{: #gettingstarted-cordova}
*Última atualização: 17 de março de 2016*

Se desejar iniciar com um novo aplicativo Cordova, é possível usar o app HelloWorld. Este aplicativo demonstra como conectar seu backend móvel ao {{site.data.keyword.Bluemix}} usando um aplicativo móvel sem autenticação. O app já possui o SDK instalado. Quando você estiver pronto, poderá obter as bibliotecas específicas que deseja usar em seu app.

1. Crie seu backend móvel em {{site.data.keyword.Bluemix_notm}}.

	1. Na seção Modelos do catálogo do {{site.data.keyword.Bluemix_notm}}, clique em MobileFirst Services Starter.
	1. Insira um nome e um host para seu app e clique em **Criar**.
	1. Clique em **Concluir**.

2. Obtenha o projeto a partir do GitHub. É possível usar o comando de clonar git para obter o projeto. Em seu
computador, abra o terminal e, em seguida, insira o comando a seguir:

	```Bash
	git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloworld
	```

3. Execute os seguintes comandos usando o diretório do projeto para incluir os ambientes de plataforma Android e iOS:

	### Android

	```Bash
	cordova platform add android
	```

	### iOS

	```Bash
	cordova platform add ios
	```

4. Inclua o plug-in Cordova com o seguinte comando:

	```Bash
	cordova plugin add ibm-mfp-core
	```

5. Configure a amostra HelloWorld.

	* Mude para o diretório no qual você clonou o projeto.
	* Abra o arquivo *&lt;your_app_dir&gt;*/www/js/index.js e substitua *&lt;APPLICATION_ROUTE&gt;* e *&lt;APPLICATION_ID&gt;* pelo ID do aplicativo Bluemix e valores de rota.

		**Observação:** assegure-se de que a rota esteja protegida usando o protocolo https.

		```Javascript
		// Bluemix credentials
		route: "<APPLICATION_ROUTE>",
		GUID: "<APPLICATION_GUID>",
		```

6. Configure o aplicativo Cordova para iOS. A plataforma Android não requer configuração adicional.

	### iOS
  Configure seu projeto Xcode da seguinte maneira para evitar erros de compilação.

	1. Use a versão mais recente do Xcode para abrir o arquivo `xcode.proj` no diretório *&lt;app_name&gt;*/platforms/ios.

		**Importante:** se você receber uma mensagem para "Converter para a sintaxe Swift mais recente", clique em **Cancelar**.

	2. Acesse **Configurações de Compilação > Compilador Swift - Geração de Códigos > Cabeçalho de Ponte do Objective-C** e inclua o seguinte caminho:

		```
		<your_project_name>/Plugins/ibm-mfp-core/Bridging-Header.h
		```

	3. Acesse **Configurações de Compilação > Vinculação > Caminhos da Procura Runpath** e inclua o seguinte parâmetro do Frameworks:

		```
		@executable_path/Frameworks
		```

7. Construa e execute a amostra no seu emulador móvel ou dispositivo.

  ### Android
	1. Construa o aplicativo Cordova usando o seguinte comando:

    **Importante:** antes de abrir o projeto no Android Studio, deve-se primeiro construir o aplicativo
Cordova através da interface da linha de comando (CLI) do Cordova. Caso contrário, erros de construção serão encontrados.

	```Bash
	cordova build android
	```

	2. Execute o aplicativo de amostra no Android Studio.

  ### iOS
  1. Construa o aplicativo Cordova em Xcode.

    **Dica:** a construção em Xcode oferece mais opções, como depuração e configuração do projeto.

  2. Execute o aplicativo de amostra no Xcode.

Um aplicativo de visualização única com um botão **PING BLUEMIX** é exibido. Quando você toca no botão, o aplicativo testa a conexão do cliente ao aplicativo de backend {{site.data.keyword.Bluemix_notm}}. A conexão é testada usando a rota do aplicativo especificada no arquivo `index.js`.


![Aplicativo Hello World conectado com êxito ao Bluemix](images/yayconnected.jpg "Figura 1. Aplicativo Hello World conectado com êxito ao Bluemix")


Ao conectar-se com sucesso ao {{site.data.keyword.Bluemix_notm}} usando o aplicativo móvel, uma mensagem dizendo "Eba! Você está conectado" é exibida.


<!--![Hello World application not connected to Bluemix](images/bummer_android.jpg "Figure 2. Hello World application not connected to Bluemix")-->

Se a conexão falhar, uma mensagem de erro será exibida. Mais informações sobre o erro estão incluídas na mensagem. É possível verificar os seguintes itens para solucionar seu erro:

- Verifique se você colou corretamente os valores de
rota e GUID.
- Visualize o log de depuração do Xcode ou do Android.
- Verifique o status do seu aplicativo no {{site.data.keyword.Bluemix_notm}}.

## Próximas etapas:
{: #next}
Para obter informações sobre como obter o SDK e integrá-lo ao seu aplicativo móvel, veja:
* [Mobile Client Access: configurando o plug-in do Cordova](../../services/mobileaccess/getting-started-cordova.html)
* [Push Notifications: configurando o plug-in do Cordova](../../services/mobilepush/enablepush_cordova.html#setup_sdk_cordova)

# rellinks

## exemplos
   * [HelloWorld (Cordova)](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloworld)

## sdk
   * [bms-clientsdk-cordova-core](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

<!--## api
   * [Core API](https://classicdocs.{DomainName}/docs/api/content/api/mobilefirst/cordova/core-api-doc/overview-summary.html)
-->
