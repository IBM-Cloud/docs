---

copyright:
  years: 2015, 2016

---

# Informações Iniciais
{: #getting-started}
Para obter uma introdução sobre o {{site.data.keyword.amashort}}, é possível incluir o serviço {{site.data.keyword.amashort}} em um aplicativo {{site.data.keyword.Bluemix}} existente, ou é possível criar um novo app com o modelo.  

## Criando uma instância do serviço {{site.data.keyword.amashort}}
{: #service-instance}

É possível criar uma nova instância de um serviço {{site.data.keyword.amashort}} a partir do catálogo do {{site.data.keyword.Bluemix}}.  Se você não usar o modelo para criar um novo backend móvel, deverá configurar o SDK do servidor em seu backend existente.


  * **Novo app**: as instruções nas seções a seguir descrevem como criar um novo app que cria um backend móvel e protege
com o {{site.data.keyword.amashort}} Server SDK. Clique no modelo do **MobileFirst Services Starter** para criar um novo aplicativo com o serviço {{site.data.keyword.amashort}}.
  * **App existente**: clique no ícone do {{site.data.keyword.amashort}} e crie uma nova instância de serviço que esteja ligada a um aplicativo existente. Para
configurar o novo server SDK em seu app existente, veja [Protegendo recursos em nuvem](protecting-resources.html).


## Criando um backend móvel com o modelo do MobileFirst Services Starter
{: #create-backend}
Ao usar o MobileFirst Services Starter, você obtém uma instância de um tempo de execução do Node.js que é executada no IBM {{site.data.keyword.Bluemix_notm}} para implementar sua lógica de backend customizada. Um conjunto de serviços móveis principais que fornecem funções de segurança, dados, push e monitoramento está ligado a esse app Node.js. Depois que o {{site.data.keyword.Bluemix_notm}} Node.js for criado, é possível configurar seu ambiente de desenvolvimento e começar a usar os SDKs de serviços móveis do {{site.data.keyword.Bluemix_notm}}. É possível usar os SDKs para acessar os serviços que estão ligados ao seu app em nuvem com chamadas API simples.

1. No catálogo do {{site.data.keyword.Bluemix_notm}}, acesse a seção **Modelo** e clique em **MobileFirst Services Starter**.
1. Inclua informações sobre seu backend móvel, incluindo o espaço, o nome, o host e o plano de serviço.
1. Clique em **CRIAR**.



## Próximas Etapas
{: #next-steps}
Vários terminais do aplicativo Node.js que você criou com o modelo são protegidos com {{site.data.keyword.amashort}}. Para saber mais sobre o aplicativo backend móvel padrão, veja [bms-hellotodo-strongloop](https://github.com/ibm-bluemix-mobile-services/bms-hellotodo-strongloop).

É possível configurar seu app móvel para usar o {{site.data.keyword.amashort}} SDK.  Depois de configurar o SDK, é possível iniciar a configuração da autenticação e o monitoramento do seu app.  Siga as instruções de sua plataforma de desenvolvimento do dispositivo móvel:

* [Android](getting-started-android.html)
* [iOS (Swift SDK)](getting-started-ios.html)
* [iOS (Objective-C SDK)](getting-started-ios.html)
* [Cordova](getting-started-cordova.html)
