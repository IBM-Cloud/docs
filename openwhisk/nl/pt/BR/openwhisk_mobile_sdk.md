
# Usando o SDK móvel do OpenWhisk

O OpenWhisk fornece um SDK móvel para dispositivos iOS e watchOS que
permite que apps móveis disparem facilmente acionadores remotos e chamem ações remotas. Uma versão para
Android não está atualmente disponível; os desenvolvedores para Android podem usar a API de REST do
OpenWhisk diretamente.

O SDK móvel é gravado em Swift 3.0 e suporta o iOS 10 e liberações mais recentes. É possível construir o SDK móvel usando o Xcode 8.0. As versões do Swift 2.2/Xcode 7 legado do SDK estão disponíveis até 0.1.7, embora isso agora esteja descontinuado.

## Incluindo o SDK em seu app

É possível instalar o SDK móvel usando o CocoaPods, o Carthage ou a partir do diretório de origem.

### Instalando usando o CocoaPods

O SDK do OpenWhisk para dispositivo móvel está disponível para
distribuição pública por meio do CocoaPods. Supondo que o CocoaPods esteja instalado, coloque as linhas
a seguir em um arquivo chamado 'Podfile' dentro do diretório de projeto do aplicativo iniciador.

```
install! 'cocoapods', :deterministic_uuids => false
use_frameworks!

target 'MyApp' do
     pod 'OpenWhisk', :git => 'https://github.com/openwhisk/openwhisk-client-swift.git', :tag => '0.2.2'
end

target 'MyApp WatchKit Extension' do
     pod 'OpenWhisk', :git => 'https://github.com/openwhisk/openwhisk-client-swift.git', :tag => '0.2.2'
end
```

A partir da linha de comandos, digite `pod install`. Esse comando instala o SDK para um app iOS com uma extensão watchOS.  Use o arquivo de área de trabalho que o CocoaPods cria para o seu
aplicativo para abrir o projeto no Xcode. 

Após a instalação, abra a área de trabalho do seu projeto.  É possível obter o seguinte aviso ao construir:
`Use Legacy Swift Language Version” (SWIFT_VERSION) is required to be configured correctly for targets which use Swift. Use the [Edit > Convert > To Current Swift Syntax…] menu to choose a Swift version or use the Build Settings editor to configure the build setting directly.`
Isso ocorrerá se o Cocoapods não atualizar a versão do Swift no projeto Pods.  Para corrigir, selecione o
projeto Pods e o destino OpenWhisk. Acesse Configurações de construção e mude a configuração `Use Legacy Swift Language Version` para `no`. Como alternativa, é possível incluir as seguintes instruções de instalação no final do seu arquivo pod:

```
post_install do |installer|
  installer.pods_project.targets.each do |target|
    target.build_configurations.each do |config|
      config.build_settings['SWIFT_VERSION'] = '3.0'
    end
  end
end
```

### Instalando usando o Carthage

Crie um arquivo no diretório de projeto do app e chame-o de 'Cartfile'. Coloque a
linha a seguir no arquivo:
```
github "openwhisk/openwhisk-client-swift.git" ~> 0.2.2 # Or latest version
```

A partir da linha de comandos, digite `carthage update --platform ios`. O Carthage faz download e constrói o SDK, cria um diretório chamado Carthage no diretório de projeto do seu app e coloca um arquivo OpenWhisk.framework dentro de Carthage/build/iOS.

Deve-se, então, incluir OpenWhisk.framework nas estruturas integradas em seu projeto Xcode

### Instalando a partir do código-fonte

O código-fonte está disponível em https://github.com/openwhisk/openwhisk-client-swift.git.
Abra o projeto usando o `OpenWhisk.xcodeproj` que usa Xcode.
O projeto contém dois esquemas: "OpenWhisk" (destinado ao iOS) e "OpenWhiskWatch" (destinado ao watchOS 2).
Construa o projeto para os destinos que você precisa e inclua as estruturas resultantes em
seu app (geralmente, em ~/Library/Developer/Xcode/DerivedData/nome de seu app).

## Instalando o exemplo do app iniciador

É possível usar a CLI do OpenWhisk para fazer download de código de
exemplo que integra a estrutura do SDK do OpenWhisk.  

Para instalar o exemplo do app iniciador, insira o comando a seguir:
```
$ wsk sdk install iOS
```

Esse comando faz download de um arquivo compactado que contém o app iniciador. Dentro do diretório de projeto há um arquivo pod. 

Para instalar o SDK, insira o comando a seguir:
```
$ pod install
```

## Introdução ao SDK

Para estar funcionando rapidamente, crie um objeto WhiskCredentials com suas credenciais de API do
OpenWhisk e crie uma instância do
OpenWhisk por meio do objeto.

Por exemplo, use o código de exemplo a seguir para criar um objeto de credenciais:

```
let credentialsConfiguration = WhiskCredentials(accessKey: "myKey", accessToken: "myToken")
let whisk = Whisk(credentials: credentialsConfiguration!)
```

No exemplo anterior, você transmite o `myKey` e o `myToken` que são
obtidos do OpenWhisk. É possível recuperar a chave e o token com o comando da CLI a seguir:

```
$ wsk property get --auth
```
```
whisk auth        kkkkkkkk-kkkk-kkkk-kkkk-kkkkkkkkkkkk:tttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttt
```

As sequências antes de dois-pontos é sua chave e a sequência após os dois-pontos é
seu token.

## Chamando uma ação do OpenWhisk


Para chamar uma ação remota, é possível chamar `invokeAction` com o nome da ação. É
possível especificar o namespace ao qual a ação pertence ou apenas deixá-lo em branco
para aceitar o namespace padrão. Use um dicionário para passar parâmetros para a ação conforme necessário.

Por
exemplo:

```swift
// In this example, we are invoking an action to print a message to the OpenWhisk Console
var params = Dictionary<String, String>()
params["payload"] = "Hi from mobile"
do {
    try whisk.invokeAction(name: "helloConsole", package: "mypackage", namespace: "mynamespace", parameters: params, hasResult: false, callback: {(reply, error) -> Void in
        if let error = error {
            //do something
            print("Error invoking action
\(error.localizedDescription)")
        } else {
            print("Action invoked!")
        }
    })
} catch {
    print("Error \(error)")
}
```

No exemplo anterior, você chama a ação `helloConsole` usando o namespace padrão.

## Disparando um acionador do OpenWhisk 

Para disparar um acionador remoto, é possível chamar o método `fireTrigger`. Passe parâmetros conforme necessário usando um dicionário.

```swift
// In this example we are firing a trigger when our location has changed by a certain amount
var locationParams = Dictionary<String, String>()
locationParams["payload"] = "{\"lat\":41.27093, \"lon\":-73.77763}"
do {
    try whisk.fireTrigger(name: "locationChanged", package: "mypackage", namespace: "mynamespace", parameters: locationParams, callback: {(reply, error) -> Void in
        if let error = error {
            print("Error firing trigger \(error.localizedDescription)")
        } else {
            print("Trigger fired!")
        }
    })
} catch {
    print("Error \(error)")
}
```

No exemplo anterior, você está disparando um acionador que é chamado
`locationChanged`.

## Usando ações que retornam um resultado

Se a ação retornar um resultado, configure hasResult para true na chamada invokeAction. O resultado da ação é retornado no dicionário de resposta, por exemplo:

```swift
do {
    try whisk.invokeAction(name: "actionWithResult", package: "mypackage", namespace: "mynamespace", parameters: params, hasResult: true, callback: {(reply, error) -> Void in
        if let error = error {
            //do something
            print("Error invoking action
\(error.localizedDescription)")
        } else {
            var result = reply["result"]
            print("Got result \(result)")
        }
    })
} catch {
    print("Error \(error)")
}
```

Por padrão, o SDK retorna apenas o ID de ativação e qualquer resultado produzido pela ação chamada. Para obter os metadados do objeto de resposta inteiro, que inclui o código de status de resposta HTTP, use a configuração a seguir:

```swift
whisk.verboseReplies = true
```

## Configurando o SDK

É possível configurar o SDK para trabalhar com diferentes instalações do
OpenWhisk usando o parâmetro baseURL. Por exemplo:

```swift
whisk.baseURL = "http://localhost:8080"
```

Neste exemplo, use uma instalação em execução no localhost:8080. Se você não
especificar a URL base, o SDK móvel usará a instância em execução em
https://openwhisk.ng.bluemix.net.

É possível passar um NSURLSession customizado caso requeira manipulação de rede especial. Por exemplo,
é possível ter sua própria instalação do OpenWhisk que usa certificados
autoassinados:

```swift
// create a network delegate that trusts everything
class NetworkUtilsDelegate: NSObject, NSURLSessionDelegate {
    func URLSession(session: NSURLSession, didReceiveChallenge challenge: NSURLAuthenticationChallenge, completionHandler: (NSURLSessionAuthChallengeDisposition, NSURLCredential?) -> Void) {
        completionHandler(NSURLSessionAuthChallengeDisposition.UseCredential, NSURLCredential(forTrust: challenge.protectionSpace.serverTrust!))
    }
}
// create an NSURLSession that uses the trusting delegate
let session = NSURLSession(configuration: NSURLSessionConfiguration.defaultSessionConfiguration(), delegate: NetworkUtilsDelegate(), delegateQueue:NSOperationQueue.mainQueue())
// set the SDK to use this urlSession instead of the default shared one
whisk.urlSession = session
```

### Suporte para nomes qualificados

Todas as ações e acionadores têm um nome completo composto por um namespace, um pacote e um nome de ação ou de acionador. O
SDK pode aceitar esses elementos como parâmetros quando você está chamando uma ação ou
disparando um acionador. O SDK também fornece uma função que aceita um nome completo semelhante a `/mynamespace/mypackage/nameOfActionOrTrigger`. 
A sequência de nome qualificado suporta valores padrão não denominados para namespaces e pacotes que usuários
do OpenWhisk têm, de modo que as regras de análise a seguir se aplicam:

- qName = "foo" resulta em namespace = default, package = default, action/trrigger = "foo"
- qName = "mypackage/foo" resulta em namespace = default, package = mypackage, action/trigger = "foo"
- qName = "/mynamespace/foo" resulta em namespace = mynamespace, package = default, action/trigger = "foo"
- qName = "/mynamespace/mypackage/foo resulta em namespace = mynamespace, package = mypackage, action/trigger = "foo"

Todas as outras combinações emitem um erro WhiskError.QualifiedName. Portanto, ao
usar nomes qualificados, deve-se agrupar a chamada em uma construção "`do/try/catch`".

### Botão do SDK

Por conveniência, o SDK inclui um `WhiskButton`, que estende o `UIButton` para permitir que ele chame ações.  Para usar o `WhiskButton`, siga este exemplo:

```swift
var whiskButton = WhiskButton(frame: CGRectMake(0,0,20,20))
whiskButton.setupWhiskAction("helloConsole", package: "mypackage", namespace: "_", credentials: credentialsConfiguration!, hasResult: false, parameters: nil, urlSession: nil)
let myParams = ["name":"value"]
// Call this when you detect a press event, e.g. in an IBAction, to invoke the action
whiskButton.invokeAction(parameters: myParams, callback: { reply, error in
    if let error = error {
        print("Oh no, error: \(error)")
    } else {
        print("Success: \(reply)")
    }
})
// or alternatively you can set up a "self contained" button that listens for press events on itself and invokes an action
var whiskButtonSelfContained = WhiskButton(frame: CGRectMake(0,0,20,20))
whiskButtonSelfContained.listenForPressEvents = true
do {
   // use qualified name API which requires do/try/catch
   try whiskButtonSelfContained.setupWhiskAction("mypackage/helloConsole", credentials: credentialsConfiguration!, hasResult: false, parameters: nil, urlSession: nil)
   whiskButtonSelfContained.actionButtonCallback = { reply, error in
       if let error = error {
           print("Oh no, error: \(error)")
       } else {
           print("Success: \(reply)")
       }
   }
} catch {
   print("Error setting up button \(error)")
}
```
