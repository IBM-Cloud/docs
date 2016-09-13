---

copyright:
 years: 2015, 2016

---

# Instalando o plug-in Push do Cordova
{: #cordova_install}

Instale e use o plug-in Push do cliente para
desenvolver ainda mais seus aplicativos Cordova. Isso
também instala o plug-in Núcleo do Cordova, que inicializa sua
conexão com o Bluemix.

### Antes de começar

1. Faça download das versões mais recentes do Android Studio SDK e Xcode.
1. Configure o emulador. Para Android Studio, use um emulador que suporte a API do Google.
1. Instale a ferramenta de linha de comandos Git. Para Windows, certifique-se de
selecionar a opção **Executar Git no prompt de comandos do Windows**. Para
obter informações sobre como fazer download e instalar essa ferramenta, consulte
[Git](https://git-scm.com/downloads).

1. Instale o Node.js e a ferramenta Node Package Manager (NPM). A ferramenta de
linha de comandos NPM é empacotada com o Node.js. Para obter informações sobre como fazer download e instalar o Node.js, consulte
[Node.js](https://nodejs.org/en/download/).
1. Na linha de comandos, instale as ferramentas de linha de comandos Cordova
usando o comando **npm install -g cordova**. Isso é
necessário para usar o plug-in Push do Cordova. Para obter informações sobre como
instalar o Cordova e configurar o app Cordova, consulte
[Cordova Apache](https://cordova.apache.org/#getstarted).

	**Nota**: Para visualizar o arquivo leia-me do plug-in Push do
Cordova, acesse [https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push)


## Instalando o plug-in Push do Cordova
1. Mude para a pasta na qual deseja criar seu app Cordova e
execute o comando a seguir para criar um aplicativo Cordova. Se
você tiver um app Cordova existente, vá para a etapa 3.


	cordova create your_app_name
	cd your_app_name
	```
1. Opcional: (Opcional) Edite o arquivo **config.xml** e mude o
nome do aplicativo no elemento <name> para um da sua escolha, em vez do nome
HelloCordova padrão.

	**Nota**: Certifique-se de especificar o ID do pacote
configurável correto. Se você não fizer isso, as mensagens de erro a seguir serão
exibidas no Xcode.
	* O executável foi assinado com autorizações inválidas.
	* As autorizações especificadas no arquivo de autorizações de assinatura de
código do aplicativo não correspondem às especificadas no seu perfil de fornecimento.

	Para corrigir esse problema, especifique o ID do pacote configurável correto no
Xcode ou no arquivo **config.xml** do seu app Cordova.

1. Inclua a API mínima suportada ou a declaração de destino de
implementação no arquivo config.xml do seu aplicativo Cordova. O valor minSdkVersion deve
ser maior que 15. O valor targetSdkVersion deve sempre refletir o SDK mais recente do
Android que esta disponível no Google.
	* **Android** - com seu editor, abra o arquivo config.xml e atualize o elemento
```<platform name="android">``` com as versões mínima e de destino do SDK:

	```
	<!-- add deployment target declaration -->
	<platform name="android">  
			  <preference name="android-minSdkVersion" value="15" />
			  <preference name="android-targetSdkVersion" value="23" />
			</platform>
	```
   * **iOS** - Atualize o elemento <platform name="ios">
com uma declaração de destino de implementação:

	```
	<platform name="ios">
	    <preference name="deployment-target" value="8.0" />
	    <!-- other properties -->
	</ platform>
	```

1. Na interface da linha de comandos (CLI) do Cordova, inclua suas plataformas: iOS,
Android, ou ambas, usando os comandos a seguir.

	```
	cordova platform add ios
	cordova platform add android
	```
1. No diretório raiz do aplicativo Cordova, insira o comando a seguir para
instalar o plug-in Push do Cordova: **cordova plugin add ibm-mfp-push**.

	Dependendo das plataformas incluídas, você vê algo semelhante ao
seguinte:

	```
	Installing "ibm-mfp-push" for android
	Installing "ibm-mfp-push" for ios
	```
1. Em *your-app-root-folder*, verifique se o plug-in Principal e Push
do Cordova foram instalados com sucesso usando o comando a seguir: **cordova plugin list**.

	Dependendo das plataformas incluídas, você vê algo semelhante ao
seguinte:

	```
	ibm-mfp-core 1.0.0 "MFPCore"
	ibm-mfp-push 1.0.0 “MFPPush"
	```
1. (Somente iOS) - Configure seu ambiente de desenvolvimento iOS.
	a. Abra o arquivo your-app-name.xcodeproj no diretório *your-app-name***/platforms/ios** com Xcode.

	b. Inclua o Cabeçalho de ponte. Acesse **Configurações de compilação >
Compilador Swift - Geração de código > Cabeçalho de ponte Objective-C** e inclua o
caminho a seguir: *your-project-name***/Plugins/ibm-mfp-core/Bridging-Header.h**

	c. Inclua o parâmetro Frameworks. Acesse **Configurações de compilação > Link > Caminhos da procura Runpath** e inclua o parâmetro a seguir:
	```
	@executable_path/Frameworks
	```
	d. Remova o comentário das instruções de importação Push a seguir em seu cabeçalho de ponte. Acesse *your-project-name***/Plugins/ibm-mfp-core/Bridging-Header.h**

	```
	//#import <IMFPush/IMFPush.h>
	//#import <IMFPush/IMFPushClient.h>
	//#import <IMFPush/IMFResponse+IMFPushCategory.h>
	```
	e. Compile e execute seu aplicativo com Xcode.
1. (Somente Android)- Compile seu projeto Android usando o comando a seguir:
**cordova build android**.

	**Nota**: Antes de abrir seu projeto no Android Studio,
deve-se primeiro compilar o aplicativo Cordova por meio da CLI do Cordova. Caso
contrário, você encontrará erros de compilação.

1. Próxima etapa. [Inicializando
o plug-in Cordova](t_cordova_initalize.html).
