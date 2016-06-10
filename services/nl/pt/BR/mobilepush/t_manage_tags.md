---

copyright:
 years: 2015, 2016

---

# Gerenciando Identificações
{: #manage_tags}

Use o painel Push para criar e excluir tags para
seu aplicativo e depois inicializar notificações baseadas em
tag. A notificação baseada em tag é recebida no dispositivo que está inscrito na tag.


## Criando marcações
{: #create_tags}

Notificações baseadas em tag são mensagens de
notificação que se destinam a todos os dispositivos inscritos
em uma tag específica. Cada dispositivo pode se inscrever em
qualquer número de tags. Quando uma tag é excluída, todas as informações associadas a
ela, incluindo seus assinantes e dispositivos são excluídos. Nenhum cancelamento de
assinatura automático é necessário para essa tag, uma vez que ela não existe mais e
nenhuma ação adicional é necessária no lado do cliente.

1. No painel Push, selecione a guia **Tags**.
1. Clique no botão + **Criar tag**.   

   a. No campo **Nome**, insira o nome da tag. Por exemplo, "coupons".
   
   b. No campo **Descrição**, insira uma descrição da tag.
   
   c. Clique em  **Salvar**.
   
1. Na área **Fragmentos de códigos**,
selecione a plataforma para seu aplicativo móvel.
1. Modifique os fragmentos de códigos para manipular erros e
depois copie os fragmentos de códigos para cada tag em seu
aplicativo móvel.

## Excluindo marcações
{: #delete_tags}

1. Na guia **Tag**, selecione a tag que deseja
excluir e clique no ícone de exclusão.
1. Clique em **OK**.

## Editando uma descrição de tag
{: #edit_tags}

1. Na guia **Tag**, selecione a tag que deseja
editar.
1. Clique no ícone de edição.
1. Edite a descrição d tag e clique no botão
**Salvar**.

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

# Assinando e removendo assinatura de tags
{: #Subscribe_tags}

Use os fragmentos de código a seguir para permitir que seus dispositivos obtenham
assinaturas, bem como assinem e cancelem a assinatura de uma tag.

## Android

Copie e cole este fragmento de código em seu
aplicativo móvel Android.

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

## Cordova

Copie e cole este fragmento de código em seu aplicativo móvel
Cordova.

```
var tag = "YourTag";
MFPPush.subscribe(tag, success, failure);
MFPPush.unsubscribe(tag, success, failure);
```

## Objective-C

Copie e cole este fragmento de código em seu aplicativo móvel
Objective-C.

Use a API **subscribeToTags** para assinar uma
identificação.

```
[push subscribeToTags:tags completionHandler:
^(IMFResponse *response, NSError *error) {
  if (error){
     [self updateMessage:error.description];
  }else{
      NSDictionary* subStatus = [[NSDictionary alloc]init];
      subStatus = [response subscribeStatus];
      [self updateMessage:@"Parsed subscribe status is:"];
      [self updateMessage:subStatus.description];
  }
}];
```

Use a API **unsubscribeFromTags** para cancelar a assinatura de uma
identificação.

```
[push unsubscribeFromTags:tags completionHandler:
^(IMFResponse *response, NSError *error) {
   if (error){
       [self updateMessage:error.description];
 } else {
       NSDictionary* subStatus = [[NSDictionary alloc]init];
       subStatus = [response unsubscribeStatus];
       [self updateMessage:subStatus.description];
  }
}];
```

## Swift

Copie e cole este fragmento de código em seu aplicativo móvel
Swift.

**Assinar tags disponíveis**

Use a API **subscribeToTags** para assinar uma
identificação.

```
push.subscribeToTags(tagsArray: tags) { (response: IMFResponse!, error: NSError!) -> Void in
	if (error != nil) { 
		//error while subscribing to tags
	} else {
		//successfully subscribed to tags var subStatus = response.subscribeStatus();
	}
} 
```

**Cancelar assinatura de tags**

Use a API **unsubscribeFromTags** para cancelar a assinatura de uma
identificação.

```
push.unsubscribeFromTags(response, completionHandler: { (response, statusCode, error) -> Void in

    if error.isEmpty {
        print( "Response during unsubscribed tags : \(response.description)")
        print( "status code during unsubscribed tags : \(statusCode)")
    }
    else {
        print( "Error during  unsubscribed tags \(error) ")
        print( "Error during unsubscribed tags \n  - status code: \(statusCode) \n Error :\(error) \n")
    }
}
```


# Usando notificações baseada em tag
{: #using_tags}


Notificações baseadas em tag são mensagens de
notificação que se destinam a todos os dispositivos inscritos
em uma tag específica. Cada dispositivo pode ser inscrito em qualquer número de tags. Esta seção
descreve como enviar notificações baseadas em tag. As assinaturas são mantidas pela
instância do Bluemix do serviço de notificação push. Quando uma tag é excluída, todas as informações associadas a
ela, incluindo seus assinantes e dispositivos são excluídos. Nenhum cancelamento de
assinatura automático é necessário para essa tag, uma vez que ela não existe mais e
nenhuma ação adicional é necessária no lado do cliente.

**Antes de começar**

Crie tags na tela **Tag**. Para obter informações sobre como
criar tags, consulte
[Criando tags](t_manage_tags.html).

1. A partir do painel **Notificação push**,
clique na guia **Notificações**.
1. Selecione a opção **Tags** para enviar notificações baseadas
em tag.
1. No campo **Procurar** tags, procure pelas tags que deseja
usar e clique no botão
**+Incluir**.![Tela
Notificações](images/tag_notification.jpg)
1. Acesse a área **Criar suas notificações **, e
no campo **Texto da mensagem**,
insira o texto que deseja enviar em sua notificação.
1. Clique no botão **Enviar**.
