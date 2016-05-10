---

copyright:
 years: 2015, 2016

---

# Usando APIs REST
{: #push-api-rest}

É possível usar uma API (interface de programação de aplicativo) REST (Representational State Transfer) para notificações push. É possível também usar o SDK e a [API Push](https://mobile.{DomainName}/imfpushrestapidocs/) para desenvolver melhor seus aplicativos cliente.

Com a API REST Push, aplicativos do servidor backend e clientes podem acessar funções Push.

- Registros de dispositivo
- Registros
- Messages
- Subscriptions
- Marcações

Para obter a URL base para a API REST:

1. Crie um aplicativo backend no catálogo do Bluemix® da seção Modelos que ligará automaticamente o serviço de Push a esse aplicativo. Se também já tiver criado um app backend, certifique-se de ligar o app ao Push Notification Service. 

1. Na página principal do painel Bluemix, acesse a área **Aplicativos** e depois clique em seu app.

3. Clique em OPÇÕES MÓVEIS. Os valores rota e GUID do app são exibidos na parte superior da página de detalhes do app.



## Aceitar cabeçalho do idioma
{: #push-api-rest-accept}

O cabeçalho "Accept-Language" especifica qual idioma a ser usado para mensagens de erro geradas pela [API
REST de Push](https://mobile.{DomainName}/imfpushrestapidocs/){: new_window}. Os idiomas a seguir são suportados para as mensagens de erro: chinês (simplificado), chinês (tradicional), inglês (EUA), alemão, francês, italiano, japonês, coreano, português e espanhol.

## appSecret
{: #push-api-rest-secret}

Quando um aplicativo é ligado ao Push Notifications, o serviço gera um appSecret (uma chave exclusiva) e o transmite no cabeçalho de resposta. Se você estiver usando a API REST do IBM® Push Notifications for Bluemix, use a referência da API REST para obter informações sobre quais APIs precisa proteger. Para obter informações sobre a API REST, consulte a Referência de API REST.

O cabeçalho da solicitação deve conter o appSecret. Caso contrário, o servidor retornará um código de erro 401 Desautorizado. Quando o Push Notification é incluído em um aplicativo, um AppID específico é criado. Como parte da resposta, você obtém um cabeçalho chamado appSecret que é usado para criar tags ou enviar mensagens. A operação acontece por meio de serviços no catálogo ou do modelo.

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
       "appSecret": "8dac71a5-2219-42b3-a9f3-dbb828ba1f04"  
       }
   }
 ]
}
``` 

##Filtros de API REST de Push
{: #push-api-rest-filters}

Filtros definem um critério de procura que restringe os dados retornados de uma API GET de Push. Aplique os filtros no resultado da operação Get que deseja filtrar. O filtro restringe o número de entradas incluídas no resultado. Por exemplo, é possível usar um filtro para procurar uma tag cujo nome seja iniciado com "test". É possível gerar um filtro usando a sintaxe a seguir.

**nome** O nome do campo ao qual o filtro está sendo aplicado.

**operador** == (correspondência exata) ou =@ (contém subsequência) que descreve a correspondência de filtro a ser usada.

**expressão** Os valores a serem incluídos no resultado.

Quando uma vírgula e uma barra invertida são exibidas em uma expressão, elas devem ser escapadas com barra invertida.

Ao usar vários filtros, eles podem ser combinados usando a lógica AND e OR.\

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
