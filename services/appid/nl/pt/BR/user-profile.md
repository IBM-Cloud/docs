---

copyright:
  years: 2017
lastupdated: "2017-03-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# Entendendo perfis de usuários
{: #user-profile}

Um perfil de usuário é uma entidade que é armazenada e mantida pelo {{site.data.keyword.appid_short}}. O perfil retém os atributos e a identidade de um
usuário e pode ser anônimo ou vinculado a uma identidade gerenciada por um provedor de identidade.
{:shortdesc}

O {{site.data.keyword.appid_short_notm}} fornece uma API para efetuar login, seja anonimamente ou por autenticação com um IdP Connect OpenId (OIDC); veja [Configurando provedores de identidade](/docs/services/appid/identity-providers.html#setting-up-idp) O terminal de API de atributo de perfil do usuário é um recurso protegido pelo token de acesso gerado pelo {{site.data.keyword.appid_short_notm}} durante o processo de login e de autorização.


## Armazenando, lendo e excluindo atributos do usuário
{: #storing-data}



O {{site.data.keyword.appid_short_notm}} fornece uma <a href="https://appid-profiles.ng.bluemix.net/swagger-ui/index.html#/" target="_blank">API de REST <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> para executar operações CRUD em atributos do usuário, bem como um SDK para <a href="https://github.com/ibm-cloud-security/appid-clientsdk-android" target="_blank">Android <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> e clientes móveis do <a href="https://github.com/ibm-cloud-security/appid-clientsdk-swift" target="_blank">Swift <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.


## Identidade do OAuth
{: #oauth}

Ao chamar a API de login do OAuth, o {{site.data.keyword.appid_short_notm}} usa protocolos do OAuth 2.0 e do OIDC para autorizar e autenticar o
responsável pela chamada com um provedor de identidade selecionado. Uma vez autenticada, a identidade será associada com um
registro do usuário do {{site.data.keyword.appid_short_notm}}. O {{site.data.keyword.appid_short_notm}} retorna um token de acesso que pode ser
usado para acessar os atributos do usuário e um token de identidade que retém as informações de identidade fornecidas pelo provedor de identidade. O mesmo registro
do usuário e seus atributos poderão ser acessados novamente por meio de qualquer cliente que se autenticar com essa mesma identidade.


## Usuário Anônimo
{: #anonymous}

Quando você efetuar login anonimamente, o {{site.data.keyword.appid_short_notm}} criará um registro do usuário ad hoc que será marcado como anônimo. O
{{site.data.keyword.appid_short_notm}} retorna acesso anônimo e tokens de identidade para o responsável pela chamada. Usando o token de acesso anônimo, o
aplicativo de usuário poderá criar, ler, atualizar, excluir atributos que estiverem armazenados no registro do usuário. Como um exemplo, um desenvolvedor pode criar
um aplicativo no qual um usuário pode começar imediatamente a incluir itens em um carrinho de compras sem precisar efetuar login.


## Usuário identificado
{: #identified}

Um usuário anônimo com uma identidade fornecida por um provedor de identidade pode se tornar um usuário identificado. O fluxo para mover de um usuário anônimo para um usuário identificado é esboçado nas etapas a seguir:

* O desenvolvedor passa o token de acesso anônimo para a API de login.
* O {{site.data.keyword.appid_short_notm}} autentica o responsável pela chamada com o provedor de identidade.
* O {{site.data.keyword.appid_short_notm}} localiza o registro do usuário anônimo definido pelo token de acesso e designa a identidade para ele.

    **Nota**: a identidade poderá ser designada ao registro anônimo somente se a mesma identidade ainda não foi designada a outro usuário. Se a
identidade já estiver associada a outro usuário do {{site.data.keyword.appid_short_notm}}, os tokens de acesso e de identidade conterão informações de
registro desse usuário e fornecerão acesso aos seus atributos. O usuário anônimo anterior e os seus atributos não serão acessíveis por meio do novo token de
acesso. Até o token expirar, as informações ainda poderão ser acessadas através do token de acesso anônimo. O desenvolvedor poderá escolher como ele deseja mesclar os
atributos anônimos do usuário anônimo e o usuário conhecido.

* Os novos tokens de acesso e de identidade recebidos do {{site.data.keyword.appid_short_notm}} apontam para o usuário conhecido e o token de
identidade contém as informações públicas que são recebidas do provedor de identidade.
* Os tokens anônimos tornam-se inválidos para o usuário.

Os atributos que eram contidos por esse usuário enquanto ele estava anônimo serão acessíveis com o novo token de acesso. Novos tokens podem ser incluídos, mudados
ou excluídos. Ao avançarem, o usuário e os seus atributos serão resolvidos e acessíveis quando efetuarem login com a mesma identidade de qualquer cliente.


## Separação e criptografia de dados
{: #data}

O {{site.data.keyword.appid_short_notm}} armazena e criptografa atributos de perfil do usuário. Como um serviço de múltiplos locatários, cada locatário
tem uma chave de criptografia designada e os dados do usuário em cada locatário são criptografados com apenas essa chave do locatário.

O {{site.data.keyword.appid_short_notm}} assegura que as informações privadas sejam criptografadas antes de serem armazenadas.
