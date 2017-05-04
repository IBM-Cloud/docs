---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# Como funciona
{: #about}

É possível aprender sobre os componentes, a arquitetura e o fluxo de solicitação que o {{site.data.keyword.appid_short_notm}} usa.
{:shortdesc}


É possível usar o serviço das maneiras a seguir:

* Para incluir autenticação em seus aplicativos móveis e da web
* Para conceder acesso a recursos de backend protegidos e aplicativos da web
* Para proteger aplicativos Node.js e Swift que estão hospedados no {{site.data.keyword.Bluemix_notm}}
* Para armazenar dados do usuário, como preferências de app ou informações de seus perfis sociais públicos
* Para usar dados armazenados para construir experiências personalizadas de app
* Para proteger recursos para usuários autenticados e anônimos

**Nota**: os protocolos implementados são totalmente compatíveis com o OpenID Connect (OIDC).


## Componentes
{: #components}

* Painel - Faça download de amostras de migração, veja logs de atividade, configure vários tipos de autenticação e provedores de identidade
* SDK do cliente - Compile apps móveis e da web que usem o serviço para implementar a autenticação do usuário
    * Pré-requisitos para Android: API 25 ou superior, Java 8.x, ferramentas do Android SDK 25.2.5 ou superior, Android SDK Platform Tools 25.0.3 ou superior,
Android Build Tools versão 25.0.2
    * Pré-requisitos para iOS: iOS9 ou superior, MacOS 10.11.5, Xcode 8,2
* SDK do servidor - Proteja os recursos que são hospedados no {{site.data.keyword.Bluemix_notm}}
    * Os tempos de execução suportados são Node.js e Swift

## Visão geral da arquitetura
{: #architecture}

Com o {{site.data.keyword.appid_short_notm}} é possível incluir um nível de segurança em seus aplicativos solicitando aos usuários para se conectarem. Também
é possível usar o servidor SDK para proteger os seus recursos de backend.

O diagrama a seguir mostra uma visão geral de como o serviço do {{site.data.keyword.appid_short_notm}} funciona.

![{{site.data.keyword.appid_short_notm}} diagrama de arquitetura](/images/appid_architecture2.png)

Figura 1. Diagrama de arquitetura do {{site.data.keyword.appid_short_notm}}

<dl>
  <dt> Client SDK </dt>
    <dd> O SDK do cliente fornece uma classe de solicitação para se comunicar com os seus recursos em nuvem. O SDK do cliente automaticamente inicia o processo de
autenticação quando ele detecta um desafio de autorização.</dd>
  <dt> Bluemix </dt>
    <dd>  O SDK do servidor extrai o token de acesso da solicitação e a valida com o {{site.data.keyword.appid_short_notm}}. Após a autenticação bem-sucedida,
o {{site.data.keyword.appid_short_notm}} retorna tokens de autorização e identidade para o seu aplicativo. </dd>
  <dt> Provedores de identidade </dt>
    <dd> É possível configurar o Facebook, o Google ou ambos para autenticar os seus apps. </dd>
</dl>


## Fluxo de Pedido
{: #request}

O diagrama a seguir descreve como uma solicitação flui do SDK do cliente para seu aplicativo backend e provedores de identidade.

![{{site.data.keyword.appid_short_notm}} fluxo de solicitação](/images/appidflow.png)


* Use o SDK do cliente {{site.data.keyword.appid_short_notm}} para fazer uma solicitação aos seus recursos de backend que são protegidos
com o SDK do servidor {{site.data.keyword.appid_short_notm}}.
* O {{site.data.keyword.appid_short_notm}} SDK do servidor detecta uma solicitação não autorizada e retorna um HTTP 401 e escopo de autorização.
* O SDK do cliente detecta automaticamente o HTTP 401 e inicia o processo de autenticação.
* Quando o SDK do cliente entra em contato com o serviço, o SDK do servidor retorna o widget de login se mais de um provedor de identidade é configurado. {{site.data.keyword.appid_short_notm}} chama o provedor de identidade e apresenta o formulário de login para esse provedor ou retorna um código de concessão que permite autenticar se nenhum provedor de identidade é configurado.
* {{site.data.keyword.appid_short_notm}} solicita que o aplicativo do cliente autentique fornecendo um desafio de autenticação.
* Se o Facebook ou o Google for configurado, e o usuário efetuar login, a autenticação será manipulada pelo respectivo provedor de identidade OAuth Flow.
* Se a autenticação terminar com o mesmo código de concessão, o código será enviado para o terminal do token. O terminal retorna dois tokens: um de acesso e um de identidade. Desse ponto em diante, todas as solicitações feitas com o SDK do cliente terão um cabeçalho de autorização recém-obtido.
* O SDK do cliente reenvia automaticamente a solicitação original que acionou o fluxo de autorização.
* O SDK do servidor extrai o cabeçalho de autorização da solicitação, valida o cabeçalho com o serviço e concede acesso a um recurso de backend.
