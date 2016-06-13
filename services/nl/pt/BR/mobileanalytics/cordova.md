<!-- Attribute definitions -->
{:codeblock: .codeblock}

# Introdução à amostra de HelloWorld
{: #gettingstarted-cordova}

Se desejar iniciar com um novo aplicativo Cordova, é possível usar o aplicativo HelloWorld. Esse aplicativo demonstra como se conectar ao backend do Bluemix a partir de um aplicativo móvel sem autenticação. O aplicativo já possui o SDK instalado. Quando você estiver pronto, poderá obter as bibliotecas específicas que deseja usar em seu aplicativo.

1. Crie seu backend móvel no Bluemix.
<ol>
	<li>Na seção Modelos do catálogo do Bluemix, clique em MobileFirst Services Starter.</li>
    	<li>Insira um nome e um host para seu aplicativo e clique em **Criar**.</li>
    	<li>Clique em **Concluir (Finish)**. </li>
</ol>
2. Obtenha o projeto a partir do GitHub. Opcionalmente, é possível usar o comando git clone para obter o projeto. Em seu
computador, abra o terminal e, em seguida, insira o comando a seguir:
```
git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloworld
```

3. Execute os seguintes comandos usando o diretório do projeto para incluir os ambientes de plataforma Android e iOS:

Android:
```
cordova platform add android
```

iOS:
```
cordova platform add ios
```

4. Inclua o plug-in Cordova com o seguinte comando:
```
cordova plugin add ibm-mfp-core
```

5. Configure o aplicativo Cordova para Android, iOS ou ambos.

 * Android

	 Antes de abrir o projeto no Android Studio, compile e execute o aplicativo Cordova usando a interface da linha de comandos (CLI) para evitar erros de compilação.

	 ```
	 cordova build android
	 ```

	 ```
	 cordova run android
	 ```

 * iOS

	 Configure seu projeto Xcode da seguinte maneira para evitar erros de compilação.

	    1. Use a versão mais recente do Xcode para abrir o arquivo xcode.proj no
diretório &lt;app_name&gt;/platforms/ios.

			**Importante:** se você receber uma mensagem para "Converter na sintaxe mais recente do Swift", clique em Cancelar.

		2. Acesse **Configurações de Compilação > Compilador Swift - Geração de Códigos > Cabeçalho de Ponte do Objective-C** e inclua o seguinte caminho:

		```
		<your_project_name>/Plugins/ibm-mfp-core/Bridging-Header.h
		```
		3. Acesse **Configurações de Compilação > Vinculação > Caminhos da Procura Runpath** e inclua o seguinte parâmetro do Frameworks:

		```
		@executable_path/Frameworks
		```
		4. Compile e execute seu aplicativo com Xcode.

6. Configure a amostra HelloWorld
<ol>
	<li>Mude para o diretório no qual o projeto foi clonado</li>
	<li>Abra o arquivo &lt;your_app_dir&gt;/www/js/index.js e substitua &lt;APPLICATION_ROUTE&gt; e &lt;APPLICATION_ID&gt; pelo ID do aplicativo Bluemix e valores de rota.</li>
</ol>

Nota: certifique-se de que seu &lt;APPLICATION_ROUTE&gt; esteja usando seguramente o protocolo https.

```
// Bluemix credentials route: "<APPLICATION_ROUTE>", GUID: "<APPLICATION_GUID>",
```

7. Execute a amostra no seu emulador ou dispositivo móvel.

   Compile o aplicativo Cordova usando os seguintes comandos:
	 ```
	 cordova build ios
	 ```
	 ```
	 cordova build android
	 ```

   Execute o aplicativo de amostra usando os seguintes comandos:
	 ```
	 cordova run ios
	 ```
   ```
	 cordova run android
	 ```


Um aplicativo de visualização única com um botão **PING BLUEMIX** é exibido. Ao dar um toque no botão, o aplicativo testa a conexão do cliente para o aplicativo Bluemix de backend. A conexão é testada usando a Rota do aplicativo especificada no arquivo index.js.


![Aplicativo Hello World conectado com êxito ao Bluemix](images/yayconnected.jpg "Figura 1. Aplicativo Hello World conectado com êxito ao Bluemix")

Quando você se conecta com sucesso ao Bluemix a partir do aplicativo móvel, uma mensagem que diz "Oba! Você está conectado" é exibida.
8. Resolva quaisquer problemas.

<!--![Hello World application not connected to Bluemix](images/bummer_android.jpg "Figure 2. Hello World application not connected to Bluemix")-->

Se a conexão falhar, uma mensagem: "Puxa! Algo deu errado" será exibida. Mais informações sobre o erro são incluídas.
Verifique os seguintes itens:
 * Verifique se você colou corretamente os valores de
rota e GUID.
 * Visualize o log de depuração do Xcode ou do Android.
 * Verifique o status de seu aplicativo no Bluemix.

## Próximas etapas:
{: #next}
Para obter informações sobre como obter o SDK e integrá-lo ao seu aplicativo móvel, veja Configurando o SDK do cliente Cordova.

# rellinks

## samples
   * [HelloWorld (Cordova)](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloworld)

## sdk
   * [bms-clientsdk-cordova-core](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)

<!--## api
   * [Core API](https://www.{DomainName}/docs/api/content/api/mobilefirst/cordova/core-api-doc/overview-summary.html)
-->
