---

copyright:
  years: 2015, 2016

---

# Sobre {{site.data.keyword.amashort}}
{: #mca-overview}

O serviço {{site.data.keyword.amafull}} fornece serviços de autenticação e monitoramento para aplicativos móveis que acessam recursos em nuvem hospedados no {{site.data.keyword.Bluemix_notm}}.

É possível usar o serviço {{site.data.keyword.amashort}} para proteger os aplicativos Node.js e Liberty for Java&trade; que são hospedados no {{site.data.keyword.Bluemix_notm}} com vários tipos de autenticação. Ao instrumentar seus aplicativos móveis com o {{site.data.keyword.amashort}} SDK, é possível usar os recursos de autenticação fornecidos pelo serviço {{site.data.keyword.amashort}}. Logs de monitoramento e do lado do cliente são reunidos automaticamente e enviados para o serviço {{site.data.keyword.amashort}} sob demanda. Use o painel do {{site.data.keyword.amashort}} para configurar os vários tipos de autenticação e ver dados que são reunidos pelo SDK do lado do cliente.

**Nota**: o serviço {{site.data.keyword.amashort}} era conhecido anteriormente como Advanced Mobile Access.

## Componentes
do {{site.data.keyword.amashort}}
{: #components}

* **Painel do {{site.data.keyword.amashort}}**: configure vários tipos de autenticação e monitore desempenho, analítica, estatísticas de uso e logs do dispositivo do aplicativo móvel.
* **{{site.data.keyword.amashort}} Client SDK**: instrumente aplicativos móveis para usar a funcionalidade do {{site.data.keyword.amashort}}. As plataformas suportadas são: iOS 8+, Android 4+, Cordova.
* **{{site.data.keyword.amashort}} Server SDK**: proteja os recursos que estão hospedados no {{site.data.keyword.Bluemix_notm}}. Atualmente, os tempos de execução suportados são Node.js e Liberty for Java&trade;.

## Tipos de autenticação
{: #authtypes}
É possível usar os tipos de autenticação a seguir em seu app móvel:
* **Facebook**: use o Facebook como um provedor de identidade. Os usuários efetuarão login no app móvel com suas credenciais do Facebook.
* **Google**: use o Google como um provedor de identidade. Os usuários efetuarão login no app móvel com suas credenciais do Google+.
* **Customizado**: crie seu próprio provedor de identidade. Você controlará totalmente que tipo de informações serão reunidas e validadas.

## Visão geral da arquitetura do {{site.data.keyword.amashort}}
{: #architecture}

![image](images/mca-overview.jpg)

* Proteja seus recursos em nuvem (aplicativos Node.js) com o {{site.data.keyword.amashort}} Server SDK.
* Use a classe de `solicitação` fornecida pelo {{site.data.keyword.amashort}} Client SDK para se comunicar com seus recursos em nuvem protegidos.
* O {{site.data.keyword.amashort}} Server SDK detecta uma solicitação não autorizada e retorna o desafio de autorização HTTP 401.
* O {{site.data.keyword.amashort}} Client SDK detecta o desafio de autorização HTTP 401 e inicia automaticamente o processo de autenticação com o serviço {{site.data.keyword.amashort}}.
* A autenticação do Facebook, do Google ou Customizada é usada para autenticar.
* Após a autenticação bem-sucedida, o {{site.data.keyword.amashort}} retorna um token de autorização.
* O {{site.data.keyword.amashort}} Client SDK inclui automaticamente o token de autorização na solicitação original e a envia novamente para o recurso em nuvem.
* O {{site.data.keyword.amashort}} Server SDK extrai o accessToken da solicitação e valida-o com o serviço {{site.data.keyword.amashort}}.
* O acesso é concedido.  A resposta é retornada para o aplicativo móvel.

## Fluxo de solicitação do {{site.data.keyword.amashort}}
{: #flow}
O diagrama a seguir descreve como uma solicitação flui do SDK para seu backend móvel e para os provedores de identidade.

![image](images/mca-sequence-overview.jpg)

1. Use o {{site.data.keyword.amashort}} SDK para fazer uma solicitação para seus recursos de backend que são protegidos com o {{site.data.keyword.amashort}} Server SDK.
* O {{site.data.keyword.amashort}} Server SDK detecta uma solicitação não autorizada e retorna HTTP 401 + escopo de autorização.
* O {{site.data.keyword.amashort}} Client SDK detecta automaticamente o HTTP 401 e inicia o processo de autenticação.
* O {{site.data.keyword.amashort}} Client SDK entra em contato com o serviço {{site.data.keyword.amashort}} e solicita a emissão de um cabeçalho de autorização.
* O serviço {{site.data.keyword.amashort}} solicita ao app cliente para se autenticar primeiro fornecendo um desafio de autenticação de acordo com o tipo de autenticação configurado atualmente.
* O {{site.data.keyword.amashort}} Client SDK:
   *  **Autenticação do Facebook ou do Google:** processa automaticamente o desafio de autenticação (para autenticação do Facebook ou do Google)
   * **Autenticação customizada**: obtém credenciais com base na lógica fornecida pelo desenvolvedor.
* Se a autenticação do Facebook ou do Google estiver configurada, o {{site.data.keyword.amashort}} Client SDK usará o SDK associado para obter tokens de acesso do Facebook ou do Google. Esses tokens servem como a resposta do desafio de autenticação.
* Se a autenticação Customizada estiver configurada, o desenvolvedor deverá obter a resposta do desafio de autenticação e fornecê-la para o {{site.data.keyword.amashort}} Client SDK.
* Depois que a resposta do desafio de autenticação é obtida, ela é enviada para o serviço {{site.data.keyword.amashort}}.
* O serviço valida a resposta do desafio de autenticação com um provedor de identidade respectivo (Facebook/Google/Customizado).
* Se a validação for bem-sucedida, o serviço {{site.data.keyword.amashort}} irá gerar um cabeçalho de autorização e o retornará para o {{site.data.keyword.amashort}} Client SDK. O cabeçalho de autorização contém dois tokens: um token de acesso contendo informações de permissões de acesso e um token de ID contendo informações sobre o usuário atual, o dispositivo ou o aplicativo.
* Desse ponto em diante, todas as solicitações feitas com o {{site.data.keyword.amashort}} Client SDK terão um cabeçalho de autorização recém-obtido.
* O {{site.data.keyword.amashort}} Client SDK reenvia automaticamente a solicitação original que acionou o fluxo de autorização.
* O {{site.data.keyword.amashort}} Server SDK extrai o cabeçalho de autorização da solicitação, valida o cabeçalho com o serviço {{site.data.keyword.amashort}} e concede acesso a um recurso de backend.
