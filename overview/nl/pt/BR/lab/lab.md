---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-03-17"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# IBM Cloud Identity and Access Management (IAM)
{: #iam_overview}

O IBM Cloud IAM fornece uma maneira segura de gerenciar as identidades do usuário e de serviço e de acessar recursos para estas identidades. É possível visualizar e gerenciar usuários na conta ou na organização, dependendo das opções de acesso que você estiver autorizado a gerenciar. É possível executar todas as operações para usuários, incluindo convidar e gerenciar usuários e suas funções designadas e as contas ou as organizações, ou ambos, que eles podem acessar. Como um proprietário da conta, é possível gerenciar as opções de acesso das quais você e os usuários são membros, independentemente da função, na conta atual.

O gerenciamento de identidade inclui o seguinte:
 * Gerenciamento de usuários 
   * criar, excluir e atualizar informações do usuário
   * gerenciamento de chave API
   * criação, atualização e troca de token
   * autenticação de identidade do usuário
 * Gerenciamento de ID de serviço
   * criar, excluir e atualizar informações do usuário
   * gerenciamento de chave API
   * criação, atualização e troca de token
   * autenticação de identidade de serviço
   
   
O gerenciamento de acesso inclui o seguinte:
 * Gerenciamento de Diretiva
   * criar, excluir e atualizar políticas
 * Decisões de acesso aos recursos
 
## Visão geral da identidade
{: #identity}

O Cloud IAM Token Service é o serviço de autenticação do IBM Cloud que é construído de acordo com os padrões abertos especificados pelo [OAuth 2.0]( https://tools.ietf.org/html/rfc6749), [JWT](https://tools.ietf.org/html/rfc7519), [Perfil do JWT](https://tools.ietf.org/html/rfc7523) e [JWKS](https://tools.ietf.org/html/rfc7517).

Um foco do Token Service é a autenticação de desenvolvedores, de operadores e de administradores para o IBM Cloud Platform. Para essa autenticação, o Token Service é conectado ao sistema IBMid para autenticar usuários e, em ambientes dedicados e locais, ele pode ser conectado a um sistema de autenticação escolhido pelo cliente, como o LDAP. 

Para recuperar um token do IAM, é possível usar tipos de concessão padrão do OAuth 2.0, como `password`, por exemplo:
```
curl
    -u "<clientid>:<clientsecret>"
    –H "Content-Type: application/x-www-form-urlencoded"
    –d "grant_type=password&username=<IBMid>&password=<IBMid password>
       [&ims_account=<ims account>][&bss_account=<bss account>]
       [&response_type=cloud_iam,uaa,ims_portal]"
    "https://iam.ng.bluemix.net/oidc/token[?pretty=true]"
```
{: codeblock}

Como uma extensão para o OAuth 2.0, é necessário fornecer informações de conta para tornar a conta do token específica. Também é possível listar tipos de resposta diferentes para obter tokens `UAA` ou `IMS` para interações com APIs do CloudFoundry ou do IMS.

O Cloud IAM Token Service permite criar, atualizar, excluir e usar chaves API para usuários. Estas chaves API podem ser criadas com chamadas da API ou com o Bluemix Console. Para utilizar uma chave API, um adotante pode usar o tipo de concessão estendido a seguir:
```
curl
    -u "<clientid>:<clientsecret>"
    –H "Content-Type: application/x-www-form-urlencoded"
    –d "grant_type=urn:ibm:params:oauth:grant-type:apikey&
       apikey=<apikeyvalue>[&response_type=cloud_iam,uaa,ims_portal]"
    "https://iam.ng.bluemix.net/oidc/token[?pretty=true]"
```
{: codeblock}

O token resultante pode ser usado como um recuperado com uma concessão senha ou IU de login.

Como variação adicional, o Cloud IAM Token Service permite efetuar login interativamente com a IU. Isso é implementado usando o tipo de concessão `authorization_code` do OAuth 2.0 e também é conhecido como `OAuth Dance`, já que ele causa múltiplos redirecionamentos do navegador da web durante a fase de autenticação.

Outro foco do Token Service é a capacidade de criar IDs de Serviço e chaves API para os IDs de Serviço. Um ID de Serviço é semelhante a um "ID funcional" ou a um "ID do aplicativo" e é usado para autenticar com relação a serviços, e não para representar um usuário.

Os usuários podem criar IDs de Serviço e ligá-los a escopos, como uma conta do Bluemix ou uma organização ou um espaço do CloudFoundry. Essa ligação é feita para fornecer a um ID de Serviço um contêiner para residir. Esse contêiner também define quem pode atualizar e excluir o ID de serviço e quem pode criar, atualizar, ler e excluir chaves API que estiverem associadas a este ID de Serviço. Um ID de Serviço NÃO está relacionado a um usuário.

Para obter um melhor entendimento de como usar IDs de Serviço, é possível experimentar o [Demo do Aplicativo](https://iam.ng.bluemix.net/demo) que demonstra as APIs.

## Visão geral do gerenciamento de acesso
{: #access_management}

O IAM é um sistema Attribute Based Access Control (ABAC) com condições inspiradas pela publicação do
[NIST](http://nvlpubs.nist.gov/nistpubs/specialpublications/NIST.sp.800-162.pdf).  

O IAM usa uma combinação de atributos para determinar o acesso aos recursos. As políticas do IAM possuem regras que são aplicadas às funções, aos atributos de IDs de usuários/serviço, aos atributos de recursos e às condições. Isso permite uma abordagem flexível e poderosa para definir o acesso para IDs de usuários e de serviço.

Por exemplo, se uma máquina virtual, VM123, puder ter os seguintes atributos: 
```
    resource: {
      'serviceName': 'virtual-machine',
      'region': 'us-south',
      'resourceType': 'vm',
      'resource': 'vm123'
    }
```
{: codeblock}
  
Qualquer combinação desses atributos de recursos pode ser usada para criar uma política.

Para obter exemplos mais detalhados, consulte [Exemplos de política do IAM](https://console.stage1.ng.bluemix.net/docs/developing/Access-Management/policy_examples.html#iam_policy_examples).

O ABAC é diferente do Role Based Access Control (RBAC), em que funções predefinidas são designadas a usuários. Estas funções predefinidas possuem privilégios e usuários específicos com a função que possui todos os privilégios que são definidos por esta função.  
 
Por exemplo, uma Função `Administrador` de Máquina Virtual. Essa função implica todos os privilégios de tipo Administrador em qualquer recurso de máquina virtual. 

Uma maneira simples de pensar no ABAC é:

1. Há Usuários, Recursos, Contextos e Ações.
1. Cada instância de um Usuário, Recurso, Contexto e Ação possui um identificador exclusivo.
1. Cada instância recebe atributos.
   Basicamente, isso significa: "O que é verdade sobre a instância de um ponto de vista de autorização".
   Exemplos:
   1. O usuário é do signo de Peixes e nasceu na década de 1960.
   1. O Recurso é um jogador de uma equipe de beisebol.
   1. O Contexto é das 9h às 17h no Horário do Leste dos EUA.
   1. A Ação é "possível de atualizar".
1. Políticas são criadas para determinar qual conjunto de atributos possui permissão para o Usuário executar a Ação no Recurso.
1. Quando uma solicitação é feita por um Usuário para executar uma Ação em um Recurso, as políticas são consultadas para ver se a solicitação é permitida.

A imagem a seguir mostra uma visualização detalhada da sequência de autorizações. 

![Sequência de autorizações](auth_sequence.png)

## Configurando o controle de acesso para seu serviço
{: #setup_access_mgmt}

A integração de um serviço no {{site.data.keyword.Bluemix_notm}} requer um conjunto diferente de operações do que a integração de um serviço no Cloud IAM. Tecnicamente, é possível integrar-se com o {{site.data.keyword.Bluemix_notm}} e com o Cloud IAM de modo independente e em qualquer ordem. A equipe do IAM Cloud está trabalhando com a equipe de integração de serviço do {{site.data.keyword.Bluemix_notm}} para que o serviço do {{site.data.keyword.Bluemix_notm}} no processo de integração também inclua a integração do Cloud IAM.

Para configurar o controle de acesso para seu serviço, deve-se usar as seguintes etapas como parte de seu processo de integração:

### Etapa 1: Criar um ID de serviço fazendo essa solicitação de HTTP:
```
  POST https://iam.ng.bluemix.net/serviceids
  Authorization: <bluemix token>
  Content-Type: application/json

  {
    "name": "<service id name>",
    "description": "<service id description>",
    "boundTo": "<crn>"
  }
```
{: codeblock}

Comando curl:
```  
curl -X POST -H 'Authorization: <bluemix token>' -H 'Content-Type: application/json' -d '{"name": "<service id name>", "description": "<service id description>", "boundTo": "<crn>"}' 'https://iam.ng.bluemix.net/serviceids'
```
{: codeblock}

O seguinte descreve os valores de `ID de serviço` e `CRN de serviço` usados no comando `curl` em mais detalhes:
  
#### ID de serviço 
  
O nome do ID de serviço pode ser igual ao nome do serviço que aparece nos CRNs para seu serviço.
  
Seu ID de serviço deve ser ligado a uma conta, organização ou espaço. Essa ligação determina quem pode gerenciar seu ID de serviço. Por exemplo, o administrador ao qual seu ID de serviço é ligado é capaz de atualizar ou de excluir. Seu token do {{site.data.keyword.Bluemix_notm}} precisa ter acesso à conta, à organização e ao espaço no qual está ligando o ID. Para ligar a uma conta, o CRN `boundTo` deve ser semelhante ao seguinte: 

`crn:v1:::<service name>::a/<account id>:::` 
  
Para uma organização, ele deve ser semelhante ao seguinte:
`crn:v1:<cname>:<ctype>:<service name>:<region>:o/<organization id>:::` 
  
Para um espaço, ele deve ser semelhante ao seguinte:
`crn:v1:<cname>:<ctype>:<service name>:<region>:s/<space id>:::`  
  
O valor `boundTo` que é especificado não tem efeito sobre quais recursos seu ID de serviço pode acessar. 
  
As políticas de acesso do IAM controlam quais recursos seu ID de serviço pode acessar. Embora seu ID de serviço esteja ligado a uma organização IBM, políticas do IAM podem ser criadas para permitir que seu ID de serviço acesse recursos fora dessa organização. Ao integrar-se com o IAM, a primeira política de acesso que é criada pela equipe do IAM permite que o ID de serviço crie políticas para quaisquer recursos que pertencerem ao seu serviço.

Consulte [createServiceid](https://iam.stage1.ng.bluemix.net/ibm/api/explorer/) para obter mais informações sobre essa API e APIs relacionadas.

#### CRN de serviço

O nome do serviço no CRN `boundTo` deve corresponder ao nome do serviço que aparece no CRN do seu serviço.
  
Consulte a [Especificação do CRN](https://github.ibm.com/ibmcloud/builders-guide/blob/master/specifications/crn/CRN.md) para ajudá-lo a preencher estes campos.

Na resposta, salvar metadados->UUID e metadados->CRN, que são seus ID de serviço e o CRN do ID de serviço.


### Etapa 2: Entrar em contato com o Esquadrão AccessControl em [#iam-usuários](https://ibm-cloudplatform.slack.com/messages/iam-adopters). 
Seu ID de serviço recebe a função de Administrador de políticas para os recursos de seu serviço.

Use este formato:
```
IAM adopter service info

service id: uuid from step #1
service name: your service name as it will appear in the crns for your service
```
{: codeblock}

### Etapa 3: Deve-se criar uma chave API por meio do seu ID de serviço. Use a solicitação de HTTP a seguir:
```
  POST https://iam.ng.bluemix.net/apikeys
  Authorization: <bluemix token>
  Content-Type: application/json

  {
    "boundTo": "<service id crn>",
    "name": "<api key name>",
    "description": "<api key description>"
  }
```
{: codeblock}

Comando curl: 
```
  curl -X POST -H 'Authorization: <bluemix token>' -H 'Content-Type: application/json' -d '{"boundTo": "<service id crn>", "name": "<api key name>", "description": "<api key description>"}' https://iam.ng.bluemix.net/apikeys
```
{: codeblock}

`boundTo` precisa ser o CRN do seu ID de serviço (metadados de campo->CRN salvo na resposta da etapa 1). O nome e a descrição podem ser qualquer coisa.

Na resposta, salvar entidade->apiKey.

Consulte [createAPIKey](https://iam.stage1.ng.bluemix.net/ibm/api/explorer/#!/Cloud_IAM_Service_Id_and_Api_Key_MVP/createAPIKey) para obter mais informações sobre essa API e APIs relacionadas.

### Etapa 4: obter um token de acesso para sua chave API de IDs de serviço. 

Quando a permissão é estabelecida, seu serviço pode fazer solicitações PAP e PDP para os recursos de seu serviço.

Use o campo **apiKey** na etapa 3, que é o valor da sua chave API (apikey_value).

  * Em seguida, obtenha o token com o valor da chave API (certifique-se de usar caracteres de escape):

    Comando curl:
```
    curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -H "Accept: application/json" -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-type%3Aapikey&apikey=<apikey_value>" "https://iam.ng.bluemix.net/oidc/token"
```
{: codeblock}

Use o campo **access_token** no resultado, que é o seu token de chave API (para seu ID de serviço). O **access_token** precisa ser codificado em URL quando usado no comando curl, conforme mostrado anteriormente.


### Etapa 5: Registrar a lista de ações de serviço possíveis para o nome do serviço.

  a. Mapear ações de serviço para Funções Definidas pelo Sistema do IAM. Esse mapeamento é usado posteriormente durante o registro de serviço.

  * Uma lista de Funções Definidas pelo Sistema do IAM pode ser localizada executando a seguinte solicitação:
  
Comando curl:
```
curl -X GET --header 'Accept: application/json' --header 'Authorization: <api key token>' 'https://iampap.ng.bluemix.net/acms/v1/roles'
```
{: codeblock}

**Nota:** use a *versão do CRN* das Funções Definidas pelo Sistema do IAM na sua carga útil de registro de serviço. 

A seguir há um exemplo de mapeamento de ações de serviço para funções.

  <table>
    <tr>
      <th>Terminal de API</th>
      <th>Ação de Serviço</th>
      <th>Funções Definidas pelo Sistema do IAM</th>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}</td>
      <td>key-protect.keys.create</td>
      <td>Administrator</td>
    </tr>
    <tr>
      <td>GET /api/keys/{key_id}</td>
      <td>key-protect.keys.read</td>
      <td>Visualizador, Editor, Administrador</td>
    </tr>
    <tr>
      <td>PUT /api/keys/{key_id}</td>
      <td>key-protect.keys.update</td>
      <td>Editor, Administrador</td>
    </tr>
    <tr>
      <td>DELETE /api/keys/{key_id}</td>
      <td>key-protect.keys.delete</td>
      <td>Administrator</td>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}/encode</td>
      <td>key-protect.keys.encode</td>
      <td>Editor, Administrador</td>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}/decode</td>
      <td>key-protect.keys.decode</td>
      <td>Editor, Administrador</td>
    </tr>
  </table>

  b. Use a linha de comandos a seguir para registrar seu serviço com o `PAP`:
```
  curl -X PUT -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'Authorization: <api key token>' -d '{
    "displayName": {
      "default": <service display name>
    },
    "actions": [{
      "id": <service_action>,
      "displayName": {
        "default": <service action display name>
      },
      "roles": [<system_defined_role_crn>]
    }]
  }' 'https://iampap.ng.bluemix.net/acms/v1/services/<service_name>'
  ```
{: codeblock}
  
As ações devem ser definidas conforme especificado no
[Formato de Ação de Serviço](https://console.stage1.ng.bluemix.net/docs/developing/Access-Management/index.html#action_format).
  
Por exemplo, ao usar o formato padrão:

  `<service-name>.<component>.<verb>`
  
  Usando a ação `key-protect.keys.decode` do exemplo anterior 
  * service-name = key-protect
  * component = keys
  * verb = decode
  

### Etapa 6: Verificar o serviço registrado de acordo com os detalhes na etapa 5.

```
curl -H "Authorization: <api key token>" "https://iampap.ng.bluemix.net/acms/v1/services/<service_name>"
```

### Etapa 7 (opcional): Excluir o serviço que você registrou na etapa 5.

```
curl -X DELETE -H "Authorization: <api key token>" "https://iampap.ng.bluemix.net/acms/v1/services/<service_name>"
```

### Etapa 8: Configurar o serviço para usar o SDK do PEP para verificar permissões com o PDP. Escolha a linguagem do SDK correspondente.

  * [SDK do PEP para Java](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Java)
  * [SDK do PEP para Nodejs](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Node)
  * [SDK do PEP para Python](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Python)
 

## Terminologia
{: #terminology}

### Terminologia da identidade

* IBMid - uma identidade fornecida e hospedada pela IBM par acessar o IBM Cloud e aplicativos, comunidades e suporte IBM.
* ID do usuário - identificação que representa uma pessoa real.
* ID de serviço - identificação que representa um usuário técnico, uma máquina, um aplicativo ou serviços. Semelhante aos "IDs funcionais" ou aos "IDs de aplicativo", que também representam um usuário técnico, mas usa o tipo de entidade "ID do usuário".
* OAuth 2.0 - padrão aberto para autorizar o acesso a aplicativos e APIs sem fornecer credenciais para o serviço de destino. O OAuth também é usado para conter informações de autenticação.
* OpenID Connect - padrão aberto construído sobre o OAuth 2.0 que foca em fornecer informações sobre o usuário autenticado.
* ID do cliente - aplicativos que interagem com terminais compatíveis com OAuth 2.0 e que requerem um par de ID/segredo do cliente para autenticação. Um aplicativo precisa registrar-se com um Token Service para obter um ID do cliente.
* Terminal de token - usado pelo cliente para obter um ou mais tokens apresentando informações de identidade, como um nome de usuário ou senha, concessão de autorização ou token de atualização.
* Terminal de autorização - usado pelo cliente para autenticar um usuário com o serviço de token por meio da IU.
* Token - uma sequência opaca ou transparente que permite que um aplicativo recupere a autenticação e/ou a autorização de uma identidade.
* Token de acesso - esse token é usado para ser enviado como informações de identidade para APIs. Ele contém informações de identidade e é válido somente por um curto período de tempo. 
* Token de atualização - esse token é armazenado somente no cliente que solicitou a autenticação. Ele será usado para obter um novo token de acesso, (por exemplo, atualizar o token de acesso), se o token de acesso expirar. Como o token de atualização tem um tempo de vida longo, ele não deve deixar o sistema do cliente, a não ser para o propósito de atualizar o próprio token de acesso. 
* Cookie de identidade - após efetuar login no IBM Cloud Token Service, um cookie contendo sua identidade é emitido para seu navegador. Você não receberá um novo desafio para efetuar login enquanto esse cookie existir e for válido. Ele expirará após 24 horas, se você efetuar logout do IBM Cloud Token Service ou fechar o navegador.
* JSON Web Token - um padrão baseado em JSON (RFC 7519) para representar tokens de acesso. O conteúdo do token de acesso é transparente, (ou seja, pode ser facilmente lido). Um token baseado em JWT é geralmente assinado para ser capaz de verificar a prova de origem do token.
* Chave Pública - pode ser usada para validar uma assinatura de um Token da Web JSON. Se estiver utilizando criptografia assimétrica, a chave pública poderá ser publicada para consumo pelos clientes com segurança.
* Chave Privada - pode ser usada para criar uma assinatura para um JSON Web Token. Essa chave deve ser mantida em segredo, caso contrário, tokens de acesso válidos poderão ser criados por outros.
* realmid - identificador para distinguir usuários de diferentes registros do usuário. Os valores atualmente utilizados são "IBMid" para usuários autenticados pelo sistema IBMid e "iam" para IDs de Serviço autenticados pelo Token Service.
* identifier - identificador que nunca muda e identifica exclusivamente um usuário dentro de um registro do usuário (indicado pelo parâmetro `realmid`). A combinação de <realmid>-<identifier> deve sempre resultar em um usuário identificável exclusivamente. No caso do IBMid, o identificador exclusivo da IBM, 'IUI', é usado.             
* sujeito - o nome do usuário da identidade. Muitas vezes na mesma forma de um endereço de e-mail. No caso do IBMid, esse é o IBMid da identidade.
* Solicitações customizadas - informações não padrão adicionais dentro de um JSON Web Token.

### Terminologia de gerenciamento de acesso

* (PAP) Policy Administration Point - ponto que gerencia políticas de autorização de acesso.
* (PDP) Policy Decision Point - ponto que avalia solicitações de acesso com relação às políticas de autorização antes de emitir decisões de acesso.
* (PEP) Policy Enforcement Point - ponto que intercepta a solicitação de acesso do usuário a um recurso e faz uma solicitação de decisão para o PDP para obter a decisão de acesso (ou seja, o acesso ao recurso é aprovado ou rejeitado) e age na decisão recebida.
* (PIP) Policy Information Point - a entidade do sistema que age como uma origem de valores de atributo (ou seja, um recurso, um sujeito ou um ambiente).
* (PRP) Policy Retrieval Point - ponto em que as políticas de autorização de acesso XACML são armazenadas, normalmente um banco de dados ou um sistema de arquivos. 
* sujeito - a "pessoa" em um par de autorizações de recurso e sujeito, como um usuário ou grupo. O recurso é aquele que o sujeito pode acessar.
* função - uma coleção de permissões que podem ser designadas a um usuário, grupo de usuários, sistema, serviço ou aplicativo que permitem executar determinadas tarefas.
* recurso - um objeto físico ou lógico nos quais as ações podem ser executadas, como uma organização, um espaço, um banco de dados ou uma tabela.
* condições - uma função que é avaliada como "True", "False" ou "Indeterminate".
* ações - uma tarefa definida que um aplicativo executa em um objeto ou recurso como resultado de um evento.
* política - um conjunto de regras, um identificador para o algoritmo de combinação de regra e (opcionalmente) um conjunto de obrigações ou de conselhos. Pode ser um componente de um conjunto de políticas.

## Funções definidas pelo Sistema
{: #system_defined_roles}

As funções do IBM Cloud representam uma coleção de ações que são fornecidas por serviços ativados pelo IAM.

O agrupamento das ações como funções fornece flexibilidade para suportar ações para quaisquer serviços ou
recursos usando um conjunto mínimo de funções definidas pelo
Sistema. Por exemplo, se precisar de um `Administrador` para MVs,
Armazenamento e Redes, será possível usar a função do `Administrador` para todos os três,
mas apenas para mudar o destino da política. `Administrador` em MVs, `Administrador` em Armazenamento e
`Administrator` em Rede.

*O que o IBM Cloud IAM não faz*: uma alternativa que é utilizada por outros sistemas de
gerenciamento de acesso é construir recursos na função. Essa abordagem causa inadvertidamente um novo nome de
função para cada tipo de recurso que for introduzido no sistema. Por exemplo, com essa abordagem, seria
necessária uma função `VMAdministrator`, uma função
`StorageAdministrator` e uma função `NetworkAdministrator` para
cobrir a administração de recursos de MVs, Armazenamento e Rede.


A tabela a seguir mostra Funções Definidas pelo Sistema do IAM e exemplos de ações que são mapeadas para elas.

|Nome da função do IBM Cloud| Descrição | Exemplo de ações|
|:-----------------|:-----------------|:-----------------|
|Viewer|ações que não mudam o estado (isto é, somente leitura)| <ul><li>listar dispositivos</li><li>ler objeto de armazenamento</li><li>executar consulta</li><li>executar procura</li></ul>|
|Aplicativos|ações que podem modificar o estado e criar/excluir sub-recursos|<ul><li>criar MV</li><li>excluir MV</li><li>anexar armazenamento</li><li>reiniciar</li><li>iniciar/parar</li><li>renomear</li></ul>|
|Operador|ações necessárias para configurar e operar recursos|<ul><li>atualizar configuração</li><li>iniciar/parar MV</li><li>logs de visualização</li><li>backup/restauração</li></ul>|
|Administrator|todas as ações, incluindo a capacidade de gerenciar o controle de acesso|<ul><li>convidar usuário </li><li>criar MV</li>atualizar políticas de acesso de usuário</li><li>listar dispositivos</li><li>criar MV</li><li>excluir MV</li><li>anexar armazenamento</li><li>reiniciar</li><li>iniciar/parar</li><li>renomear</li><li>backup/restauração</li></ul>|
|Administrador de faturamento|ações relacionadas à administração de faturamento|<ul><li>atualizar cartão de crédito</li><li>listar faturas</li><li>fazer download de faturas</li></ul>|

A lista mais atual de Funções Definidas pelo Sistema pode ser consultada por meio do microsserviço do PAP
em:

Comando curl: 

`curl -X GET --header 'Accept: application/json' --header 'Authorization: <api key token>' 'https://iampap.ng.bluemix.net/acms/v1/roles'`
    
    
## Formato de ação de serviço
{: #action_format}

As ações devem ser definidas em 1 de 2 formatos:
  
* Padrão:

    `<service-name>.<component>.<verb>`
* Ponto de Interceptação de Controle de Acesso: 

    `<METHOD> /<api_route>`
  
### Padrão
A maioria dos serviços chama o PDP do IAM diretamente e pode modificar o código-fonte para suportar a formatação de ação padrão.  
 
 Esse formato deve incluir todas as três partes e é alfanumérico, sem espaços ou caracteres especiais diferentes de '-'.

`<service-name>.<component>.<verb>`

Em que: 
* service-name - o nome do serviço que está definido no campo de nome de serviço do CRN.
* component - recurso ou subcomponente do serviço.
* verb - verbo que define ação suportada para o componente do nome de serviço. 
  
Por exemplo: `key-protect.keys.decode` 
* service-name = key-protect
* component = keys
* verb = decode

### Ponto de Interceptação de Controle de Acesso da API de REST
{: intercept_point}

Em alguns casos, as solicitações da API de REST são direcionadas por meio de um gateway que age como um Ponto de Interceptação de Controle de Acesso. O PDP do IAM é chamado diretamente no ponto de interceptação antes de chamar o serviço real da API de REST. O serviço que processa a solicitação da API de REST nunca chama o PDP do IAM.

O ponto de interceptação conhece somente a rota da API de REST e o terminal para o qual a solicitação deve ser enviada. Consulte, [Considerações para Pontos de Interceptação de Controle de Acesso](https://console.stage1.ng.bluemix.net/docs/developing/Access-Management/intercept_point.html#intercept_point_overview) para obter mais detalhes.


 Esse formato deve incluir ambas as partes e suporta caracteres seguros para URLs, conforme especificado pelo [RFC 1738](https://www.ietf.org/rfc/rfc1738.txt).
 
 
`<METHOD> /<api_route>`
  
Em que:
* METHOD - o método da API de REST. 
* api_route - o URI para a API de REST. 

Por exemplo: `GET /v1/things/thing123`
* METHOD = GET
* api_url = /v1/things/thing123

<!---
# Setting up access control for your service
{: #setup_access_mgmt}

Onboarding a service to {{site.data.keyword.Bluemix_notm}} is a different set of operations than onboarding a service with Cloud IAM. Technically you can onboard with {{site.data.keyword.Bluemix_notm}} and Cloud IAM independently and in any order. The Cloud IAM team is working with the {{site.data.keyword.Bluemix_notm}} service onboarding team so that the {{site.data.keyword.Bluemix_notm}} service on boarding process will also include Cloud IAM onboarding.

To setup access control for your service you must use the following steps.

#### Step 1: Create a service id by making this http request:
  ```
  POST https://iam.ng.bluemix.net/serviceids
  Authorization: <bluemix token>
  Content-Type: application/json

  {
    "name": "<service id name>",
    "description": "<service id description>",
    "boundTo": "<crn>"
  }
  ```
Curl command:
  ```  
  curl -X POST -H 'Authorization: <bluemix token>' -H 'Content-Type: application/json' -d '{"name": "<service id name>", "description": "<service id description>", "boundTo": "<crn>"}' 'https://iam.ng.bluemix.net/serviceids'
  ```
  
### Service id 
  
The service id name can be the same as the service name that appears in the crns for your service.
  
Your service id must be bound to an account, organization, or space. This binding determines who can manage your service id. For example, the administrator where your service id is bound are able to update or delete. Your {{site.data.keyword.Bluemix_notm}} token needs to have access to the account, organization, and space you are binding the id to. To bind to an account, the `boundTo` crn must look like the following: 

`crn:v1:::<service name>::a/<account id>:::` 
  
For an organization it must look like the following:
`crn:v1:<cname>:<ctype>:<service name>:<region>:o/<organization id>:::` 
  
For a space it must look like the following:
`crn:v1:<cname>:<ctype>:<service name>:<region>:s/<space id>:::`  
  
The `boundTo` value specified has no affect on which resources your service id can access. 
  
IAM access policies control which resources your service id can access. Even though your service id is bound to an IBM organization, IAM policies can be created that allow your service id to access resources outside of that organization.  When on boarding with IAM the first access policy that is created by the IAM team allows the service id to create policies for any resources owned by your service.

See [createServiceid](https://iam.stage1.ng.bluemix.net/ibm/api/explorer/#!/Cloud_IAM_Service_Id_and_Api_Key_MVP/createServiceid) for more information on this api and related apis.

###Service crn

The service-name in the `boundTo` crn must match the service name that appears in the crn for your service.
  
See the [CRN spec](https://github.ibm.com/ibmcloud/builders-guide/blob/master/specifications/crn/CRN.md) for help filling in these fields.

From the response, save metadata&ndash>uuid and metadata&ndash>crn, which are your service id and service id crn.


#### Step 2: Contact the AccessControl Squad at [#iam-adopters](https://ibm-cloudplatform.slack.com/messages/iam-adopters). 
Your service id will be given the role of Administrator of policies for your service's resources.

Use this format:
```
IAM adopter service info

service id: uuid from step #1
service name: your service name as it will appear in the crns for your service
```

#### Step 3: You must create an api key from your service id. Use the following http request:
```
  POST https://iam.ng.bluemix.net/apikeys
  Authorization: <bluemix token>
  Content-Type: application/json

  {
    "boundTo": "<service id crn>",
    "name": "<api key name>",
    "description": "<api key description>"
  }
```
Curl command: 
```
  curl -X POST -H 'Authorization: <bluemix token>' -H 'Content-Type: application/json' -d '{"boundTo": "<service id crn>", "name": "<api key name>", "description": "<api key description>"}' https://iam.ng.bluemix.net/apikeys
```
`boundTo` needs to be the crn of your service id (field metadata&ndash>crn saved from step 1’s response). The name and description can be anything.

From the response, save entity&ndash>apiKey.

See [createAPIKey](https://iam.stage1.ng.bluemix.net/ibm/api/explorer/#!/Cloud_IAM_Service_Id_and_Api_Key_MVP/createAPIKey) for more information on this api and related apis.

#### Step 4: Get an access token for your service id's API key. 

When the permission is established, your service can make PAP and PDP requests for your service's resources.

Use the entity **apiKey** field from step #3, this is your API key value (apikey_value).

  * Then get the token with the API key value (make sure you use escape characters):

    Curl Command: 
    ```
    curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -H "Accept: application/json" -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-type%3Aapikey&apikey=<apikey_value>" "https://iam.ng.bluemix.net/oidc/token"
    ```

Use the **access_token** field in the result, this is your api key token(for your service id).


#### Step 5: Register the list of possible service actions for the service name.

  a. Map service actions to IAM System Defined Roles. This mapping is used later during the service registration.

  * A list of IAM System Defined Roles can be found by performing the following request:
Curl command:
```
curl -X GET &ndash&ndashheader 'Accept: application/json' &ndash&ndashheader 'Authorization: <api key token>' 'https://iampap.ng.bluemix.net/acms/v1/roles'
```

**Note:** Use the _crn version_ of the IAM System Defined Roles in your service registration payload.

The following is an example of mapping service actions to roles.

  <table>
    <tr>
      <th>API Endpoint</th>
      <th>Service Action</th>
      <th>IAM System Defined Roles</th>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}</td>
      <td>key-protect.keys.create</td>
      <td>Administrator</td>
    </tr>
    <tr>
      <td>GET /api/keys/{key_id}</td>
      <td>key-protect.keys.read</td>
      <td>Viewer, Editor, Administrator</td>
    </tr>
    <tr>
      <td>PUT /api/keys/{key_id}</td>
      <td>key-protect.keys.update</td>
      <td>Editor, Administrator</td>
    </tr>
    <tr>
      <td>DELETE /api/keys/{key_id}</td>
      <td>key-protect.keys.delete</td>
      <td>Administrator</td>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}/encode</td>
      <td>key-protect.keys.encode</td>
      <td>Editor, Administrator</td>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}/decode</td>
      <td>key-protect.keys.decode</td>
      <td>Editor, Administrator</td>
    </tr>
  </table>

  b. Use the following command line to register your service with the `PAP`:
```
  curl -X PUT -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'Authorization: <api key token>' -d '{
    "displayName": {
      "default": <service display name>
    },
    "actions": [{
      "id": <service_action>,
      "displayName": {
        "default": <service action display name>
      },
      "roles": [<system_defined_role_crn>]
    }]
  }' 'https://iampap.ng.bluemix.net/acms/v1/services/<service_name>'
  ```
  
Actions must be defined as specified in the 
[Service Action Format](https://console.stage1.ng.bluemix.net/docs/developing/Access-Management/index.html#action_format).
  
For example, using the standard format:

  `<service-name>.<component>.<verb>`
  
  Using action `key-protect.keys.decode` from the previous example 
  * service-name = key-protect
  * component = keys
  * verb = decode
  
  [TODO: Also support REST like action format, yet to be approved]: <>

#### Step 6: Configure the service to use the PEP SDK in order to check permissions with the PDP. Pick the corresponding SDK language.

  * [PEP SDK for Java](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Java)
  * [PEP SDK for Nodejs](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Node)
  * [PEP SDK for Python](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Python)


<!---
# Identity and Access Management Adopter Guidelines
{: #iam_guidelines}

Onboarding a service to {{site.data.keyword.Bluemix_notm}} is a different set of operations than onboarding a service with Cloud IAM. Technically you can onboard with {{site.data.keyword.Bluemix_notm}} and Cloud IAM independently and in any order. The Cloud IAM team is working with the {{site.data.keyword.Bluemix_notm}} service onboarding team so that the {{site.data.keyword.Bluemix_notm}} service on boarding process will also include Cloud IAM onboarding. Until that work is complete please use the following onboarding steps.

- Users are identified with their IBMid.
  - Users authenticate with their IBMid and password.
  - Authentication returns a UAA/OAuth token which is used to access services within the IBM Cloud.
  
- Services are identified by their ServiceIDs.
  - Services authenticate with their ServiceID and APIkey.
  - Authentication returns an OAuth token which is used to access other services within the IBM Cloud.
  
- Services grant access to their resources by creating *Access Policies*.
  - *Roles* can be viewed and *Access Policies* can be managed through the 
  *Policy Administration Point (PAP)*.
  - Actions are permitted or denied through the *Policy Enforcement Point (PEP)* and *Policy Decision Point (PDP)*. 
  

## Creating a ServiceID
{: #create_serviceid}

To create a ServiceID you must use one of the following steps:

Make a one-time request for your ServiceID/APIkey.

 * Create a ServiceID with [swagger](https://iam.ng.bluemix.net/docs).
```
POST /serviceids
```
 * Create a ServiceID using `curl`.
```
curl -X POST -H "Authorization: $CF_TOKEN" -H 'Content-Type: application/json' -d '{"name": "IAMdemo", "description": "IAM demo of adopting service", "boundTo": "crn:v1:staging:public:docker-registry:us-south:o/57666a74-e136-4eb0-a085-220345fac266:::"}' 'https://iam.ng.bluemix.net/serviceids’
```
**Note**
The `boundTo` is the {{site.data.keyword.Bluemix_notm}} Org that is owned by you or your admin.

## Creating a ServiceID metadata response
{: #create_serviceid_metadata}

The following is a ServiceID metadata response using `curl`. Your service ID is expressed with a UUID and CRN format.

```
{"metadata":{\
"uuid":"ServiceId-3ec0dd02-7a10-40bf-92e7-b9a329547c07",\
"crn":"crn:v1:staging:public:iam:us-south:o/57666a74-e136-4eb0-a085-220345fac266::\
serviceid:ServiceId-3ec0dd02-7a10-40bf-92e7-b9a329547c07",\
"version":"1-4d9b1b10ce893f750a2d7e0d6ee34fd7"},"entity":{"boundTo":"crn:v1:staging:public:docker-registry:\
us-south:o/57666a74-e136-4eb0-a085-220345fac266:::","name":"IAMdemo","descripti\
on":"IAM demo of adopting service"}}
```

## Creating an APIkey for your ServiceID
{: #create_apikey_serviceid}

Create an APIkey
```
POST /apikeys
```

The following is a `curl` example of creating an APIkey
```
curl -X POST -H 'Authorization: $CF_TOKEN' -H 'Content-Type: application/json' -d '{"boundTo": "crn:v1:staging:public:iam:us-south:o/57666a74-e136-4eb0-a085-220345fac266::serviceid:ServiceId-3ec0dd02-7a10-40bf-92e7-b9a329547c07", "name": "IAMdemo", "description": "IAM deom of adopting service"}' https://iam.ng.bluemix.net/apikeys
```

## Authenticating with an APIkey
{: #auth_apikey}

The following is a `curl` example of authenticating with an APIkey
```
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -H \
"Accept: application/json" -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-ty\
pe%3Aapikey&apikey=DuE2s….bfRKc=" "https://iam.s\tage1.ng.bluemix.net/oidc/token”
{"access_token":"eyJraWQiOiIyMDE2MTAyNC0wMDowMDowMCIsImFsZyI6IlJTMjU2In0.eyJpZG\
VudGlmaWVyIjoiU2VydmljZUlkLTNlYzBkZDAyLTdhMTAtNDBiZi05MmU3LWI5YTMyOTU0N2MwNyIsI\
nN1YiI6IlNlcnZpY2VJZC0zZWMwZGQwMi03YTEwLTQwYmYtOTJlNy1iOWEzMjk1NDdjMDciLCJzdWJf\
dHlwZSI6IlNlcnZpY2VJZCIsImFjY291bnQiOnsiYnNzIjoiMDY0Zjg3NTZlMzZlODk5MDAyYjliM2M\
wNzZiZTM3OGIifSwibWZhIjp7fSwiaWF0IjoxNDc5Mzk3MTYwLCJleHAiOjE0Nzk0MDA3NjAsImlzcy\
I6Imh0dHBzOi8vaWFtLnN0YWdlMS5uZy5ibHVlbWl4Lm5ldC9vaWRjL3Rva2VuIiwiZ3JhbnRfdHlwZ\
SI6InVybjppYm06cGFyYW1zOm9hdXRoOmdyYW50LXR5cGU6YXBpa2V5Iiwic2NvcGUiOiJvcGVuaWQi\
LCJjbGllbnRfaWQiOiJkZWZhdWx0In0.APRVqQmfUwn6K4Kg2sicT_kGpqSGQXr4Vua8Q5p4B0_dfGE\
tbbe10JqHeE4ovud6u8xjclAIcqCcbjIH4RijnUNGReVse49gS6JlXxmiNGA8OVlNGjiL68ygIpYsj-\
crx8kVuTrXAFqx9lhLEBhAzDneldu-gjSz7wrQKqISikcMXPXQkmLDuoT-OGNq8rG4fCiENBiweUrGf\
_Yw9W5NSiWyQGdWmczS70Krc_hx1iXskmt8pz5_0_vPXY6_tG5rY6KPw-bHO1wux91Q7aTZwCmaL0zI\
F2d3cIuFe1XywJ_926MfwWy65MxC3xv7-_rsZMFoprrLtBsuEnshNWUDhg",
"token_type":"Bearer","expires_in":3600,"expiration":1479400760}
```

## Registering your ServiceID with IAM
{: #register_serviceid}

To complete the on boarding process, contact the AccessControl Squad at
[#iam-adopters](https://ibm-cloudplatform.slack.com/messages/iam-adopters). 

Your service id will be given the role of Administrator of policies for your 
service's resources.

Call the `PAP` and `GET` the existing policies
```
curl -X GET -H 'Authorization:<APIkeyToken>' \
'https://iampap.ng.bluemix.net/acms/v1/scopes/global/service_ids/\
ServiceId-3ec0dd02-7a10-40bf-92e7-b9a329547c07/policies'

Response:
{"policies":[]}  <-- no policies yet
```

## Creating access policies
{: #creating_policies}

Now that you are fully on boarded, you can begin creating access policies 
for resources owned by your service.
-->

# IDs de Serviços de Laboratório e chaves API

interconnect-service1:
  * ServiceId-2bc4561c-615f-4ba3-ab50-eba3b70a69d3
  * 7DRDYlbFM8Mpt7cOKS7clQisOItOfFcvItkd4MQsd20M

interconnect-service2:
  * ServiceId-089f58e9-f0a0-4b47-b3db-a2d9036080aa
  * rOB0ZqGR1pbiWxNMbn_OfFDmuJcULhqnYW_G0hNnJj0w

interconnect-service3:
  * ServiceId-9a57c3ed-2a8d-45ff-8b34-a7feb80e81bd
  * 6qZoPsd_V47hQQHHVFR1Z8PeGwTZKmNxHgGlURH7OIPf

interconnect-service4;
  * ServiceId-df633c5f-dee3-4e7b-87c3-7a3ed57d6509
  * 3yICAhsR55nlXJLjPA2nLBcAM1SX7LrXpOabjivVeteQ

interconnect-service5:
  * ServiceId-e3703b76-4f91-4323-9b6d-db3122952a72
  * 1ZD8qf_jqHC7JVOzrrvbuI3Dcr153hkGsr4Ll7EvsXKW

interconnect-service6:
  * ServiceId-2a31b14e-6cad-4597-82cf-04f2cb16c26d
  * XFROeDFVyBnJfecSjNhZngPDOniX-5qXl9QWZrsuNjYY

interconnect-service7:
  * ServiceId-56b98026-bb1c-4166-8128-c4841d10373c
  * cBponeC40MEgPy4mW55kb26XbMFAVmF0y2T3T1fYXJuL

interconnect-service8:
  * ServiceId-7a9cf953-044e-474a-9ffb-e66a1b68f437
  * OEGprDQNk7TLxFNrCbKfvLGxQRrbGS-PvhKSCUYJYn1a

interconnect-service9:
  * ServiceId-147203b6-0156-41c6-a28c-7306f047eebb
  * 2OiRisDKDXYA0_0BtlA7OyBk-7II9NUa709HgbF-D_kY

interconnect-service10:
  * ServiceId-87909073-acb8-403c-ab32-91d632e6c5a6
  * 93eWV_Ns2UrjNGENaaau1yOQmGDvTO2FxEivThGIZUOV

interconnect-service11:
  * ServiceId-0e2ec208-926e-4db7-aab4-c0d3bf44865f
  * gEa6bECSMAVF68cS5AbckIKp47_OX3_q63JNWI6-Q5Y0

interconnect-service12:
  * ServiceId-c793ae24-5f43-4c55-815a-830b8c79d1ee
  * WRSnr-FJZ_mI2DbG-8MNqPdAZHq3IkVZU-WbWL7l7uNC

interconnect-service13:
  * ServiceId-b426e816-6975-47df-ac69-01c08560ef3e
  * MkFJJ_zJDg5MiIRUo78dzCC-Mmw3r9DSzZVMvHZ7A63Z

interconnect-service14:
  * ServiceId-d97a9df4-6dbe-43ab-8b10-a70bb3ff9085
  * N63GX1wfo6UDc5kNrEWYHcPT27bD9V0JLmoB-iKsPfEb

interconnect-service15:
  * ServiceId-c6090a5b-569d-40cc-84f5-12480a9ede60
  * xLuJdPmW5npQMuHs4hyJOWZMaYY7i_DwZOSjWlZjnjjK

interconnect-service16:
  * ServiceId-c1d34878-cac3-43a3-bad6-a5b4992d9ed9
  * UZjSMGF8Aw42lzbHtkgDH14FyJxe0s0aN0O4Qk9uBe8T

interconnect-service17:
  * ServiceId-9ccaba36-6b07-4e9b-8b97-fbe1111f4908
  * CJb3qUI3cQWUiMMSt2RuL3ti9yE-F2-i2-1yIfowOM30

interconnect-service18:
  * ServiceId-84a01c41-8330-49e3-842f-b45eaa368d3d
  * 8-qw4_k5Sbjd1sxAiKksHubfPIlkjK2C9S0DnK-WpPDo

interconnect-service19:
  * ServiceId-2ef5d7ea-7ce0-453d-aa70-fbc5f4b781ef
  * Cz4QHZR_qd_WUZsScF-dVcu31J08dPuF_gszMd4oCLJj

interconnect-service20:
  * ServiceId-9e85525e-fe29-45e1-81b5-0681cd0b7f22
  * -OeamgjtKqnGUmdKFAVOWjKhYJMYP8HstCcPrRKfy4V9

interconnect-service21:
  * ServiceId-62c49423-3205-446e-a4aa-e24deb9b158e
  * N2XQ6MpKTvRJX_2IuDQoOiMK5AIhICUFj2wMVyg8O6Pn

interconnect-service22:
  * ServiceId-2de4c08b-f2cc-4e93-bb8b-eebf2222f93e
  * lEOzJvJJV0EgDjQQa8g5kr_D-PawYqIN-QE1QTNpoD5S

interconnect-service23:
  * ServiceId-49e6dc57-70f2-4a69-aac9-311394454475
  * G7epLqdbohZ8tVs8Jcx4qSjlMzlzrw2piNEnPiP4RZ7A

interconnect-service24:
  * ServiceId-7a4ac3ec-bd69-4dbf-8439-f8f5a2ffb88a
  * I7d2KnqbyeQG1rk1AcKeVXgNT1iqCwhSAhan9g-pWucx

interconnect-service25:
  * ServiceId-542a018b-9248-4bb3-bfc1-e0c9d1e70b46
  * WUl0OMnGkLP1BF3bdkqOJeT3niuwD2p1kWd8In05jpho

interconnect-service26:
  * ServiceId-c94f5b5e-0d43-4843-8153-d402fae7e1b5
  * dBtmioisFz_7gTYBPL1IArA_E9F4HYnYYAKVZJfxIcv3

interconnect-service27:
  * ServiceId-37986f6b-325c-42c3-8973-c88c7d365c0c
  * SY1kOsSpSPSLOocmBMwuPWO7u-60aglBliO2Qa4tu4dv

interconnect-service28:
  * ServiceId-08a48402-a02c-4fe6-9260-635188202aad
  * QFaQPoJaYAcVsVlmnVIlkO1haVY_xg8ZZEt-AkmAzAIn

interconnect-service29:
  * ServiceId-e9414ce2-c8d5-44d6-be68-f6c5176f4482
  * FKiafH2hr8eooB0nS6N-3vDrYkIbltzBZb688U8JxpvD

interconnect-service30:
  * ServiceId-e5caa06b-4087-4f55-b51c-bbbad4d78d84
  * 2hcjXXt2G7hmyqAhWlqhXHL9OwFlNdr2_3NZ3tVkBMF2

interconnect-service31:
  * ServiceId-e71b84e8-fe53-4e40-af46-af26f9e59db3
  * 0vwL6DjNl8ATJJ_mvHrEfuzYt9dyeZulA1nKj_q3zUjf

interconnect-service32:
  * ServiceId-fc200643-5788-4af9-a1a5-847d373331b3
  * gM919kowr90lDhuRNbvc-kt3WOKW0YQLRGYNqLVbwC-B

interconnect-service33:
  * ServiceId-df0898a2-8b19-49fc-a88b-f4868c6d2b18
  * KjDoJ5z2WGv2hIG9PRJuylkh0SPLnvAYLY7mVRkmCGGf

interconnect-service34:
  * ServiceId-1eaa9835-fb15-49a6-b19c-74970795a33f
  * wUXkKrKqJmZO8S4io1QoryPlZml9_G6A4L-6WHftl7Ny

interconnect-service35:
  * ServiceId-14f7e5fc-5be8-49b5-9843-4b338cc0c34e
  * Fi7nwbNHJVU7CXAba-MJR2jiCSG524zQVb5CIFWwAM1D

interconnect-service36:
  * ServiceId-fdfe7ec7-1ec7-4798-bb1d-1815b0d31b57
  * wEj7KGnheNnadxzLTOjOe1TlSqgOB75pEzEV5tz6xxl9

interconnect-service37:
  * ServiceId-4488b45e-992f-4479-8cc1-c7160dafb067
  * weXbJ6CkIgcY0K6Aly3yNmjVb6a7cFWhlphaiD27XMdY

interconnect-service38:
  * ServiceId-5830536e-b38e-47a4-9b2b-d3c996a545dd
  * ElMOFJEGKh6qbq1CLoImqK8gvSP0KQLyxmPlY8bZecbw

interconnect-service39:
  * ServiceId-a03d5d46-d064-41c3-b330-35dfc149333b
  * qR0PIg9jT-cPWbj8ShWmha42qXP5Qijoin8l0TfxBH8w

interconnect-service40:
  * ServiceId-8b7e2cdc-b1c6-4707-8554-7c42c7ff1276
  * VZofAdNllinmi7jQMfQlmvbbJcbpAguunzKKeanweF8c

interconnect-service41:
  * ServiceId-cda9707c-8fee-497d-a514-e593b4e01002
  * Eoj46Od3qp381LaEc5nhYj-CIGZmrJKt4Gc9oRfB1naD

interconnect-service42:
  * ServiceId-c743b5f8-5ba6-464e-86ed-83e8dd3ee1b5
  * nespdN1a1I_TQ7pwgBD2gCgtjWpHJrUigUk_69GJTCDC

interconnect-service43:
  * ServiceId-40513e4d-53e6-4dde-8baf-f3a5c82ba234
  * lYCUBuwNSyW9DNOXcBXfof4znnrZihALfdbTRvytni48

interconnect-service44:
  * ServiceId-afee12ac-c58a-433c-be98-416acbb670e2
  * 2SBqJdVgwwuBBV8k3eDg6_4NVeDBaLynQgImqct4DfFv

interconnect-service45:
  * ServiceId-65a3733a-eb0a-402b-ae91-5a412dc9725f
  * to5dKzNvpNLearwdg0KeJc-zftazx-xlu0yt1uk1Q0VP

interconnect-service46:
  * ServiceId-10413fbe-10aa-4bb5-b641-65a9bbeb9d53
  * kKyrLaYCqbhNxH-Axcv7ABcX0aGdPw-MR2nYjkVORVhY

interconnect-service47:
  * ServiceId-82ead5c9-195a-4780-bbec-b3655a475896
  * -uTIzbpCJSIn45vYZP86YtrKzpgwyQZThibltlL2rRgu

interconnect-service48:
  * ServiceId-c06741b5-0ec8-4131-8b2b-276a4f72c0a1
  * 6FpfmxrQpdD00X4_m8Jhk-r4Bwg4x47BZRnLfA-qVe67

interconnect-service49:
  * ServiceId-ee93887b-11d1-49b9-be63-2764a42beb57
  * 46ZqlkPk_n3QjTbweHa3X4HLQc4N-_O0ODYSfDHu_vui

interconnect-service50:
  * ServiceId-71dd52eb-7bbc-4ff0-aaf3-70816830660e
  * vDhkWd9DzUf7V_5cWaMhmz8IPmyshCJlZcu_tf39EyNm


