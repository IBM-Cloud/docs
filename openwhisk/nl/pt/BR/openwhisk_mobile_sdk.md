---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Usando o SDK móvel do {{site.data.keyword.openwhisk_short}}
{: #openwhisk_mobile_sdk}
*Última atualização: 28 de março de 2016*

O {{site.data.keyword.openwhisk}} fornece um SDK móvel para dispositivos com iOS e watchOS 2 que permite que apps móveis disparem acionadores remotos e chamem ações remotas facilmente. Uma versão para Android não está atualmente disponível; os desenvolvedores para Android podem usar a API REST do {{site.data.keyword.openwhisk}} diretamente.
{: shortdesc}

O SDK móvel é escrito em Swift 2.2 e suporta o iOS 9 e liberações posteriores.

## Incluindo o SDK em seu app
{: #openwhisk_add_sdk}
É possível instalar o SDK móvel usando o CocoaPods, o Carthage ou a partir do diretório de origem.

### Instalando usando o CocoaPods 

O SDK do {{site.data.keyword.openwhisk_short}} para dispositivo móvel está disponível para distribuição pública por meio do CocoaPods. Supondo que o Cocoapods esteja instalado, coloque as linhas a seguir em um arquivo chamado 'Podfile' dentro do diretório de projeto do app starer. 

```
source 'https://github.com/openwhisk/openwhisk-podspecs.git'

use_frameworks!

target 'MyApp' do
     platform :ios, '9.0'
     pod 'OpenWhisk'
end

target 'MyApp WatchKit Extension' do
     platform :watchos, '2.0'
     pod 'OpenWhisk-Watch'
end
```
{: codeblock}

Na linha de comandos, digite "pod install". Isso instalará o SDK para um app iOS com uma extensão watchOS 2.  Use o arquivo de área de trabalho que o Cocoapods cria para seu app para abrir o projeto no Xcode.

### Instalando usando o Carthage

Crie um arquivo no diretório de projeto de seu app e chame-o de 'Cartfile'. Coloque as linhas a seguir no Cartfile:
```
github "openwhisk//openwhisk-client-swift.git" ~> 0.1.0 # Or latest version
```
{: codeblock}

Na linha de comandos, digite 'carthage update --platform ios'. O Carthage faz download e constrói o SDK, cria um diretório chamado Carthage no diretório de projeto do seu app e coloca um arquivo OpenWhisk.framework dentro de Carthage/build/iOS. Inclua OpenWhisk.framework nas estruturas integradas em seu projeto Xcode.

### Instalando a partir do código-fonte

O código-fonte está disponível em https://github.com/openwhisk//openwhisk-client-swift.git. Abra o projeto usando o arquivo OpenWhisk.xcodeproj no Xcode.  O projeto contém dois esquemas "OpenWhisk" e "OpenWhiskWatch" destinados ao iOS e ao WathOS2, respectivamente.  Construa o projeto para os destinos que precisa e inclua as estruturas resultantes em seu app (geralmente, em ~/Library/Developer/Xcode/DerivedData/nome de seu app).

## Instalando o exemplo do app iniciador
{: #openwhisk_install_sdkstart}

É possível usar a CLI do {{site.data.keyword.openwhisk_short}} para fazer download de código de exemplo que incorpora a estrutura do SDK do {{site.data.keyword.openwhisk_short}}.  

Para instalar o exemplo do app iniciador, insira o comando a seguir:
```
wsk sdk install iOS
```
Isso fará download de um arquivo zip que contém o app iniciador.  Dentro do diretório do projeto está um Podfile.  Execute "pod install" a partir de um terminal para instalar o SDK.
{: pre}

## Introdução ao SDK
{: #openwhisk_sdk_getstart}

Para estar funcionando rapidamente, crie um objeto WhiskCredentials com suas credenciais da API do {{site.data.keyword.openwhisk_short}} e crie uma instância do {{site.data.keyword.openwhisk_short}} a partir disso.

Por exemplo, no Swift 2.1, use o código de exemplo a seguir para criar um objeto de credenciais:

```
let credentialsConfiguration = WhiskCredentials(accessKey: "myKey", accessToken: "myToken")

let whisk = Whisk(credentials: credentialsConfiguration!)
```
{: codeblock}

No exemplo anterior, você passa o `myKey` e o `myToken` que obtém do {{site.data.keyword.openwhisk_short}}. É possível recuperar a chave e o token com o comando da CLI a seguir:

```
wsk property get --auth
```
{: pre}
```
whisk auth        kkkkkkkk-kkkk-kkkk-kkkk-kkkkkkkkkkkk:tttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttt
```
{: screen}

As sequências antes e depois dos dois pontos são sua chave e token, respectivamente.

## Chamando uma ação do {{site.data.keyword.openwhisk_short}}
{: #openwhisk_sdk_invoke}


Para chamar uma ação remota, é possível chamar `invokeAction` com o nome da ação. É possível especificar o namespace ao qual a ação pertence ou apenas deixá-lo em branco para aceitar o namespace padrão.  Use um dicionário para passar parâmetros para a ação conforme necessário.

Por
exemplo:

```
// In this example, we are invoking an action to print a message to
the OpenWhisk Console var params = Dictionary<String, String>()
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
{: codeblock}

No exemplo anterior, você chama a ação `helloConsole` usando o namespace padrão.

## Disparando um acionador do {{site.data.keyword.openwhisk_short}}
{: #openwhisk_sdk_fire}

Para disparar um acionador remoto, é possível chamar o método `fireTrigger`. Passe parâmetros conforme necessário usando um dicionário.

```
// In this example we are firing a trigger when our location has
changed by a certain amount

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
{: codeblock}

No exemplo anterior, você está disparando um acionador chamado `locationChanged`.

## Usando ações que retornam um resultado
{: #openwhisk_sdk_actionresult}

Se a ação retornar um resultado, configure hasResult para true na chamada invokeAction. O resultado da ação é retornado no dicionário de resposta, por exemplo:

```
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
{: codeblock}

Por padrão, o SDK retorna apenas o ID de ativação e qualquer resultado produzido pela ação chamada. Para obter os metadados do objeto de resposta inteiro, que inclui o código de status de resposta HTTP, use a configuração a seguir:

```
whisk.verboseReplies = true
```
{: codeblock}

## Configurando o SDK
{: #openwhisk_sdk_configure}

É possível configurar o SDK para trabalhar com diferentes instalações do {{site.data.keyword.openwhisk_short}} usando o parâmetro baseURL. Por exemplo:

```
whisk.baseURL = "http://localhost:8080"
```
{: codeblock}

Neste exemplo, use uma instalação em execução no localhost:8080.  Se
você não especificar o baseUrl, o SDK móvel usará a instância em execução em https://openwhisk.ng.bluemix.net.

É possível passar um NSURLSession customizado caso requeira manipulação de rede especial. Por exemplo, você pode ter sua própria instalação do {{site.data.keyword.openwhisk_short}} que usa certificados autoassinados:

```
// create a network delegate that trusts everything class
NetworkUtilsDelegate: NSObject, NSURLSessionDelegate {
    func URLSession(session: NSURLSession, didReceiveChallenge challenge: NSURLAuthenticationChallenge, completionHandler: (NSURLSessionAuthChallengeDisposition, NSURLCredential?) -> Void) {
        completionHandler(NSURLSessionAuthChallengeDisposition.UseCredential, NSURLCredential(forTrust: challenge.protectionSpace.serverTrust!))
    }
}

// create an NSURLSession that uses the trusting delegate let
session = NSURLSession(configuration:
NSURLSessionConfiguration.defaultSessionConfiguration(), delegate:
NetworkUtilsDelegate(), delegateQueue:NSOperationQueue.mainQueue())

// set the SDK to use this urlSession instead of the default
shared one whisk.urlSession = session
```
{: codeblock}

### Suporte para nomes qualificados

Todas as ações e acionadores têm um nome completo composto por um namespace, um pacote e um nome de ação ou de acionador. O SDK pode aceitá-los como parâmetros ao chamar uma ação ou disparar um acionador. O SDK também fornece uma função que aceita um nome completo semelhante a `/mynamespace/mypackage/nameOfActionOrTrigger`. A sequência de nome qualificado suporta valores padrão não denominados para namespaces e pacotes que usuários do {{site.data.keyword.openwhisk_short}} têm, portanto, as regras de análise a seguir se aplicam:

- qName = "foo" resulta em namespace = default, package = default, action/trrigger = "foo"
- qName = "mypackage/foo" resulta em namespace = default, package = mypackage, action/trigger = "foo"
- qName = "/mynamespace/foo" resulta em namespace = mynamespace, package = default, action/trigger = "foo"
- qName = "/mynamespace/mypackage/foo resulta em namespace = mynamespace, package = mypackage, action/trigger = "foo"

Todas as outras combinações emitem um erro WhiskError.QualifiedName. Portanto, ao usar nomes qualificados, deve-se agrupar a chamada em uma construção "`do/try/catch`".

### Botão do SDK

Por conveniência, o SDK inclui um `WhiskButton`, que estende o `UIButton` para permitir que ele chame ações.  Para usar o `WhiskButton`, siga este exemplo:

```
var whiskButton = WhiskButton(frame: CGRectMake(0,0,20,20))

whiskButton.setupWhiskAction("helloConsole", package: "mypackage", namespace: "_", credentials: credentialsConfiguration!, hasResult: false, parameters: nil, urlSession: nil)

let myParams = ["name":"value"]

// Call this when you detect a press event, e.g. in an
IBAction, to invoke the action whiskButton.invokeAction(parameters:
myParams, callback: { reply, error in
    if let error = error {
        print("Oh no, error: \(error)")
    } else {
        print("Success: \(reply)")
    }
})

// or alternatively you can set up a "self contained" button
that listens for press events on itself and invokes an action

var whiskButtonSelfContained = WhiskButton(frame: CGRectMake(0,0,20,20))
whiskButtonSelfContained.listenForPressEvents = true
do {

   // use qualified name API which requires do/try/catch
   try
whiskButtonSelfContained.setupWhiskAction("mypackage/helloConsole",
credentials: credentialsConfiguration!, hasResult: false, parameters:
nil, urlSession: nil)
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
{: codeblock}
