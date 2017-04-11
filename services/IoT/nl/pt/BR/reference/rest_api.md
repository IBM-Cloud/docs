---

copyright:

years: 2017
lastupdated: "2017-03-16"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# APIs
{: #overview}

Várias APIs estão disponíveis para desenvolver código para dispositivos, gateways e aplicativos que se conectam ao {{site.data.keyword.iot_full}}.

As APIs HTTP são protegidas com autenticação básica HTTP. Quando você gera uma chave API usando o painel, são apresentados uma chave e um token de autenticação. Para
obter mais informações, consulte


## APIs de REST HTTP

Depois de registrar-se em sua própria organização, você receberá um ID da organização com 6 caracteres. Esse ID será necessário no nome do host para quaisquer chamadas API; a URL base para sua organização poderá ser acessada no endereço a seguir:

https://<**orgId**>.internetofthings.ibmcloud.com/api/v0002/

Para autenticar solicitações para a API do aplicativo, configure o nome do usuário para a chave API e a senha para o token de autenticação.

Para APIs de sistema de mensagens, use o endereço a seguir: https://<**orgId**>.messaging.internetofthings.ibmcloud.com:/api/v0002


## Links da API

Use os links na tabela a seguir para descobrir mais sobre as APIs fornecidas pelo {{site.data.keyword.iot_short_notm}}.

### APIs de HTTP gerais

API do                     | Use para...       
------------- | -------------
[Administração da organização ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/orgAdmin.html){: new_window} | Configurar uma organização (incluindo a criação e exclusão de dispositivos), verificar o uso, o status de serviço e diagnosticar problemas de conexão de dispositivo.
[Segurança ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/security.html){: new_window} | Gerenciar convites do usuário e autenticação, além de autorização de usuários, chaves API e dispositivos.
[Information Management ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/info-mgmt.html){: new_window} |  Acessar dados do evento de dispositivo, bem como obter e atualizar a localização do dispositivo e obter informações do clima para esse local. **Nota:** as informações do clima dependem da integração da The Weather Company.
[A Weather Company ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/info-mgmt.html#!/Device_Location_Weather){: new_window} | Integrar dados da The Weather Company aos dispositivos existentes.
[Analítica ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/analytics.html){: new_window} | Criar regras, alertas e ações para os dados que vêm para o {{site.data.keyword.iot_short_notm}} de dispositivos.
[Gerenciamento de dispositivo ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/device-mgmt.html){: new_window} | Interagir com dispositivos gerenciados usando o protocolo de gerenciamento de dispositivo.
[Sistema de mensagens ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/http-messaging.html){: new_window}   | Publicar eventos e enviar comandos usando HTTP. **Nota:** para APIs de sistema de mensagens, use o endereço https://<**orgId**>.messaging.internetofthings.ibmcloud.com:/api/v0002



### APIs HTTP de extensão

API do                     | Use para...       
------------- | -------------
[Extensão AT&T ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/ext-atnt.html){: new_window} | Administrar dispositivos AT&.
[Extensão Jasper ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/ext-jasper.html){: new_window} | Administrar dispositivos Jasper.
[Extensão Orange ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/ext-orange.html){: new_window} | Visualizar dados do cartão SIM de dispositivos que estão conectados à sua organização do {{site.data.keyword.iot_short_notm}} e têm um cartão SIM da Orange instalado.

### APIs HTTP Beta

API do                     | Use para...       
------------- | -------------
[Segurança do gateway ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html){: new_window}   | Verificar e designar funções para dispositivos de gateway.
[Segurança do dispositivo ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-devices-beta.html){: new_window} | Verificar e designar funções para dispositivos.
[Mapeamento de interface ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html){: new_window}   |   Mapear e acessar dados do dispositivo usando interfaces.
