---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Autenticando usuários com as credenciais do Google
{: #google-auth}

É possível configurar o serviço {{site.data.keyword.amafull}} para proteger recursos usando o Google como provedor de identidade. Os usuários do seu aplicativo móvel ou da Web podem usar suas
credenciais do Google para autenticação.
{:shortdesc}

**Importante**: não é necessário instalar separadamente o client SDK fornecido pelo Google. O Google SDK é instalado automaticamente por gerenciadores de dependência quando você configura o {{site.data.keyword.amashort}} client SDK.

## Fluxo de solicitação do {{site.data.keyword.amashort}}
{: #google-auth-overview}

### Fluxo de solicitação do cliente

Veja o diagrama a seguir para entender como o {{site.data.keyword.amashort}} integra-se ao Google para autenticação.

![Diagrama do fluxo de solicitação do cliente](images/mca-sequence-google.jpg)

* Use o {{site.data.keyword.amashort}} SDK para fazer uma solicitação para seus recursos de backend que são protegidos com o {{site.data.keyword.amashort}} server SDK.
* O {{site.data.keyword.amashort}} server SDK detecta a solicitação não autorizada e retorna um código HTTP 401 e um escopo de autorização.
* O {{site.data.keyword.amashort}} client SDK detecta automaticamente o código HTTP 401 e inicia o processo de autenticação.
* O SDK do cliente {{site.data.keyword.amashort}} entra em contato com o serviço {{site.data.keyword.amashort}} e solicita
um cabeçalho de autorização.
* O serviço {{site.data.keyword.amashort}} solicita que o cliente primeiro autentique com o Google fornecendo um desafio de autenticação.
* O {{site.data.keyword.amashort}} client SDK usa o Google SDK para iniciar o processo de autenticação. Após uma autenticação bem-sucedida, o SDK do Google retorna um token de acesso do Google.
* O token de acesso do Google é considerado uma resposta ao desafio de autenticação. O token é enviado ao serviço {{site.data.keyword.amashort}}.
* O serviço valida a resposta ao desafio de autenticação com servidores Google.
* Se a validação for bem-sucedida, o serviço {{site.data.keyword.amashort}} irá gerar um cabeçalho de autorização e o retornará para o {{site.data.keyword.amashort}} client SDK. O cabeçalho de autorização contém dois tokens: um token de acesso que contém informações de permissões de acesso e um token de ID que contém informações sobre o usuário, dispositivo e aplicativo atuais.
* Desse ponto em diante, todas as solicitações feitas por meio do {{site.data.keyword.amashort}} client SDK terão um cabeçalho de autorização recém-obtido.
* O {{site.data.keyword.amashort}} client SDK reenvia automaticamente a solicitação original que acionou o fluxo de autorização.
* O {{site.data.keyword.amashort}} server SDK extrai o cabeçalho de autorização da solicitação, valida-o com o serviço {{site.data.keyword.amashort}} e concede acesso a um recurso de backend.


### Fluxo de solicitação de aplicativo da web {{site.data.keyword.amashort}}
{: #mca-google-web-sequence}
O fluxo de solicitação de aplicativo da web {{site.data.keyword.amashort}} é semelhante ao fluxo do cliente móvel. Entretanto, o {{site.data.keyword.amashort}} protege o aplicativo da web, em vez de um recurso de backend do {{site.data.keyword.Bluemix_notm}}.

  * A solicitação inicial é enviada pelo aplicativo da web (a partir de um formulário de login, por exemplo).
  * O redirecionamento final é para a área protegida do próprio aplicativo da web, em vez do recurso protegido de backend.



## Próximas Etapas
{: #google-auth-nextsteps}

* [Ativando a autenticação do Google para apps Android](google-auth-android.html)
* [Ativando a autenticação do Google para apps iOS (Swift SDK)](google-auth-ios-swift-sdk.html)
* [Ativando a autenticação do Google para apps Cordova](google-auth-cordova.html)
