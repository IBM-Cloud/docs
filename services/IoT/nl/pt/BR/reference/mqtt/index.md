---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-11-18"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Sistema de mensagens MQTT
{: #ref-mqtt}

MQTT é o protocolo primário que dispositivos e aplicativos usam para se comunicar com o {{site.data.keyword.iot_full}}. MQTT é um protocolo de transporte de sistema de mensagens de publicação e assinatura projetado para a troca eficiente de dados em tempo real entre sensor e dispositivos móveis.
{:shortdesc}

MQTT é executado por TCP/IP e, embora seja possível codificar diretamente para TCP/IP, também é possível optar por usar uma biblioteca que manipula os detalhes do protocolo MQTT para você. Uma ampla gama de bibliotecas do cliente MQTT está disponível. A IBM contribui para o desenvolvimento e suporte de diversas bibliotecas do cliente, incluindo aquelas que estão disponíveis nos sites a seguir:

- [Wiki da comunidade MQTT](https://github.com/mqtt/mqtt.github.io/wiki)
- [Projeto Eclipse Paho](http://eclipse.org/paho/)

## Suporte à versão
{: #version-support}
Para obter informações sobre as versões do MQTT que são suportadas pelo {{site.data.keyword.iot_short_notm}}, consulte [Padrões e requisitos](../standards_and_requirements.html#mqtt).

## Clientes de aplicativo, dispositivo e gateway
{: #device-app-clients}

No {{site.data.keyword.iot_short_notm}}, as principais classes de coisas são dispositivos e aplicativos. Um gateway é uma subclasse de dispositivo.

O cliente MQTT se identifica para o serviço {{site.data.keyword.iot_short_notm}} como uma classe de coisa. A classe de coisa determina os recursos do cliente quando ele está conectado. A classe de coisa também determina o mecanismo para a autenticação de cliente.

Aplicativos e dispositivos funcionam com espaços de tópico MQTT diferentes.  Os dispositivos funcionam dentro de um espaço de tópico com escopo do dispositivo, enquanto os aplicativos têm acesso total ao espaço de tópico para uma organização inteira. Para obter informações adicionais, consulte os
seguintes tópicos:

- [Sistema de mensagens MQTT para dispositivos](../../devices/mqtt.html)
- [Sistema de mensagens MQTT para aplicativos](../../applications/mqtt.html)
- [Sistema de mensagens MQTT para gateways](../../gateways/mqtt.html)

### Mensagens retidas
O {{site.data.keyword.iot_short_notm}} fornece suporte limitado para o recurso de mensagens retidas de sistema de mensagens MQTT. Se a sinalização de mensagem retida estiver configurada como true em uma mensagem MQTT enviada de um dispositivo, um gateway ou um aplicativo para o {{site.data.keyword.iot_short_notm}}, a mensagem será manipulada como uma mensagem não retida. As organizações do {{site.data.keyword.iot_short_notm}} não estão autorizadas a publicar mensagens retidas. O serviço {{site.data.keyword.iot_short_notm}} substituirá a sinalização de mensagem retida quando ela estiver configurada como true e processará a mensagem como se a sinalização de mensagem retida estivesse configurada como false.

## Níveis de qualidade de serviço
{: #qos-levels}

O protocolo MQTT fornece três qualidades de serviço para entregar mensagens entre clientes e servidores: "no máximo uma vez", "pelo menos uma vez" e "exatamente uma vez".
Embora seja possível enviar eventos e comandos usando qualquer nível de qualidade de serviço, deve-se considerar cuidadosamente qual é o nível de serviço correto para suas necessidades. O nível '2' da qualidade de serviço não é sempre uma opção melhor que o nível '0'.

### No máximo uma vez (QoS0)

O nível da qualidade de serviço "no máximo uma vez" (QoS0) é o modo mais rápido de transferência e às vezes é chamado de "disparar e esquecer". A mensagem é entregue no máximo uma vez ou pode não ser entregue definitivamente. A entrega pela rede não é reconhecida e a mensagem não é armazenada. A mensagem poderá ser perdida se o cliente for desconectado ou se o servidor falhar.

O protocolo MQTT não requer servidores para encaminhar publicações no nível '0' de qualidade de serviço para um cliente. Se o cliente estiver desconectado no momento em que o servidor recebe a publicação, a publicação poderá ser descartada, dependendo da implementação do servidor.

**Dica:** ao enviar dados em tempo real em um intervalo, use a qualidade de serviço de nível 0. Se uma única mensagem desaparecer, não importa muito porque outra mensagem contendo dados mais novos será enviada pouco depois. Neste cenário, o custo extra de usar uma qualidade de serviço mais alta não resulta em qualquer benefício tangível.

### Pelo menos uma vez (QoS1)

Com qualidade de serviço de nível 1 (QoS1), a mensagem é sempre entregue pelo menos uma vez. Se uma falha ocorrer antes de um reconhecimento ser recebido pelo remetente, uma mensagem poderá ser entregue várias vezes. A mensagem deve ser armazenada localmente no emissor até que o remetente receba confirmação de que a mensagem foi publicada pelo destinatário. A mensagem é armazenada para o caso de ser necessário enviá-la novamente.

### Exatamente uma vez (QoS2)

O nível 2 da qualidade de serviço (QoS2) "exatamente uma vez" é o mais seguro, mas o modo mais lento de transferência. A mensagem é sempre entregue exatamente uma vez e também deve ser armazenada localmente no remetente, até que o remetente receba confirmação de que a mensagem foi publicada pelo destinatário. A mensagem é armazenada para o caso de ser necessário enviá-la novamente. Com a qualidade de serviço de nível 2, uma sequência de handshaking e confirmação mais sofisticada é usada do que para o nível 1 para assegurar que as mensagens não sejam duplicadas.

**Dica:** ao enviar comandos, se você desejar confirmação de que apenas o comando especificado será acionado e que será acionado apenas uma vez, use a qualidade de serviço de nível 2. Este é um exemplo de quando s sobrecargas adicionais de nível 2 podem ser vantajosas com relação aos outros níveis.

## Buffers de assinatura e sessão de limpeza
{: #subscription-buffers-and-clean-session}

A cada assinatura de um dispositivo ou aplicativo é alocado um buffer de 5000 mensagens.  O buffer permite que qualquer aplicativo ou dispositivo fique para trás dos dados ativos que está processando e também construa uma lista não processada de até 5000 mensagens pendentes para cada assinatura que fez. Quando o buffer estiver cheio, as mensagens mais antigas serão descartadas quando uma nova mensagem for recebida.

Use a opção da sessão de limpeza MQTT para acessar o buffer de assinatura. Quando a sessão de limpeza for configurada para falso, o assinante receberá mensagens do buffer. Quando a sessão de limpeza for configurada para verdadeiro, o buffer será reconfigurado.

**Nota:** o limite do buffer de assinatura se aplica independentemente da configuração da qualidade de serviço usada. É possível que uma mensagem enviada no nível 1 ou 2 não seja entregue a um aplicativo que seja incapaz de acompanhar a taxa de mensagens para a assinatura que ele fez.

## Limitações da carga útil da mensagem
{: #message-payload}

O {{site.data.keyword.iot_short_notm}} suporta envio e recebimento de mensagens em qualquer formato permitido pelo padrão MQTT. MQTT é agnóstico com relação a dados, portanto, é possível enviar imagens, textos em qualquer codificação, dados criptografados e praticamente todo tipo de dados em formato binário. No entanto, há algumas limitações para casos de uso específicos.   

Há também limitações de tamanho para a carga útil da mensagem no {{site.data.keyword.iot_short_notm}}.

### Restrições de formato de carga útil da mensagem

A carga útil da mensagem pode conter qualquer sequência válida, no entanto, os formatos JSON ("json"), texto ("text") e binário ("bin") são mais comumente usados que outros tipos de formato.

A tabela a seguir esboça as restrições de carga útil da mensagem para diferentes tipos de formato:

Formato da carga útil  | Diretrizes para casos de uso específicos
--------- | ----------  
JSON | JSON é o formato padrão para o {{site.data.keyword.iot_short_notm}}. Se planeja usar os painéis, placas e cartões integrados do {{site.data.keyword.iot_short_notm}}, além da análise de dados, assegure que o formato da carga útil da mensagem se adeque a texto JSON bem formado.
Texto (Text) | Use codificação de caracteres UTF-8 válida.
Binary | Sem restrições.


### Tamanho máximo de carga útil da mensagem

**Importante:** o tamanho máximo de carga útil no {{site.data.keyword.iot_short_notm}} é 131072 bytes. Mensagens com uma carga útil maior que o limite são rejeitadas. O cliente de conexão também é desconectado e uma mensagem aparece nos logs de diagnóstico, conforme esboçado no exemplo de mensagem do dispositivo a seguir:

`Closed connection from x.x.x.x. The message size is too large for this endpoint.`

## Intervalo keep-alive MQTT
{: #mqtt-keep-alive}

O intervalo keep-alive MQTT, que é medido em segundos, define o tempo máximo que pode passar sem comunicação entre o cliente e o broker. O cliente MQTT deve assegurar que, na ausência de qualquer outra comunicação com o broker, um pacote PINGREQ seja enviado. O intervalo keep-alive permite que tanto o cliente quanto o broker detectem que a rede falhou, resultando em uma conexão interrompida, sem precisar esperar que o período de tempo limite de TCP/IP seja atingido.

Se seus clientes MQTT {{site.data.keyword.iot_short_notm}} usarem assinaturas compartilhadas, o valor do intervalo keep-alive poderá ser configurado apenas entre 1 e 3600 segundos. Se um valor de 0 ou um valor maior que 3600 for solicitado, o broker {{site.data.keyword.iot_short_notm}} configurará o intervalo keep-alive para 3600 segundos.
