---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Gerenciando Identificações
{: #manage_tags}
Última atualização: 11 de janeiro de 2017
{: .last-updated}

Use o painel {{site.data.keyword.mobilepushshort}} para criar e excluir
tags de seu aplicativo e depois inicializar notificações baseadas em tag. A notificação
baseada em tag é recebida nos dispositivos inscritos nas tags.


## Criando marcações
{: #create_tags}

Notificações baseadas em tag são mensagens que se destinam a todos os dispositivos inscritos em uma tag específica. Cada dispositivo pode se inscrever em
qualquer número de tags. Quando uma tag é excluída, informações associadas a essa tag, incluindo seus assinantes e dispositivos, são excluídos. O
cancelamento de assinatura automático não é necessário, uma vez que a tag não
existe mais. Nenhuma ação posterior é necessária no lado do cliente.

1. No painel {{site.data.keyword.mobilepushshort}}, selecione a tag **Tags**.
1. Clique no botão + **Criar tag**.   
   1. No campo **Nome**, insira o nome da tag. Por exemplo, "coupons".
   1. No campo **Descrição**, insira uma descrição de tag.
   1. Clique em **Salvar**.

1. Na área **Fragmentos de códigos**,
selecione a plataforma para seu aplicativo móvel.
1. Modifique os fragmentos de códigos para manipular erros e
depois copie os fragmentos de códigos para cada tag em seu
aplicativo móvel.

## Excluindo marcações
{: #delete_tags}

1. Na guia **Tag**, selecione a tag que você deseja excluir e
clique no ícone **Excluir**.
1. Clique em **OK**.

## Editando uma descrição de tag
{: #edit_tags}

1. Na guia **Tag**, selecione a tag que deseja
editar.
1. Clique no ícone **Editar**.
1. Edite a descrição d tag e clique no botão
**Salvar**.

# Obtendo tags
{: #get_tags}

As tags fornecem uma maneira de enviar notificações destinadas a usuários com base
em seus interesses, ao contrário das transmissões em geral que são enviadas a todos os
aplicativos. É possível criar e gerenciar tags usando a guia Tag no painel
{{site.data.keyword.mobilepushshort}} ou use APIs REST. É possível usar fragmentos de código para gerenciar e consultar as assinaturas de identificação de seu aplicativo
móvel. É possível usar esses fragmentos de código para obter assinaturas, assinar uma
tag, cancelar a assinatura de uma tag ou obter uma lista de tags disponíveis. Copie esses
fragmentos de código para seu aplicativo móvel.

## Obtendo tags no Android
{: android-get-tags}

A API **getTags**
retorna a lista de identificações disponíveis as quais o dispositivo pode assinar. Depois que o dispositivo é inscrito em uma tag específica, ele pode receber {{site.data.keyword.mobilepushshort}} enviada para essa tag.

Copie os fragmentos de código a seguir para seu aplicativo móvel Android para obter
uma lista de tags nas quais o dispositivo está inscrito e obter uma lista de tags
disponíveis.

Use a API **getTags** a seguir para obter uma lista de tags
disponíveis as quais o dispositivo podem assinar.

```
// Get a list of available tags to which the device can subscribe
push.getTags(new MFPPushResponseListener<List<String>>(){
   @Override
   public void onSuccess(List<String> tags){
   updateTextView("Retrieved available tags: " + tags);
   System.out.println("Available tags are: "+tags);
   availableTags = tags;
   subscribeToTag();
  }
  @Override
  public void onFailure(MFPPushException ex){
     updateTextView("Error getting available tags.. " + ex.getMessage());
    }
   })  
```
	{: codeblock}

Use a API **getSubscriptions** para obter uma lista
de tags nas quais o dispositivo está inscrito.

```
// Get a list of tags that to which the device is subscribed.
push.getSubscriptions(new MFPPushResponseListener<List<String>>() {
  @Override
    public void onSuccess(List<String> tags) {
  updateTextView("Retrieved subscriptions : " + tags);
    System.out.println("Subscribed tags are: "+tags);
    subscribedTags = tags;
    subscribeToTag();
    }
  @Override
    public void onFailure(MFPPushException ex) {
       updateTextView("Error getting subscriptions.. " + ex.getMessage());
  }
})
	```
	{: codeblock}

## Obtendo tags no Cordova
{: cordova-get-tags}

Copie os fragmentos de código a seguir para seu aplicativo móvel para obter uma
lista de tags nas quais o dispositivo está inscrito e uma lista de tags disponíveis.

Recupere uma matriz de tags que estiverem disponíveis para assinatura.

```
//Get a list of available tags to which the device can subscribe
BMSPush.retrieveAvailableTags(function(tags) {
  alert(tags);
}, failure); 
```
	{: codeblock}

```
//Get a list of available tags to which the device is subscribed.
BMSPush.retrieveSubscriptions(function(tags) {
   alert(tags); 
}, failure); 
```
	{: codeblock}


## Obtendo tags no Swift
{: swift-get-tags}

A API **retrieveAvailableTagsWithCompletionHandler** retorna a lista de
identificações disponíveis as quais o dispositivo pode assinar. Depois que o dispositivo é inscrito em uma tag específica, ele pode receber {{site.data.keyword.mobilepushshort}} enviada para essa tag.

Chame o {{site.data.keyword.mobilepushshort}} para obter assinaturas para uma tag.

Copie os fragmentos de códigos a seguir em seu aplicativo móvel Swift para obter uma
lista de tags disponíveis nas quais o dispositivo está inscrito e para obter uma lista de
tags disponíveis as quais o dispositivo pode assinar.
```
//Get a list of available tags to which the device can subscribe
	push.retrieveAvailableTagsWithCompletionHandler({ (response, statusCode, error) -> Void in
    if error.isEmpty 
		{
     print( "Response during retrieve tags : \(response)")
        print( "status code during retrieve tags : \(statusCode)")
    }
    else {
    print( "Error during retrieve tags \(error) ")
    Print( "Error during retrieve tags \n  - status code: \(statusCode) \n Error :\(error) \n")
    	}
	}
```
		{: codeblock}

```
//Get a list of available tags to which the device is subscribed
push.retrieveSubscriptionsWithCompletionHandler { (response, statusCode, error) -> Void in
    if error.isEmpty {
    print( "Response during retrieving subscribed tags : \(response?.description)")
        print( "status code during retrieving subscribed tags : \(statusCode)")
    }
    else {
    print( "Error during retrieving subscribed tags \(error) ")
    Print( "Error during retrieving subscribed tags \n  - status code: \(statusCode) \n Error :\(error) \n")
        }
	}
```
	{: codeblock}

## Google Chrome, Safari e Mozilla Firefox
{: web-get-tags}

Para obter a lista de identificações disponíveis, a qual os clientes podem assinar, use o código a seguir.

```
var bmsPush = new BMSPush();
  bmsPush.retrieveAvailableTags(function(response) 
	{
  alert(response.response)
    var json = JSON.parse(response.response);
    var tagsA = []
  for (i in json.tags)
	{
    tagsA.push(json.tags[i].name)
    }
   alert(tagsA)
 })
```
	{: codeblock}


## Apps Google Chrome e Extensões
{: web-get-tags}

Para obter a lista de identificações disponíveis, a qual os clientes podem assinar, use o código a seguir.

```
var bmsPush = new BMSPush();
  bmsPush.retrieveAvailableTags(function(response) 
	{
  alert(response.response)
    var json = JSON.parse(response.response);
    var tagsA = []
  for (i in json.tags)
	{
    tagsA.push(json.tags[i].name)
    }
   alert(tagsA)
 })
```
	{: codeblock}

Copie os fragmentos de código a seguir em seus Apps Google Chrome e Extensões para
obter uma lista de identificações nas quais os clientes se inscreveram.

```
var bmsPush = new BMSPush();
  bmsPush.retrieveSubscriptions(function(response) 
	{
   alert(response.response)
 })
```
	{: codeblock}


# Assinando e removendo assinatura de tags
{: #Subscribe_tags}

Use os fragmentos de código a seguir para permitir que seus dispositivos obtenham
assinaturas, bem como assinem e cancelem a assinatura de uma tag.

## Assinando e removendo assinatura de tags no Android
{: android-subscribe-tags}

Copie e cole este fragmento de código em seu aplicativo móvel Android.

```
push.subscribe(allTags.get(0),
new MFPPushResponseListener<String>() {
  @Override
    public void onFailure(MFPPushException ex) {
  updateTextView("Error subscribing to Tag1.."
           + ex.getMessage());
  }
  @Override
  public void onSuccess(String arg0) {
  updateTextView("Succesfully Subscribed to: "+ arg0);
   unsubscribeFromTags(arg0);
   }
  });
```
	{: codeblock}

```
push.unsubscribe(tag, new MFPPushResponseListener<String>() {
 @Override
 public void onSuccess(String s) {
 updateTextView("Unsubscribing from tag");
   updateTextView("Successfully unsubscribed from tag . "+ tag);
 }
 @Override
 public void onFailure(MFPPushException e) {
 updateTextView("Error while unsubscribing from tags. "+ e.getMessage());
 }
 });
```
	{: codeblock}

## Assinando e removendo assinatura de tags no Cordova
{: cordova-subscribe-tags}

Copie e cole este fragmento de código em seu aplicativo móvel Cordova.

```
var tag = "YourTag";
BMSPush.subscribe(tag, success, failure);
BMSPush.unsubscribe(tag, success, failure);
```
	{: codeblock}


## Assinando e removendo assinatura de tags no Swift
{: swift-subscribe-tags}

Copie e cole este fragmento de código em seu aplicativo móvel Swift.

Use a API **subscribeToTags** para assinar uma
identificação.

```
push.subscribeToTags(tagsArray: ["MyTag"], completionHandler: { (response, statusCode, error) -> Void in
    if error.isEmpty {
        print("Response when subscribing to tags: \(response?.description)")
        print("Status code when subscribing to tags: \(statusCode)")
    } else {
        print("Error when subscribing to tags: \(error) ")
        print("Error status code when subscribing to tags: \(statusCode)")
    }
})
```
	{: codeblock}

Use a API **unsubscribeFromTags** para cancelar a assinatura de uma
identificação.

```
push.unsubscribeFromTags(response, completionHandler: { (response, statusCode, error) -> Void in
    if error.isEmpty {
     print( "Response during unsubscribed tags : \(response?.description)")
        print( "status code during unsubscribed tags : \(statusCode)")
    }
  else {
    print( "Error during  unsubscribed tags \(error) ")
    print( "Error during unsubscribed tags \n  - status code: \(statusCode) \n Error :\(error) \n")
  }
}
```
	{: codeblock}

## Google Chrome e Mozilla Firefox
{: web-subscribe-tags}

Para assinar tags de aplicativos da web, use o fragmento de código a seguir:

```
var tagsArray = ["tag1", "Tag2"]
bmsPush.subscribe(tagsArray,function(response) {
  alert(response.response)
})
```
	{: codeblock}

Cancele a assinatura das tags usando o método **unSubscribe**.

```
var tagsArray = ["tag1", "Tag2"]
 bmsPush.unSubscribe(tagsArray,function(response) {
 alert(response.response)
})
```
	{: codeblock}

# Usando notificações baseada em tag
{: #using_tags}

Notificações baseadas em tag são mensagens que se destinam a todos os dispositivos inscritos em uma tag específica. Cada dispositivo pode ser inscrito em qualquer número de tags. Este
tópico descreve como enviar notificações baseadas em tag. As assinaturas são mantidas pela instância do Bluemix do serviço {{site.data.keyword.mobilepushshort}}. Quando uma tag é excluída, todas as informações associadas a essa tag, incluindo seus assinantes e dispositivos, são excluídas. Nenhum cancelamento de
assinatura automático é necessário para essa tag, uma vez que ela não existe mais e
nenhuma ação adicional é necessária no lado do cliente.

Crie tags na tela **Tag**. Para obter informações sobre como
criar tags, consulte
[Criando tags](t_manage_tags.html).

1. A partir do painel **Notificação push**, clique em **Enviar notificações**.
1. Selecione a opção **Dispositivo por identificação** na lista suspensa **Enviar para**.
1. Procure as identificações que deseja usar e selecione-as.
![Tela de notificações](images/tag_notification.jpg)
1. No campo **Texto da mensagem**, insira o texto que seria enviado como uma notificação ao público inscrito.
1. Clique em **Enviar**.
