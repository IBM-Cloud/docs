# Obtendo tags
{: #get_tags}

As identificações fornecem uma maneira de enviar notificações desejadas aos usuários com base em seus interesses,
ao contrário de transmissões gerais que são enviadas a todos os aplicativos. É possível
criar e gerenciar tags usando a guia Tag no painel Push ou usar APIs REST. É possível
usar fragmentos de código nas seções a seguir para gerenciar e consultar assinaturas de
tag de seu aplicativo móvel. É possível usar esses fragmentos de código para obter
assinaturas, inscrever-se em uma tag, cancelar a assinatura de
uma tag, obter uma lista de tags disponíveis. Copie e cole esses fragmentos de código em seu aplicativo móvel.

## Android

A API **getTags**
retorna a lista de identificações disponíveis as quais o dispositivo pode assinar. Depois que o dispositivo está inscrito em uma
identificação específica, ele pode receber qualquer notificação push enviada para essa
identificação.

Copie os seguintes fragmentos de códigos em seu aplicativo
móvel Android para obter uma lista de tags nas quais o dispositivo
está inscrito e obter uma lista de tags disponíveis.

Use a API **getTags** a seguir para obter uma lista de tags
disponíveis as quais o dispositivo podem assinar.

```
// Get a list of available tags to which the device can subscribe
push.getTags(new MFPPushResponseListener<List<String>>(){  
   @Override
    public void onSuccess(List<String> tags) { 
   updateTextView("Retrieved available tags: " + tags);  
   System.out.println("Available tags are: "+tags);
   availableTags = tags;   
   subscribeToTag();   
  }    
  @Override    
  public void onFailure(MFPPushException ex) {
     updateTextView("Error getting available tags.. " + ex.getMessage());
  }
})  
```

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

## Cordova

Copie os fragmentos de códigos a seguir em seu aplicativo móvel para obter uma
lista de tags nas quais o dispositivo está inscrito e para obter uma lista de tags
disponíveis as quais o dispositivo pode assinar.

Recupere uma matriz de tags que estão disponíveis para assinatura.

```
//Get a list of available tags to which the device can subscribe
MFPPush.retrieveAvailableTags(function(tags) {
    alert(tags);
}, null);

```

```
//Get a list of available tags to which the device is subscribed.
MFPPush.getSubscriptionStatus(function(tags) {
    alert(tags);
}, null);
```

## Objective-C

Copie os fragmentos de códigos a seguir em seu aplicativo iOS desenvolvido usando
Objective-C para obter uma lista de tags nas quais o dispositivo está inscrito e para
obter uma lista de tags disponíveis as quais o dispositivo pode assinar.

Use a API **retrieveAvailableTags** a seguir para obter uma
lista de tags disponíveis as quais o dispositivo pode assinar.

```
//Get a list of available tags to which the device can subscribe 
[push retrieveAvailableTagsWithCompletionHandler:
^(IMFResponse *response, NSError *error){ 
 if (error){    
   [self updateMessage:error.description];  
 } else {
   [self updateMessage:@"Successfully retrieved available tags."];
 NSDictionary *availableTags = [[NSDictionary alloc]init];
 availableTags = [response tags];
[self.appDelegateVC updateMessage:availableTags.description];
}
}];
```
       
Use a API **retrieveSubscriptions** para obter uma
lista de tags nas quais o dispositivo está inscrito.


```
// Get a list of tags that to which the device is subscribed.
[push retrieveSubscriptionsWithCompletionHandler:
^(IMFResponse *response, NSError *error) {
  if (error){
     [self updateMessage:error.description];
   } else {
     [self updateMessage:@"Successfully retrieved subscriptions."];
 NSDictionary *subscribedTags = [[NSDictionary alloc]init];
subscribedTags = [response subscriptions];
[self.appDelegateVC updateMessage:subscribedTags.description];
}
}];
```

## Swift

A API **retrieveAvailableTagsWithCompletionHandler** retorna a lista de
identificações disponíveis as quais o dispositivo pode assinar. Depois que o dispositivo está inscrito em uma
identificação específica, ele pode receber qualquer notificação push enviada para essa
identificação.

Chame o serviço push para obter assinaturas para
uma tag.

Copie os fragmentos de códigos a seguir em seu aplicativo móvel Swift para obter uma
lista de tags disponíveis nas quais o dispositivo está inscrito e para obter uma lista de
tags disponíveis as quais o dispositivo pode assinar.


```
//Get a list of available tags to which the device can subscribe
push.retrieveAvailableTagsWithCompletionHandler({ (response, statusCode, error) -> Void in

    if error.isEmpty {

        print( "Response during retrieve tags : \(response)")
        print( "status code during retrieve tags : \(statusCode)")
    }
    else{
        print( "Error during retrieve tags \(error) ")
        Print( "Error during retrieve tags \n  - status code: \(statusCode) \n Error :\(error) \n")
    }
}
```

```
//Get a list of available tags to which the device is subscribed
push.retrieveSubscriptionsWithCompletionHandler { (response, statusCode, error) -> Void in
    if error.isEmpty {

        print( "Response during retrieving subscribed tags : \(response.description)")
        print( "status code during retrieving subscribed tags : \(statusCode)")
    }
    else {
        print( "Error during retrieving subscribed tags \(error) ")
        Print( "Error during retrieving subscribed tags \n  - status code: \(statusCode) \n Error :\(error) \n")
    }
}
```



