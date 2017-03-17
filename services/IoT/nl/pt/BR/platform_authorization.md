---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-17"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Conexão do Aplicativo

Para conectar seu aplicativo ao {{site.data.keyword.iot_full}}, deve-se conectar usando chaves API (interface de programação de aplicativos) e tokens ou fazendo a ligação de seu aplicativo diretamente com o {{site.data.keyword.iot_short_notm}} no {{site.data.keyword.Bluemix_notm}}. O painel de acesso é usado para conceder acesso.
{:shortdesc}

## Conexão da chave API
{: #api-key}
As chaves API (interface de programação de aplicativos) são usadas ao conectar aplicativos à sua organização do {{site.data.keyword.iot_short_notm}}. Os aplicativos requerem uma chave API (interface de programação de aplicativos) para se conectarem a uma organização e um token de autenticação exclusivo que deve ser usado com essa chave API.  

Para obter mais informações sobre as conexões de aplicativo, consulte [Conectividade de MQTT para aplicativos ![Ícone de link
externo](../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/applications/mqtt.html){: new_window} na documentação do desenvolvedor.

Para criar um novo par de chave API (interface de programação de aplicativos) e token de autenticação:  
1.	No painel do {{site.data.keyword.iot_short_notm}}, acesse **Aplicativos > Chaves API (interface de programação de aplicativos)**.  
2.	Clique em **Gerar chave de API**.  
**Importante:** tome nota do par de chave API (interface de programação de aplicativos) e token. Os tokens de autenticação não são recuperáveis. Se você perder ou esquecer esse token, será necessário registrar a chave API (interface de programação de aplicativos) novamente para gerar um novo token de autenticação.
 - Um exemplo de uma chave API (interface de programação de aplicativos) é `a-organization_id-a84ps90Ajs`  
 - Um exemplo de token é `MP$08VKz!8rXwnR-Q*`  
3.	Inclua um comentário para identificar a chave API (interface de programação de aplicativos) no painel, por exemplo: chave para conectar meu aplicativo.
4.	Clique em **Concluir**.



## Conexão de ligação do Bluemix
{: #bluemix-binding}
É possível fazer a ligação de aplicativos com sua organização do {{site.data.keyword.iot_short_notm}} a partir do {{site.data.keyword.Bluemix_notm}}. Ao fazer a ligação do aplicativo, ele poderá se comunicar apenas com instâncias de serviço no mesmo espaço ou organização. É possível localizar todos os dados necessários para que o aplicativo se comunique com a instância de serviço na variável de ambiente VCAP_SERVICES. Se o aplicativo estiver ligado a vários serviços, a variável VCAP_SERVICES incluirá as informações de conexão de cada instância de serviço.  

No entanto, é possível usar instâncias de serviço de outros espaços ou organizações da mesma maneira que um app externo. Em vez de criar uma ligação, use as credenciais para configurar sua instância do app diretamente. Para obter mais informações, consulte [Solicitando uma nova instância de serviço](https://console.{DomainName}/docs/services/reqnsi.html#req_instance) na documentação do {{site.data.keyword.Bluemix_notm}}.

Para ver detalhes dos aplicativos Bluemix ligados à instância de serviço do Bluemix associada à sua organização, acesse **Aplicativos > Aplicativos Bluemix**.  
