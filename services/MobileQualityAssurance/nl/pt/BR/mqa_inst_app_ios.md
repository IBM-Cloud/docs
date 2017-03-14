---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Instrumentando o MQA com um app iOS (descontinuado)
{: #instrumentios}

Para usar o {{site.data.keyword.mqafull}} com seu app iOS, deve-se fazer download do SDK e instrumentá-lo fazendo algumas mudanças usando o ambiente de desenvolvimento do Xcode.
{: shortdesc}

Para poder instrumentar um app com o {{site.data.keyword.mqa}}, deve-se ter uma conta do {{site.data.keyword.Bluemix}} e a versão corretamente instalada do ambiente de desenvolvimento para as plataformas do app que você está instrumentando.

Para instrumentar o {{site.data.keyword.mqa}} para funcionar com seu app Objective-C ou Swift, conclua as tarefas a seguir:

1. Inclua as permissões requeridas e o SDK transferido por download no seu projeto do iOS.

	1. Crie ou abra seu projeto no Xcode.

	2. Inclua as Bibliotecas de dependências a seguir selecionando `+` na seção *Estruturas e bibliotecas vinculadas* da guia *Geral* do seu projeto Xcode:

		* AssetsLibrary.framework
		* AudioToolbox.framework
		* AVFoundation.framework
		* CoreData.framework
		* CoreLocation.framework
		* CoreMedia.framework
		* CoreMotion.framework
		* CoreTelephony.framework
		* CoreText.framework
		* CoreVideo.framework
		* MediaPlayer.framework
		* QuartzCore.framework
		* Security.framework
		* SystemConfiguration.framework

	3. Arraste o SDK do {{site.data.keyword.mqa}} para a pasta `Q4M.framework` do iOS no grupo **Estruturas** da árvore do navegador. Na janela Escolher opções, selecione *Copiar itens se necessário*, **Criar grupos** e marque a caixa para o nome do seu projeto como destino.

	4. Na seção Link da guia *Configurações de construção*, configure *Outras sinalizações do vinculador* como **-ObjC** para Depurar e Liberar. Importante: Certifique-se de que a guia *Todos* seja selecionada para que Outras sinalizações do vinculador sejam incluídas na lista.

	5. *Somente para Objective-C:* Inclua a instrução de importação a seguir nos arquivos `AppDelegate.m` e `ViewController.m`:

		```
		#import <Q4M/MQALogger.h>
		```
		{: codeblock}

	6. *Somente para Swift:* Inclua um cabeçalho de ponte Objective-C para o {{site.data.keyword.mqa}} SDK for iOS concluindo as etapas a seguir:

		1. Clique com o botão direito do mouse no nó raiz do projeto e selecione **Novo arquivo**.

		2. Na janela Escolher modelo no iOS, clique no modelo Arquivo de cabeçalho na seção Origem.

		3. Nomeie o arquivo `MyProject-Bridging-Header.h`, em que *MyProject* é o nome do seu projeto Swift, e selecione o nome do seu projeto como destino. Por exemplo, nomeie o arquivo `MyProject-Bridging-Header.h`.

		4. Clique em **Criar** para salvar o arquivo na raiz de seu projeto.

		5. No novo arquivo de cabeçalho de ponte, inclua a instrução de importação a seguir para o arquivo de cabeçalho de ponte:

			```
			#import <Q4M/MQALogger.h>
			```
			{: codeblock}

		6. Com seu projeto selecionado no Xcode Project Navigator, clique em
**Configurações de construção** e procure `Objective-C Bridging Header`.

		7. Em **Compilador Swift - Geral**, configure o valor de **Cabeçalho de ponte Objective-C** como o caminho para o cabeçalho de ponte. O caminho é relativo à raiz de seu projeto. Por exemplo, se o projeto MQASampleApp estiver em `/user/example/MQASampleApp`, o caminho será `/user/example/MQASampleApp/MQASampleApp-Bridging-Header.h`. Se você salvou seu arquivo na raiz do projeto, será possível usar a variável de ambiente para configurar o caminho inserindo `${SRCROOT}/${PROJECT}-Bridging-Header.h`.

		8. Salve e construa o app para verificar se o caminho está correto.

	7. No arquivo `info.plist`, verifique as configurações a seguir nas informações do seu projeto:

		* Versão do pacote configurável - o {{site.data.keyword.mqa}} usa o valor desse campo para determinar quando enviar uma nova notificação de construção aos testadores. Quando você fizer upload de uma nova construção para o {{site.data.keyword.mqa}}, assegure-se de incrementar esse número. A sequência no campo Versão do pacote configurável é restrita a números e ao caractere de ponto (.). Como essa restrição é um requisito do Xcode, a maioria dos aplicativos segue essa convenção e não requer mudanças.
		* Sequência de versões de pacote configurável - esse campo contém uma representação de sequência do número da versão. A sequência não tem as mesmas restrições que o campo Versão do pacote configurável.

2. Configure uma nova sessão para ser iniciada com cada login.

    1. Localize o método `didFinishLaunchingWithOptions` no arquivo `AppDelegate`:

        * Objective-C: arquivo `AppDelegate.m`
        * Swift: arquivo `AppDelegate.swift`

	2. Inicie a sessão do {{site.data.keyword.mqa}}.

		* Objective-C

			1. Inicie a nova sessão em um método dentro do método `applicationDelegate`, como `didFinishLaunchingWithOptions`. É possível localizar seu delegado abrindo a pasta com o mesmo nome de seu projeto no Project Navigator. Verifique o arquivo `projectDelegate.m`.

			2. Inclua o código a seguir dentro do método `didFinishLaunchingWithOptions` antes da linha com `return YES;`:

				```
				// Starts a quality assurance session using a
				    placeholder key and QA mode
				[MQALogger startNewSessionWithApplicationKey:@"Your_Application_Key"];
				```
				{: codeblock}

			3. Substitua a variável *Your_Application_Key* pela chave do aplicativo do {{site.data.keyword.mqa}}.
               Dica: é possível localizar a chave do app na área de janela da web do {{site.data.keyword.mqa}} em Configurações de app.

		* Swift

			1. Localize o método `didFinishLaunchingWithOptions` no arquivo `AppDelegate.swift`.

			2. Inclua o código a seguir dentro do método antes da linha que lê `return true`, em que *Your_Application_Key* é uma chave válida para seu app:

				```
				// Set the application key
				MQALogger.startNewSession(withApplicationKey: "Your_Application_Key")
				```
				{: codeblock}

	3. Defina se deseja usar o modo de pré-produção ou de produção. Para obter informações sobre as diferenças entre os modos de pré-produção e produção, consulte [Diferenças entre os modos de pré-produção e produção ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/cPreprodvsProd.html){: new_window} no IBM Knowledge Center.

		* Objective-C

			1. Localize o método `didFinishLaunchingWithOptions`.

			2. Inclua uma das linhas de código a seguir dentro do método didFinishLaunchingWithOptions antes da linha com `return YES;`:

			Para usar o modo de pré-produção, inclua esta linha de código:

				```
				[[MQALogger settings] setMode:MQAModeQA];
				```
				{: codeblock}

			Para usar o modo de produção, inclua esta linha de código:

				```
				[[MQALogger settings] setMode:MQAModeMarket];
				```
				{: codeblock}

				**Exemplo completo de Objective-C**
				<pre><code>
					- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
						{
					   // Substitua o ponto de customização após a ativação do aplicativo.
					   if ([[UIDevice currentDevice] userInterfaceIdiom] == UIUserInterfaceIdiomPad) {
					      UISplitViewController *splitViewController = (UISplitViewController*)self.window.rootViewController;
					      UINavigationController *navigationController = [splitViewController.viewControllers lastObject];
					      splitViewController.delegate = (id)navigationController.topViewController;
						}
					     #ifdef Debug
					   [[MQALogger settings] setMode:MQAModeQA];
					   #else
					   [[MQALogger settings] setMode:MQAModeMarket];
					   #endif
					      // Starts a quality assurance session using a placeholder key
					      [MQALogger startNewSessionWithApplicationKey:@"Your-Application-Key"];
					      // Enables the quality assurance application crash reporting
					      NSSetUncaughtExceptionHandler(&MQAUncaughtExceptionHandler);
					      return YES; }
				</code></pre>
				{: codeblock}

        * Swift

			1. No arquivo AppDelegate.swift, procure o método `didFinishLaunchingWithOptions`.

			2. Inclua as linhas a seguir no método `didFinishLaunchingWithOptions` antes da linha que lê `return true`:

				```
				//Set the SDK mode Market vs QA for Production
				   and Pre-Production
				#if Debug
				  MQALogger.settings().mode = MQAMode.QA
				#elseif Release
				  MQALogger.settings().mode = MQAMode.Market
				#endif
				```
				{: codeblock}

			Este é um exemplo do código:

				```
				func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

				//Set the SDK mode Market vs QA for Production
				   and Pre-Production
				#if Debug
					MQALogger.settings().mode = MQAMode.QA
				#elseif Release
					MQALogger.settings().mode = MQAMode.Market
				#endif

				// Set the application key
				MQALogger.startNewSession(withApplicationKey: "Your_Application_Key")

				// Substitua o ponto de customização após a ativação do aplicativo.
				return true
				```
				{: codeblock}

				**Exemplo completo de Swift**
				<pre><code>				
				func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions:[NSObject: AnyObject]?) -> Bool {
					// Substitua o ponto de customização após a ativação do aplicativo.
					//Set the Shake Device option to true or false. If this is not explicitly set, the Shake Device is enabled by default.
					MQALogger.settings().reportOnShakeEnabled = true
					//Set the SDK mode Market vs QA for Production and Pre-Production
					#if Debug
					MQALogger.settings().mode = MQAMode.QA
					#elseif Release
					MQALogger.settings().mode = MQAMode.Market
					#endif

				//Start the MQA session with the specified app key
					   MQALogger.startNewSession(withApplicationKey: "Your_Application_Key")
				// Enables MQA crash reporting to catch uncaught exceptions
					   NSSetUncaughtExceptionHandler(exceptionHandlerPointer);

					   return true
					}
				</code></pre>
				{: codeblock}

3. Execute seu app para assegurar que {{site.data.keyword.mqa}} seja iniciado quando o app for iniciado.

4. Continue com as etapas na página [Introdução ao {{site.data.keyword.mqa}}](index.html).

# Links relacionados
{: #rellinks notoc}

## Links relacionados
{: #general notoc}
* [Introdução ao {{site.data.keyword.mqa}}](index.html){:new_window}
