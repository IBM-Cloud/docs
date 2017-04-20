---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-04-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

**Importante: o serviço {{site.data.keyword.amafull}} foi substituído pelo serviço {{site.data.keyword.appid_full}}.**

# Autenticando usuários com um provedor de identidade customizado
{: #custom-id}


Crie um provedor de identidade customizado que use o serviço {{site.data.keyword.amafull}} e implemente sua própria lógica para coletar e validar credenciais. Um provedor de identidade customizado é um aplicativo da web que expõe uma interface RESTful. É
possível hospedar o provedor de identidade customizado no local ou no {{site.data.keyword.Bluemix}}. O único requisito é que o provedor
de identidade customizado deve ser acessível a partir da Internet pública para que seja possível se comunicar com o serviço {{site.data.keyword.amashort}}.

## Fluxo de solicitação de identidade customizada do {{site.data.keyword.amashort}}
{: #custom-id-ovr}


### Fluxo de solicitação do cliente do {{site.data.keyword.amashort}}
 O diagrama a seguir demonstra como o {{site.data.keyword.amashort}} integra um provedor de identidade customizado.

![Fluxograma da solicitação](images/mca-sequence-custom.jpg)

* Use o {{site.data.keyword.amashort}} SDK para fazer uma solicitação para seus recursos de backend que são protegidos com o {{site.data.keyword.amashort}} server SDK.
* O {{site.data.keyword.amashort}} server SDK detecta uma solicitação não autorizada e retorna HTTP 401 e o escopo de autorização.
* O {{site.data.keyword.amashort}} client SDK detecta automaticamente o HTTP 401 e inicia o processo de autenticação.
* O SDK do cliente {{site.data.keyword.amashort}} entra em contato com o serviço {{site.data.keyword.amashort}} e solicita
um cabeçalho de autorização.
* O serviço {{site.data.keyword.amashort}} se comunica com o provedor de identidade customizado para iniciar o processo de autenticação.
* O provedor de identidade customizado retorna um desafio de autenticação para o serviço {{site.data.keyword.amashort}}.
* O serviço {{site.data.keyword.amashort}} retorna o desafio de autenticação para o {{site.data.keyword.amashort}} client SDK.
* O {{site.data.keyword.amashort}} client SDK delega a autenticação a uma classe customizada que você criou. Você é responsável por coletar credenciais e fornecê-las de volta para o {{site.data.keyword.amashort}} client SDK.
* Depois que o desenvolvedor fornece credenciais para o {{site.data.keyword.amashort}} SDK, elas são enviadas ao serviço {{site.data.keyword.amashort}} como uma resposta de segurança de autenticação.
* O serviço {{site.data.keyword.amashort}} valida a resposta do desafio de autenticação com o provedor de identidade customizado.
* Se a validação for bem-sucedida, o serviço {{site.data.keyword.amashort}} irá gerar um cabeçalho de autorização e o retornará para o {{site.data.keyword.amashort}} client SDK. O cabeçalho de autorização contém dois tokens: um token de acesso contendo informações de permissões de acesso e um token de ID contendo informações sobre o usuário, o dispositivo e o aplicativo atuais.
* Desse ponto em diante, todas as solicitações feitas com o {{site.data.keyword.amashort}} client SDK terão um cabeçalho de autorização recém-obtido.
* O {{site.data.keyword.amashort}} client SDK reenvia automaticamente a solicitação original que acionou o fluxo de autorização.
* O {{site.data.keyword.amashort}} server SDK extrai o cabeçalho de autorização da solicitação, valida-o com o serviço {{site.data.keyword.amashort}} e concede acesso a um recurso de backend.

### {{site.data.keyword.amashort}} Fluxo de
solicitação de aplicativo da Web
{: #mca-custom-web-sequence}

O aplicativo da Web {{site.data.keyword.amashort}}
fluxo de pedido é semelhante ao fluxo do cliente móvel. Entretanto, o {{site.data.keyword.amashort}} protege o aplicativo da web, em vez de um recurso de backend do {{site.data.keyword.Bluemix_notm}}.

  * A solicitação inicial é enviada pelo aplicativo da
Web (de um formulário de login, por exemplo).
  * O redirecionamento final é para a área protegida do aplicativo da Web em si, em vez de backend do recurso protegido.

## Entendendo os provedores de identidade customizados
{: #custom-id-about}

Com um provedor de identidade customizado, é possível fornecer desafios de autenticação customizados para serem enviados para o cliente. É possível customizar totalmente o fluxo de autenticação.

Ao criar um provedor de identidade customizado, será possível:

1. Customize um desafio de autenticação a ser enviado
pelo serviço {{site.data.keyword.amashort}} para o
aplicativo cliente móvel ou da Web. Um desafio de autenticação é um objeto JSON que contém dados customizados. O cliente pode usar esses dados customizados para customizar os fluxos de autenticação.

  Exemplo de um desafio de autenticação customizado:

	```JavaScript
	{
		status: "challenge",
		challenge: {
			message:"Enter username and password",
			retriesLeft: 2,
			minUsernameLenth: 8
		}
	}
	```
	{: codeblock}

1. Implemente qualquer fluxo de coleção de credenciais customizado no cliente, incluindo a autenticação de várias etapas e de vários formulários. Da mesma forma que para o desafio de autenticação customizado, deve-se projetar a estrutura de uma resposta de desafio de autenticação customizada.

  Exemplo de uma resposta de segurança de autenticação customizada enviada pelo cliente:

	```JavaScript
	{
		username:"bob.smith",
		password:"abcd1234",
		pincode:"1234"
	}
	```
	{: codeblock}

1. Implemente a lógica customizada de validação da resposta de desafio de autenticação fornecida.

1. Defina um objeto de identidade do usuário customizado que contém as propriedades customizadas necessárias. Existe um exemplo de um
objeto de identidade do usuário customizado que é obtido pelo cliente após a autenticação bem-sucedida:

	```JavaScript
	{
		username:"bob.smith",
		displayName:"Bob Smith",
		attributes:{
			age: 30,
			accountNumber: 12345,
			lastLogin: "Sept 1st, 2015"
		}
	}
	```
	{: codeblock}

### Implementação de amostra do provedor de identidade customizado
{: #custom-sample}

Use qualquer uma das implementações de amostra Node.js a seguir de um provedor de identidade customizado como uma referência ao desenvolver seu provedor de identidade customizado. Faça download do código do aplicativo completo dos repositórios GitHub.

 * [Amostra
simples ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample){: new_window}
 * [Amostra avançada ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management){: new_window}

## Comunicação típica entre o servidor {{site.data.keyword.amashort}} e um provedor de identidade customizado
{: #custom-id-comm}

1. O serviço {{site.data.keyword.amashort}} envia uma solicitação `startAuthorization` para o provedor de identidade customizado.
1. O provedor de identidade customizado responde com um desafio de autenticação customizado a ser enviado para o cliente.
1. O serviço {{site.data.keyword.amashort}} envia o desafio de autenticação customizado que é recebido do provedor de identidade
customizado para o cliente e, finalmente, recebe uma resposta de segurança de autenticação do cliente.
1. O serviço {{site.data.keyword.amashort}} envia uma solicitação `handleChallengeAnswer` com a resposta do desafio de autenticação para o provedor de identidade customizado.
1. O provedor de identidade customizado verifica a resposta de segurança de autenticação e responde com uma resposta de sucesso, contendo as informações de identificação do usuário.
1. Opcionalmente, o provedor de identidade customizado pode fornecer mais desafios depois de receber uma resposta de segurança do cliente. O envio de vários desafios permite um
processo de autenticação de várias etapas.

## Stateful versus stateless
{: #custom-id-state}

Por padrão, o provedor de identidade customizado é considerado um aplicativo stateless. Em alguns casos, o provedor de identidade customizado pode precisar armazenar o estado que está relacionado ao processo de autenticação. Um caso de uso de exemplo é uma autenticação de várias etapas, em que o provedor de identidade customizado precisa armazenar o resultado da primeira etapa de autenticação, antes de continuar na próxima etapa. Para suportar a funcionalidade stateful, um provedor de identidade customizado deve gerar um stateID e fornecê-lo na resposta para o serviço {{site.data.keyword.amashort}}. O serviço {{site.data.keyword.amashort}} deve passar o stateID em solicitações subsequentes pertencentes ao processo de autenticação do cliente.

## Domínio customizado
{: #custom-id-custom}

Um provedor de identidade customizado suporta um domínio de autenticação customizado. Para manipular desafios de autenticação recebidos, crie e registre uma instância do `AuthenticationDelegate`/ `AuthenticationListener` em seu aplicativo cliente. Defina o nome do domínio de autenticação customizado ao configurar um provedor de identidade customizado no painel do {{site.data.keyword.amashort}}. A região identifica a instância de serviço específica {{site.data.keyword.amashort}} de uma solicitação recebida.

## Próximas etapas
{: #next-steps}

* [Criando um provedor de identidade customizado](custom-auth-identity-provider.html)
* [Configurando o {{site.data.keyword.amashort}} para autenticação customizada](custom-auth-config-mca.html)
* [Configurando a autenticação customizada para Android](custom-auth-android.html)
* [Configurando a autenticação customizada para iOS (Swift SDK)](custom-auth-ios-swift-sdk.html)
* [Configurando a autenticação customizada para Cordova](custom-auth-cordova.html)
