---

copyright:
  years: 2015-2016

---

<!-- Attribute definitions -->
{:codeblock: .codeblock}

# Introdução à amostra Hello Bluemix for iOS
{: #gettingstarted-android}
Última atualização: 1º de junho de 2016
{: .last-updated}  

Se você desejar começar a usar um novo app iOS, poderá usar o app Hello Bluemix. Esse app demonstra como se conectar ao seu backend {{site.data.keyword.Bluemix}} por meio de um app móvel sem autenticação. Quando você estiver pronto, poderá obter as bibliotecas específicas que deseja usar em seu app.

1. Crie seu backend móvel em {{site.data.keyword.Bluemix_notm}}.
    1. Na seção Modelos do catálogo do {{site.data.keyword.Bluemix_notm}}, clique em MobileFirst Services Starter.
    2. Insira um nome e um host para seu app e clique em **Criar**.
    3. Clique em **Concluir**.
2. Execute o aplicativo de amostra Hello Bluemix:
	1. Obtenha o projeto a partir do GitHub. Opcionalmente, é possível usar o comando git clone para obter o projeto. Em seu computador, abra o terminal e, em seguida, insira o comando a seguir:
    ```
    git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-hellobluemix.git
    ```
	2. Execute o comando `pod install` a partir do diretório `bms-samples-swift-hellobluemix`, em que
o projeto foi clonado. Se você não tiver Cocoapods instalado, obtenha-o do [https://cocoapods.org](https://cocoapods.org).
	3. Abra a área de trabalho Xcode com o comando `open HelloBluemix.xcworkspace`.
	4. Em seu arquivo `AppDelegate.swift`, atualize os valores appRoute e appGuid para aqueles obtidos do backend Bluemix
que criou anteriormente.

3. Execute a amostra em seu ambiente de desenvolvimento. No Xcode, clique em **Produto&gt;Executar**. Um simulador do iOS é iniciado.

	**Importante:** seu appRoute deve usar um protocolo `https` e não `http` ou é
possível que obtenha uma falha, devido às configurações de segurança de transporte do aplicativo. É possível ler mais sobre essas configurações
na postagem do blog [Connect your iOS 9 app to Bluemix today](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/).
	
4. No simulador, clique em **Executar ping no
                {{site.data.keyword.Bluemix_notm}}**. O app de amostra obtém o cabeçalho de autorização a partir do serviço Mobile Client Access. Se o ping for bem-sucedido, o texto no simulador será atualizado.

  Quando você se conectar com sucesso ao {{site.data.keyword.Bluemix_notm}} a partir do aplicativo móvel no Xcode, verá:
  `Oba! você está conectado`
  {: screen}

  <!--
  ![Hello World application successfully connected to {{site.data.keyword.Bluemix_notm}}](images/yayconnected.jpg "Figure 1. Hello World application successfully connected to Bluemix")
-->

  Se a conexão falhar, você verá:
  `Que pena. Algo saiu errado`
  {: screen}

 <!--
  ![Hello World application not connected to Bluemix](images/bummer_android.jpg "Figure 2. Hello World application not connected to Bluemix")
  -->

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
   * [Amostra Hello Bluemix (iOS)](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-hellobluemix)

## sdk
   * [SDK principal](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)

## interface de programação de aplicativos
   * [API do Núcleo](https://www.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)
