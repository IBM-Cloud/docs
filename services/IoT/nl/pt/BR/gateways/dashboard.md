---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-10"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Conectando gateways
{: #IoT_connectGateway}

Antes que possa iniciar o recebimento de dados de dispositivos conectados a seus gateways, deve-se conectar o gateway ao {{site.data.keyword.iot_full}}. Conectar um gateway ao {{site.data.keyword.iot_short_notm}} envolve a criação de um tipo de dispositivo de gateway e o registro do gateway com o {{site.data.keyword.iot_short_notm}}. É possível usar então as informações de registro para conectar o gateway ao {{site.data.keyword.iot_short_notm}}.
{:shortdesc}

Gateways são uma classe especializada de dispositivos no {{site.data.keyword.iot_short_notm}}. Gateways servem como pontos de acesso ao {{site.data.keyword.iot_short_notm}} para outros dispositivos.


## Antes de iniciar
{: #Prerequisites}

Dispositivos de gateway têm permissões adicionais quando comparados a dispositivos regulares e podem executar as funções a seguir:
- Registrar novos dispositivos no {{site.data.keyword.iot_short_notm}}
- Enviar e receber seus próprios dados de sensor como um dispositivo diretamente conectado
- Enviar e receber dados em nome dos dispositivos conectados a ele
- Executar um agente de gerenciamento de dispositivo para que possa ser gerenciado e também gerenciar os dispositivos conectados a ele.  
Para obter informações para o desenvolvedor de gateway, consulte [Conectividade MQTT para gateways](mqtt.html).

Também é possível usar gateways para executar Edge Analytics nos dados que os dispositivos de gateway estão enviando. Para obter mais informações, consulte [Edge Analytics](../edge_analytics.html) e [Instalando o Edge Analytics Agent](#edge).

## Etapa 1: registrando o gateway com o {{site.data.keyword.iot_short_notm}}  
{: #register_gateway}

O registro de um gateway envolve classificar o dispositivo como um tipo de gateway, dando ao gateway um nome e fornecendo informações do gateway. Em seguida, você fornece um token de conexão ou aceita um token que é gerado pelo {{site.data.keyword.iot_short_notm}}.

**Dica:** é possível incluir gateways um por vez a partir do painel do {{site.data.keyword.iot_short_notm}} ou usar a [API do {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Bulk_Operations/post_bulk_devices_add) para incluir um ou mais gateways por vez.

Para incluir um gateway a partir do painel do {{site.data.keyword.iot_short_notm}}:

1. No painel do {{site.data.keyword.iot_short_notm}}, selecione **Dispositivos**.
2. Clique em **Incluir dispositivo**.
3. Selecione ou crie um tipo de dispositivo para o dispositivo que você está incluindo.  
Cada dispositivo conectado ao {{site.data.keyword.iot_short_notm}} deve estar associado a um tipo de dispositivo. Tipos de dispositivos são grupos de dispositivos que compartilham características.  
 1. Clique em **Criar tipo de dispositivo**, em seguida, em **Criar tipo de gateway**.
 2. Insira um nome de tipo de dispositivo como `my_gateway_type` e uma descrição para o tipo de gateway.   
 **Importante:** O nome de tipo de dispositivo deve ter no máximo 36 caracteres e pode conter apenas:
 <ul>
  <li>Caracteres alfanuméricos (a-z, A-Z, 0-9)</li>
  <li>Hifens (-)</li>
  <li>Sublinhados (&lowbar;)</li>
  <li>Pontos (.)</li>
  </ul>3. Opcional: Insira metadados e atributos de tipo de gateway.    
 **Dica:** é possível incluir e editar atributos e metadados posteriormente.
 4. Clique em **Criar** para incluir o novo tipo de gateway.
10. Clique em **Avançar** para iniciar o processo de incluir seu dispositivo de gateway com o tipo de gateway selecionado.
11. Insira um ID do dispositivo, como `my_gateway_device`.  
O ID do dispositivo é usado para identificar o dispositivo de gateway no painel do {{site.data.keyword.iot_short_notm}} e também é um parâmetro necessário para conectar seu dispositivo de gateway ao {{site.data.keyword.iot_short_notm}}.  
**Importante:** O ID do dispositivo deve ter no máximo 36 caracteres e pode conter apenas:
 <ul>
 <li>Caracteres alfanuméricos (a-z, A-Z, 0-9)</li>
 <li>Hifens (-)</li>
 <li>Sublinhados (&lowbar;)</li>
 <li>Pontos (.)</li>  
 </ul>
 **Dica:** para dispositivos conectados à rede, o ID do dispositivo poderia, por exemplo, ser o endereço de Controle de Acesso à Mídia do dispositivo sem dois pontos separando.  
12. Opcional: clique em **Campos adicionais** para incluir informações de dispositivo de gateway, como número de série, fabricante, modelo, etc.  
 **Dica:** é possível incluir e editar essas informações posteriormente.
12. Opcional: insira os metadados JSON do dispositivo.  
 **Dica:** é possível incluir e editar metadados do dispositivo posteriormente.
13. Clique em **Avançar** para concluir a inclusão de seu dispositivo de gateway.
14. Verifique se as informações de resumo estão corretas e, em seguida, clique em **Incluir** para incluir o dispositivo de gateway.  
**Dica:** você tem a opção para aceitar um token de autenticação gerado automaticamente ou você mesmo fornecer um token de autenticação. Se você optar por criar seu próprio token, certifique-se de que tenha entre oito e 36 caracteres de comprimento, contenha uma combinação de letras minúsculas e maiúsculas, números e hífen, sublinhado ou ponto. O token não deve conter sequências de caracteres repetidos, palavras de dicionário, nomes de usuário ou outras sequências predefinidas.
15. Na página de informações do dispositivo, copie e salve as informações do dispositivo a seguir:  
 - ID da organização, como `tubo8x`
 - Tipo de dispositivo, como `my_gateway_type`
 - ID do dispositivo. **Dica:** para dispositivos conectados à rede, isso poderia por exemplo ser o endereço de Controle de Acesso à Mídia (MAC) sem dois pontos separando.
 - Método de autenticação, como `token`
 - Token de autenticação, como `PtBVriRqIg4uh)_-Kl`  
  **Dica:** você precisará do ID da organização, do Token de autenticação, do Tipo de dispositivo e do ID do dispositivo para configurar seu dispositivo para se conectar ao {{site.data.keyword.iot_short_notm}}.  

Parabéns, você registrou seu dispositivo de gateway. Agora é possível configurar seu dispositivo de gateway para se conectar ao {{site.data.keyword.iot_short_notm}}

Consulte a orientação [Como registrar gateways no IBM Watson IoT Platform](https://developer.ibm.com/recipes/tutorials/how-to-register-gateways-in-ibm-watson-iot-platform/) para obter instruções passo a passo que demonstram o fluxo necessário para registrar um gateway.

## Etapa 2: conectando seu gateway ao {{site.data.keyword.iot_short_notm}}
{: #connect_gateway}

Após registrar um gateway com o {{site.data.keyword.iot_short_notm}}, use as informações de registro para conectar o gateway ao {{site.data.keyword.iot_short_notm}} e iniciar o recebimento de dados de dispositivos conectados ao gateway.

Para obter informações sobre como conectar seu gateway ao {{site.data.keyword.iot_short_notm}}, consulte [Conectividade MQTT para gateways](mqtt.html).

**Dica:** há uma gama de receitas disponíveis para conectar dispositivos ao {{site.data.keyword.iot_short_notm}}. Para obter uma lista de receitas, consulte as [Receitas de conexão de dispositivo](https://developer.ibm.com/recipes/tutorials/category/internet-of-things-iot/) que estão disponíveis em IBM.com.


## Etapa 3: conectando dispositivos por meio do gateway
{: #gateway_devices}

Os dispositivos conectados ao gateway são automaticamente incluídos no {{site.data.keyword.iot_short_notm}} quando o gateway publica mensagens do dispositivo. O tipo de dispositivo e o dispositivo em si são criados automaticamente quando o gateway publica uma mensagem para uma combinação de tipo de dispositivo e ID do dispositivo que ainda não existe.

Para obter informações sobre registro automático de dispositivo e publicação e recebimento de dados para dispositivos conectados, consulte [Conectividade MQTT para gateways](mqtt.html).


Quando um dispositivo é conectado com sucesso a seu gateway, ele é exibido no painel de sua organização do {{site.data.keyword.iot_short_notm}}.

Consulte a orientação [Conectando o Raspberry Pi como um gateway ao Watson IoT](https://developer.ibm.com/recipes/tutorials/connecting-raspberry-pi-as-a-gateway-to-watson-iot-using-node-red/) para obter o fluxo e a descrição detalhados. 

**Nota:** no painel do {{site.data.keyword.iot_short_notm}}, dispositivos e gateways conectados diretamente ao {{site.data.keyword.iot_short_notm}} exibem um ícone de status para indicar que estão conectados. O painel exibe dispositivos que estão conectados indiretamente por meio de um gateway como desconectados, pois não tem qualquer conhecimento de uma conectividade de dispositivos com o gateway.


## Instalando o Edge Analytics Agent
{: #edge}

O Edge Analytics Agent (EAA) é um componente de software construído com base no [Apache Quarks](http://quarks.incubator.apache.org/) para realizar opções de Edge Analytics em um gateway fazendo upload e gerenciando regras de Edge Analytics a partir do painel do {{site.data.keyword.iot_short_notm}}. Para obter mais informações sobre Edge Analytics, consulte [Edge Analytics](../edge_analytics.html).

### Instalando o EAA
{: #eaa_install}

Para instalar o EAA em seu gateway:
1. No painel do {{site.data.keyword.iot_short}}, acesse **Regras**.
2. Clique em **Fazer download do Edge Agent** para acessar a [Comunidade do IBM Edge Analytics Agent](https://www.ibm.com/developerworks/community/groups/service/html/communitystart?communityUuid=3df173af-0c21-4b9c-9fd1-e8e5561ef460&ftHelpTip=true).
3. Navegue até a seção **Arquivos** e faça download do arquivo compactado *ibm-watson-iot-edge-analytics-dslink-java-0.0.1*.
4. Para obter informações sobre como instalar e configurar o componente de software EAA em seu gateway, consulte a receita a seguir:
 - [Introdução a Edge Analytics no Watson IoT Platform](https://developer.ibm.com/recipes/?post_type=pnext_tutorial&p=19472)

### Definições de configuração do EAA
{: #eaa_configuration}

É possível usar o arquivo config.properties do EAA para configurar os parâmetros básicos de configuração de software.

Para atualizar a configuração do EAA:
1. No sistema de gateway no qual o EAA está em execução, localize o arquivo config.properties do EAA.  
Por exemplo:
`../dglux-server/dslinks/ibm-watson-iot-edge-analytics-dslink-java-0.0.1/config.properties`
2. Antes de iniciar a edição das configurações, faça uma cópia de backup do arquivo.
3. Abra o arquivo config.properties para edição.
4. Edite os parâmetros de configuração para seu ambiente:
 <dl>
 <dt>DataDirectSendEnable</dt>
 <dd>BOOLEAN (true|false)</br>
 TRUE (padrão) - Enviar todos os dados ao {{site.data.keyword.iot_short_notm}}.</br>
 FALSE - Enviar dados ao {{site.data.keyword.iot_short_notm}} somente se as regras estiverem configuradas no mecanismo. </dd>
 <dt>Intervalo de Monitoramento</dt>
 <dd>INTEGER (milliseconds)</br>
 O tempo em milissegundos antes que uma nova mensagem de monitoramento seja enviada ao {{site.data.keyword.iot_short_notm}}. </br>
 Configure um valor pequeno para relatar métricas do monitor mais vezes. Configure um valor grande para ter informações mais detalhadas de monitoramento sobre o {{site.data.keyword.iot_short_notm}}. </br>
 DEFAULT: 60000    </br>
 RECOMMENDED RANGE: [1000, 360000]</dd>
 <dt>MonitorLogDesample</dt>
 <dd>INTEGER  </br>
 Razão da reversão da amostragem entre o número de mensagens de monitoramento enviadas ao {{site.data.keyword.iot_short_notm}} em comparação às mensagens inseridas no log local. Por exemplo, se `MonitorLogDesample` estiver configurado para 10, somente uma entrada de log local será gravada para cada dez mensagens enviadas ao {{site.data.keyword.iot_short_notm}}. </br>Um número grande mantém o log local pequeno. Um número pequeno fornece um log local mais detalhado.</br>
 DEFAULT: 10</br>
 RECOMMENDED RANGE: [1, 100]</dd>
 <dt>MemoryAlertThreshold</dt>
 <dd>INTEGER (Megabytes)</br>
 O limite de memória heap da JVM livre no qual uma mensagem de log de aviso de memória é enviada ao log de diagnósticos do {{site.data.keyword.iot_short_notm}}. O alerta é acionado pelo monitoramento. </br>Um valor pequeno reduz o número de mensagens de alerta enviadas ao {{site.data.keyword.iot_short_notm}}. Um valor grande fornece um aviso antecipado se o servidor do EAA estiver começando a ter problemas de memória.</br>**Dica:** é possível usar as regras de [Cloud Analytics](../cloud_analytics.html) para configurar ações de alerta, como notificações por e-mail para alertá-lo sobre problemas de memória. Para obter informações sobre as propriedades disponíveis que podem ser usadas para construir regras, consulte [Métricas de diagnóstico do Edge Analytics Agent](../edge_analytics.html#eaa_metrics).</br>
  DEFAULT: 10</br>
 RECOMMENDED RANGE: [10 or 5% of the total memory, 200]</dd>
 </dl>
5. Salve o arquivo editado e, em seguida, reinicie o EAA.

Amostra do arquivo config.properties do EAA
```
#######################################################################
# Engine Parameters
#######################################################################
# DataDirectSendEnable
#                    - BOOLEAN(true|false) Set to true to forward all
#                      the data; Set to false to disable data direct
#                      send to IOTP when there is no rule set in the
#                      engine.
#                      DEFAULT: true
#######################################################################
DataDirectSendEnable=true

#######################################################################
# Monitoring Parameters
#######################################################################
# MonitorInterval    - INTEGER Time interval in milliseconds before a  
#                      new monitoring message is generated. Set it to a
#                      small value to report the monitor metrics more
#                      frequently. Set it to a big value to have more
#                      detailed monitoring information on IoTP.
#                      DEFAULT: 60000    RECOMMEND: [1000, 360000]
# MonitorLogDesample - INTEGER The de-sampling ratio of the number of
#                      monitoring messages sent to IOTP vs. local log,
#                      i.e. number of monitoring messages N where
#                      EAA would output only one to the Info log for
#                      every N messages. Set it big to keep the size
#                      of the log small. Set it small to have detailed
#                      monitoring information in local log.
#                      DEFAULT: 10       RECOMMEND: [1, 100]
# MemoryAlertThreshold
#                    - INTEGER the free JVM heap memory in megabyte under
#                      which a log message would be generated and send to
#                      IOTP diagnosis log. The alert is driven by the
#                      monitoring. Set it small to eliminate unnecessary
#                      alert message on IoTP. Set it big to receive early
#                      alert when the system is likely to crash. Set to
#                      Min(Max(10MB, 5% of the total memory), 200MB) is
#                      recommended.
#                      DEFAULT: 10       RECOMMEND: [10, 200]
#######################################################################

MonitorInterval=60000
MonitorLogDesample=10
MemoryAlertThreshold=10
```
