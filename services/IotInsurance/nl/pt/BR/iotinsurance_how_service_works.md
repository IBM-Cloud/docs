---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-07"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}



# Como o serviço funciona
O {{site.data.keyword.iotinsurance_full}} cria um fluxo para coletar, gerenciar e analisar dados dos segurados conectados.
{:shortdesc}

O provedor de seguro cria uma instância do
{{site.data.keyword.iotinsurance_short}} dentro da organização do
{{site.data.keyword.Bluemix_notm}}. Os clientes do segurador têm sensores em
suas casas, que são conectados à nuvem do provedor do sensor. A partir de seus
dispositivos móveis, os clientes autorizam o serviço do
{{site.data.keyword.iotinsurance_short}} a receber dados do sensor. O {{site.data.keyword.iotinsurance_short}} Transformer se conecta à nuvem do provedor do sensor e puxa os dados de cada usuário e os envia ao servidor {{site.data.keyword.iot_short_notm}}. Se o sensor mostrar que os parâmetros especificados nas proteções do segurador são atendidos na casa do cliente, notificações são enviadas para o painel do segurador e para o dispositivo do cliente.

Um sensor conectado detecta um evento, como um vazamento de água, e envia essas
informações para um fornecedor de casa inteligente, como o Wink.  O
{{site.data.keyword.iotinsurance_short}} detecta o sinal usando sua conexão com a
nuvem do fornecedor de casa inteligente e cria uma carga útil de alerta. A carga útil é
enviada por meio do MQTT para o mecanismo de blindagem do
{{site.data.keyword.iotinsurance_short}} para processamento. O mecanismo de
proteção analisa se a carga útil corresponde aos critérios que são definidos pelas regras
de blindagem. Se a resposta for sim, o mecanismo de blindagem emitirá uma carga útil de
risco por meio do MQTT para o mecanismo de ação do
{{site.data.keyword.iotinsurance_short}}. O mecanismo de ação executa as ações
definidas pela blindagem para esse tipo de risco, por exemplo, enviar uma mensagem de
texto para o proprietário.

O {{site.data.keyword.iotinsurance_short}} depende do {{site.data.keyword.iot_full}} para passar cargas úteis de alerta e risco entre seus componentes. Um sistema de trabalho completo requer usuários, blindagens e associações entre usuários e blindagens.

![Processo do {{site.data.keyword.iotinsurance_short}}. Este diagrama é descrito no corpo principal do tópico.](images/IoT4I_process.svg "{{site.data.keyword.iotinsurance_short}} process")
