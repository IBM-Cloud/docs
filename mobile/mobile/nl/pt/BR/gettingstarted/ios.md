<!-- Attribute definitions -->
{:codeblock: .codeblock}
{:screen: .screen}

# Introdução à amostra de HelloWorld
{: #gettingstarted-ios}
Se desejar iniciar com um novo app iOS, é possível usar o app HelloWorld. Esse app demonstra como se conectar ao backend do {{site.data.keyword.Bluemix}} a partir de um app móvel sem autenticação. O app já possui o SDK instalado. Quando você estiver pronto, poderá obter as bibliotecas específicas que deseja usar em seu app.

1. Crie seu backend móvel em {{site.data.keyword.Bluemix_notm}}.
<ol>
	<li>Na seção Textos padrão do catálogo do {{site.data.keyword.Bluemix_notm}}, clique em **MobileFirst Services Starter**.</li>
    <li>Insira um nome e um host para seu app e clique em **Criar**.</li>
    <li>Clique em **Concluir**. </li>
</ol>
2. Obtenha o projeto a partir do GitHub. Em seu computador, abra o terminal e insira o comando a seguir:
```
git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloworld
```

3. Inicialize o projeto.
Para inicializar o SDK, copie o código a seguir para o método `didFinishLaunchingWithOptions` no Aplicativo delegado.
   * Objective-C:
```
// inicializar o SDK com o ID e a rota do aplicativo IBM Bluemix
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:@"<insert route>" backendGUID:@"<insertGUID>"];
return YES;
```{: codeblock}
   * Swift:
```
// inicializar o SDK com o ID e a rota do aplicativo IBM Bluemix
IMFClient.sharedInstance().initializeWithBackendRoute("<insert route>", backendGUID: "<insertGUID>")
return true
```{: codeblock}

4. Execute a amostra em seu ambiente de desenvolvimento.
No Xcode, clique em **Produto&gt;Executar**. Um simulador do iOS é iniciado.
No simulador, clique em **Executar ping no
                {{site.data.keyword.Bluemix_notm}}**. O app de amostra obtém o cabeçalho de autorização a partir do serviço Mobile Client Access. Se o ping for bem-sucedido, o texto no simulador será atualizado.
<br/>Quando você se conectar com êxito ao {{site.data.keyword.Bluemix_notm}} a partir do app móvel no Xcode, uma mensagem que diz "Oba! você está conectado" será exibida:<br/>
![Aplicativo Hello World conectado com êxito ao {{site.data.keyword.Bluemix_notm}}](images/yayconnected.jpg "Figura 1. Aplicativo Hello World conectado com êxito ao {{site.data.keyword.Bluemix_notm}}")
<br/>
Se você se conectar com êxito, o Xcode do login de depuração conterá a mensagem a seguir:
```Você se conectou ao {{site.data.keyword.Bluemix_notm}} com êxito```
5. Resolva quaisquer problemas.
Quando a conexão falha, uma mensagem "Puxa, algo deu errado" é exibida. Mais informações sobre o erro são incluídas.<br/>
![Aplicativo Hello World não conectado ao {{site.data.keyword.Bluemix_notm}}](images/bummer_android.jpg "Figura 2. Aplicativo Hello World não conectado ao Bluemix")
<br/>Verifique se você colou corretamente os valores de rota e GUID:
   * Objective-C:
  ```
  [imfClient initializeWithBackendRoute:@"https://hellotest.mybluemix.net"
  backendGUID:@"9d48d73a-0878-4254-test-bdcbe6c79c31"];
  ``` {: codeblock}
   * Swift:
  ```
  IMFClient.sharedInstance().initializeWithBackendRoute("https://hellotest.mybluemix.net", backendGUID: "9d48d73a-0878-4254-test-bdcbe6c79c31")
  ```{: codeblock}


Também é possível verificar o log de depuração para obter mais informações.

## Próximas etapas:
{: #next}
Para obter informações sobre como obter o SDK e o integrar ao app móvel, consulte as informações sobre como configurar os serviços {{site.data.keyword.Bluemix}}.
   * [Mobile Client Access](../../services/mobileaccess/index.html)
   * [Enviar por push](../../services/mobilepush/index.html)

# rellinks

## exemplos
   * [HelloWorld (iOS)](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloworld)

## sdk
   * [bms-clientsdk-ios-core](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-ios-core)

## interface de programação de aplicativos
   *
[API do núcleo](https://www.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html)
