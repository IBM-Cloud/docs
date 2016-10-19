---

copyright:
  years: 2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Visão geral de recursos do {{site.data.keyword.iot_short_notm}}
{: #feature_overview}

Última atualização: 29 de junho de 2016
{: .last-updated}

O {{site.data.keyword.iot_full}} é construído com base nas áreas-chave a seguir:

  1. Connect - Conecte dispositivos e desenvolva aplicativos.
  2. Information Management - Armazene e revise dados do dispositivo e integre seu {{site.data.keyword.iot_short_notm}} a outros serviços.
  3. Analytics - Visualize dados do dispositivo de tempo real usando o painel do {{site.data.keyword.iot_short_notm}}.
  4. Risk Management - Configure conectividade e arquitetura seguras com controle de acesso para usuários e aplicativos.

## Conectar
{: #connect}

O {{site.data.keyword.iot_short_notm}} Connect é o ponto de início para qualquer serviço do {{site.data.keyword.iot_short_notm}}. Conexão de dispositivos, criação de aplicativos, controle de seus dispositivos e interatividade com serviços de terceiros estão disponíveis no {{site.data.keyword.iot_short_notm}} Connect.

### Dispositivos de gateway

Usando um gateway, é possível conectar dispositivos ao {{site.data.keyword.iot_short_notm}} que, caso contrário, não podem se conectar à Internet. Dispositivos de gateway combinam a função de um dispositivo e um aplicativo. Gateways podem receber comandos e enviar dados do dispositivo da mesma maneira que um dispositivo, mas eles também podem enviar comandos para outros dispositivos que estão conectados a ele, na mesma maneira que um aplicativo pode.

Dispositivos que não podem se conectar diretamente à Internet podem ser conectados a um dispositivo de gateway e seus dados de dispositivo podem ser enviados ao dispositivo de gateway, que por sua vez pode enviá-los a seu serviço do {{site.data.keyword.iot_short_notm}}.

### Gerenciamento de dispositivo

Os recursos de gerenciamento de dispositivo são fornecidos por meio da combinação de uma API (interface de programação de aplicativos) de gerenciamento de dispositivo e um agente de gerenciamento de dispositivo que está instalado nos dispositivos. Os dispositivos gerenciados podem executar ações de gerenciamento de dispositivo que podem ser acionadas por meio do painel principal do {{site.data.keyword.iot_short_notm}}.

O gerenciamento de dispositivo fornece a capacidade de reinicializar, fazer download e instalar atualizações de firmware, além de reconfigurar dispositivos para as configurações de fábrica remotamente, tudo isso a partir da interface com o usuário do {{site.data.keyword.iot_short_notm}}.

### Integrações de serviços de terceiros

A integração de serviço de terceiro é integrada ao {{site.data.keyword.iot_short_notm}}, incluindo suporte para os serviços de localização meteorológica da The Weather Company que permite localizar a condição meteorológica atual na localização de um dispositivo.

---

## Gerenciamento das informações
{: #information_management}

O {{site.data.keyword.iot_short_notm}} Information Management controla os dados que são enviados por dispositivos após atingirem seu serviço do {{site.data.keyword.iot_short_notm}}. Information Management inclui armazenamento de dados e transformação.

### Cache do último evento do dispositivo

Usando a API (interface de programação de aplicativos) de cache do último evento do {{site.data.keyword.iot_short_notm}}, é possível recuperar o último evento que foi enviado por um dispositivo. Isso funciona estando o dispositivo on-line ou off-line, o que permite recuperar o status do dispositivo independentemente da localização física do dispositivo ou do status de uso. Os dados do último evento de um dispositivo podem ser recuperados para qualquer evento específico que tenha ocorrido há até 365 dias.

### Armazenamento de dados do evento de dispositivo

Os dados de evento de dispositivo de seu serviço do {{site.data.keyword.iot_short_notm}} podem ser armazenados para uso posterior. O armazenamento de dados é uma primeira etapa essencial para realizar análises de dados criteriosas para obter insights a partir desses dados. Por exemplo, é possível rastrear mudanças por períodos de tempo mais longos e armazenar conjuntos de dados para uso com ferramentas de análise de dados poderosas, incluindo uso com APIs (interfaces de programação de aplicativos) do Watson e computação cognitiva.

---

## Analytics
{: #analytics}

### Visualizar dados do dispositivo de tempo real

É possível visualizar e exibir dados do dispositivo de tempo real usando cartões do painel. Os cartões do painel monitoram e exibem dados em tempo real, o que permite rastrear dispositivos ou dados do dispositivo importantes. Essas visualizações são exibidas no painel principal do {{site.data.keyword.iot_short_notm}} para fornecer acesso rápido ao contexto e status de dados do dispositivo de tempo real.

---

## Gerenciamento de Risco
{: #risk_management}

### Conectividade e arquitetura seguras

A arquitetura do {{site.data.keyword.iot_short_notm}} é projetada para evitar que dispositivos personifiquem outros dispositivos, o que mantém a integridade de seus dados do dispositivo. Os dispositivos se conectam ao {{site.data.keyword.iot_short_notm}} usando uma combinação de um ID do cliente e um token de autenticação que somente você conhece. Após os dispositivos serem registrados ou as chaves API (interface de programação de aplicativos) serem geradas, é efetuado salt e hash do token de autenticação para manter a segurança de suas credenciais. Conectividade por TLS v1.2 é totalmente suportada.

---
