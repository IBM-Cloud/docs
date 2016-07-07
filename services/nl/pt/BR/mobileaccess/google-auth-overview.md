---

copyright:
  years: 2015, 2016

---
{:screen:  .screen}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}

# Autenticando usuários com as credenciais do Google
{: #google-auth}

*Última atualização: 15 de junho de 2016*

É possível configurar o serviço {{site.data.keyword.amashort}} para proteger recursos usando o Google como provedor de identidade. Seu aplicativo móvel pode então usar suas credenciais do Google para autenticação.
{:shortdesc}

**Importante:** não é necessário instalar separadamente o SDK do Google. O Google SDK é instalado automaticamente por gerenciadores de dependência quando você configura o {{site.data.keyword.amashort}} client SDK.

## Fluxo do {{site.data.keyword.amashort}}
{: #google-auth-overview}

Veja o diagrama simplificado a seguir para entender como o {{site.data.keyword.amashort}} se integra ao Google para autenticação.

![image](images/mca-sequence-google.jpg)

1. Use o {{site.data.keyword.amashort}} SDK para fazer uma solicitação para seus recursos de backend que são protegidos com o {{site.data.keyword.amashort}} server SDK.
* O {{site.data.keyword.amashort}} server SDK detecta a solicitação não autorizada e retorna um código HTTP 401 e um escopo de autorização.
* O {{site.data.keyword.amashort}} client SDK detecta automaticamente o código HTTP 401 e inicia o processo de autenticação.
* O {{site.data.keyword.amashort}} client SDK entra em contato com o serviço {{site.data.keyword.amashort}} e pede para emitir um cabeçalho de autorização.
* O serviço {{site.data.keyword.amashort}} solicita que o cliente primeiro autentique com o Google fornecendo um desafio de autenticação.
* O {{site.data.keyword.amashort}} client SDK usa o Google SDK para iniciar o processo de autenticação. Após uma autenticação bem-sucedida, o SDK do Google retorna um token de acesso do Google.
* O token de acesso do Google é considerado uma resposta ao desafio de autenticação. O token é enviado ao serviço {{site.data.keyword.amashort}}.
* O serviço valida a resposta ao desafio de autenticação com servidores Google.
* Se a validação for bem-sucedida, o serviço {{site.data.keyword.amashort}} irá gerar um cabeçalho de autorização e o retornará para o {{site.data.keyword.amashort}} client SDK. O cabeçalho de autorização contém dois tokens: um token de acesso que contém informações de permissões de acesso e um token de ID que contém informações sobre o usuário, dispositivo e aplicativo atuais.
* Desse ponto em diante, todas as solicitações feitas por meio do {{site.data.keyword.amashort}} client SDK terão um cabeçalho de autorização recém-obtido.
* O {{site.data.keyword.amashort}} client SDK reenvia automaticamente a solicitação original que acionou o fluxo de autorização.
* O {{site.data.keyword.amashort}} server SDK extrai o cabeçalho de autorização da solicitação, valida-o com o serviço {{site.data.keyword.amashort}} e concede acesso a um recurso de backend.



## Próximas Etapas
{: #google-auth-nextsteps}

* [Ativando a autenticação do Google para apps Android](google-auth-android.html)
* [Ativando a autenticação do Google para apps iOS (Swift SDK)](google-auth-ios-swift-sdk.html)
* [Ativando a autenticação do Google para apps iOS (Objective-C SDK)](google-auth-ios.html)
* [Ativando a autenticação do Google para apps Cordova](google-auth-cordova.html)

