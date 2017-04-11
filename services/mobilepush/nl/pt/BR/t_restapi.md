---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Usando
APIs REST
{: #push-api-rest}
Última atualização: 16 de janeiro de 2017
{: .last-updated}

É possível usar uma API (interface de programação de aplicativos) REST (Representational State Transfer) para {{site.data.keyword.mobilepushshort}}. Também é possível usar o SDK e a [API de Push ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://mobile.{DomainName}/imfpush/){: new_window} para desenvolver adicionalmente seus aplicativos clientes.

Com a API REST de Push, aplicativos do servidor de backend e clientes podem acessar funções {{site.data.keyword.mobilepushshort}}.

- Registros de dispositivo
- Registros
- Messages
- Subscriptions
- Marcações
- Webhooks

Para obter a URL base para a API REST, conclua as etapas:

1. Crie um aplicativo backend no catálogo do Bluemix® da seção Modelos escolhendo o MobileFirst Services Starter. Isso liga o serviço {{site.data.keyword.mobilepushshort}} ao aplicativo. Também é possível criar uma instância de serviço de Push e deixá-la sem limites. 
1. Na página principal do painel Bluemix, acesse a área **Aplicativos** e, em seguida, selecione seu app.
3. Clique em **OPÇÕES MÓVEIS**. Os valores de GUID (Identificador Exclusivo Global)
de rota e de app são exibidos no início da página de detalhes do seu app. A tela Mostrar credenciais mostra
informações sobre o AppSecret. É possível obter o segredo do aplicativo em Opções móveis e também o segredo do cliente para algumas das APIs.

Também é possível usar a linha de comandos para obter as credenciais de serviço:

```
    cf create-service-key {push_instance_name} {key_name}

 cf service-key {push_instance_name} {key_name}
```
	{: codeblock}

## Aceitar cabeçalho do idioma
{: #push-api-rest-accept}

O cabeçalho "Accept-Language" especifica qual idioma usar para as mensagens de erro que são produzidas pela [API de REST Push ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://mobile.{DomainName}/imfpush/){: new_window}. Os idiomas a seguir são suportados para as mensagens de erro: chinês (simplificado), chinês (tradicional), inglês (EUA), alemão, francês, italiano, japonês, coreano, português e espanhol.

## appSecret 
{: #push-api-rest-secret}

Quando um aplicativo é ligado ao {{site.data.keyword.mobilepushshort}}, o serviço gera um appSecret (uma chave exclusiva) e passa-o no cabeçalho de resposta. Se
você estiver usando a API de REST do IBM {{site.data.keyword.mobilepushshort}} for Bluemix, use a referência da API de REST para obter informações sobre quais
APIs você precisa assegurar. Para obter informações, veja a [API de REST Push ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://mobile.{DomainName}/imfpush/){: new_window}.

O cabeçalho da solicitação deve conter o appSecret. Caso contrário, o servidor retornará um código de erro 401 Desautorizado. Quando o {{site.data.keyword.mobilepushshort}} é incluído em um aplicativo, um AppID específico é criado. Como parte da resposta, você obtém um cabeçalho chamado appSecret que é usado para criar tags ou enviar
mensagens. A operação acontece por meio de serviços no catálogo ou do modelo.

Para obter o valor appSecret:

1. Clique no* app-name* que está ligado ao serviço de push.
2. Clique no link **Mostrar credenciais** para exibir o appSecret (AppID).

A tela **Mostrar credenciais** mostra informações sobre o AppSecret:
```
	{
    "imfpush_Dev": [
   {
     "name": "testapp1",
     "label": "imfpush_Dev",
     "plan": "Basic",
     "credentials": {
       "url": "http://imfpush.ng.bluemix.net/imfpush/v1/apps/b615b280-b37e-4042-8815-38a758f234e2",
       "admin_url": "//mobile.ng.bluemix.net/imfpushdashboard/?appGuid=b615b280-b37e-4042-8815-38a758f234e2",
       "appSecret": "8dac71a5-2219-42b3-a9f3-dbb828ba1f04",
       }
     }
    ]
    }
```
	{: codeblock} 


##Filtros de API REST de Push
{: #push-api-rest-filters}

Filtros definem um critério de procura que restringe os dados retornados de uma API GET de {{site.data.keyword.mobilepushshort}}. Aplique os filtros no resultado da operação Get que deseja filtrar. O filtro restringe o número de entradas incluídas no resultado. Por exemplo, é possível usar um filtro para procurar tags iniciadas com "test". 

É possível gerar filtros usando a sintaxe a seguir:

**nome**: o nome do campo no qual o filtro está sendo aplicado.

**operador**: == (correspondência exata) ou =@ (contém
subsequência) que descreve a correspondência de filtro a ser usada.

**expressão**: os valores a serem incluídos no resultado.

Quando uma vírgula e uma barra invertida são exibidas em uma expressão, elas devem ser escapadas com barra invertida.

Ao usar múltiplos filtros, eles podem ser combinados usando as lógicas AND e OR.

- Para a lógica AND, use vários filtros na consulta.
- Para a lógica OR, use uma vírgula (,) dentro da expressão de filtro.
- Para as lógicas AND e OR: uma única consulta pode ter a lógica AND e OR. Cada filtro é avaliado individualmente antes que os filtros sejam combinados em uma expressão AND.

Para a API GET do dispositivo, as combinações a seguir são suportadas: - O nome é o campo de plataforma.
- Exceto para a plataforma, o operador pode ser == ou =@
- Para a plataforma, o operador deve ser ==. Se o operador =@ for usado, o valor poderá ser uma subsequência.
- Se == for usado, o valor deverá ser uma sequência correspondente exata.

Para a API GET da assinatura, as combinações a seguir são suportadas:

- O nome pode ser um destes campos: tagName ou deviceId
- Exceto para a plataforma, o operador pode ser == ou =@
- Para a plataforma, o operador deve ser ==
- Se o operador =@ for usado, o valor poderá ser uma subsequência. Se o operador == for usado, o valor deverá ser uma sequência de correspondência exata.
- Para a API GET de identificação, as combinações a seguir são suportadas:
- O nome pode ser um destes campos: “name” ou “description”
- Se o operador =@ for usado, o valor poderá ser uma subsequência.
- Se == for usado, o valor deverá ser uma sequência correspondente exata.


##Códigos de resposta do {{site.data.keyword.mobilepushshort}}
{: #push-api-response-codes}

Status: 405 Método não permitido - Método apropriado esperado.
