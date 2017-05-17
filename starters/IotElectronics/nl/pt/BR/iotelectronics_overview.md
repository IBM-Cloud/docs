---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-06"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Sobre o {{site.data.keyword.iotelectronics}}
{: #iotelectronics_about}

{{site.data.keyword.iotelectronics_full}} é uma instância de produção IoT totalmente integrada que permite que os aplicativos
se comuniquem e consumam dados coletados por seus dispositivos, sensores e gateways conectados.
{:shortdesc}

O {{site.data.keyword.iotelectronics}} usa o serviço do {{site.data.keyword.iot_full}} para conectar os seus dispositivos eletrônicos inteligentes com os aplicativos que você desenvolver. Ele
também usa o {{site.data.keyword.iot_short_notm}} para ajudar a analisar e entender os dados dos seus dispositivos. É possível estabelecer
regras para identificar condições que precisem de atenção e definam respostas automatizadas, como enviar e-mail, executar um fluxo de trabalho Node-RED ou conectar a serviços da web.

## Localizando o iniciador
{: #iot4eFindingStarter}
É possível localizar o iniciador {{site.data.keyword.iotelectronics}}
na [Seção Modelos](https://console.{DomainName}/catalog/starters/iot-for-electronics-starter/)
do catálogo {{site.data.keyword.Bluemix_notm}}.

## O que é Possível Executar com o {{site.data.keyword.iotelectronics}}
{: #Features_iote}
Explore rapidamente os recursos da solução {{site.data.keyword.iotelectronics}} usando dispositivos e dados simulados.

### Conectar dispositivos simulados
Crie dispositivos simulados e conecte-os à plataforma para ver os dados em transmissão em tempo real. Use um aplicativo baseado na web para
simular como um dispositivo recebe comandos e executa operações. Simule falhas para gerar avisos e alertas. Para fins de demonstração, as arruelas são usadas como o dispositivo simulado dentro do iniciador do {{site.data.keyword.iotelectronics}}. O dispositivo
que você optar por conectar poderia ser qualquer tipo de dispositivo eletrônico inteligente.

### Tentar um aplicativo móvel do consumidor de amostra
Use seu dispositivo móvel iOS ou Android para ver como um proprietário de dispositivo pode interagir com o dispositivo. Envie comandos para o dispositivo e
receba atualizações do dispositivo usando a plataforma e {{site.data.keyword.Bluemix_notm}}. Simule eventos de falha e visualize os
resultados no aplicativo móvel.

### Conecte os seus próprios dispositivos eletrônicos
Conecte os seus próprios dispositivos com segurança à nuvem e comece a customizar os seus próprios aplicativos. Um conjunto de exemplos e
orientações verificados está disponível e pode ser modificado e usado para provas de conceito, teste e experimentação.

## O que há no iniciador {{site.data.keyword.iotelectronics}}
{: #whatsInStarter}
O modelo do iniciador implementa a solução integrada do {{site.data.keyword.iotelectronics}}.  Todos os componentes são ligados e implementados automaticamente para você. O aplicativo do iniciador permite explorar rapidamente os recursos da
solução usando dispositivos e dados simulados. O aplicativo móvel de amostra mostra como um consumidor pode registrar, receber alertas e controlar
um dispositivo conectado. É possível usar as amostras como pontos de início para criar seus próprios aplicativos e coletar dados de seus próprios
dispositivos. Os serviços e aplicativos a seguir são incluídos na solução:

![Arquitetura do {{site.data.keyword.iotelectronics}}. Este diagrama é descrito no corpo
principal do tópico.](images/IoT4E_architecture.svg "{{site.data.keyword.iotelectronics}} architecture")

O iniciador do {{site.data.keyword.iotelectronics}} usa o serviço e APIs do {{site.data.keyword.iotelectronics}} para se conectar com o {{site.data.keyword.iot_short_notm}}. O aplicativo iniciador e o aplicativo móvel de amostra se comunicam com o serviço {{site.data.keyword.iotelectronics}}. Os
componentes a seguir estão incluídos no iniciador:

O serviço do **{{site.data.keyword.iotelectronics}}** suporta registro e notificações de usuário e de dispositivo.

O **{{site.data.keyword.iot_full}}** permite que os seus aplicativos se comuniquem com e usem dados que são coletados por seus dispositivos, sensores e gateways
conectados.

**{{site.data.keyword.sdk4nodefull}}** permite desenvolver, implementar e ajustar a escala de aplicativos
JavaScript&reg; do lado do servidor e fornece desempenho, segurança e capacidade de manutenção aprimorados.

O **{{site.data.keyword.appid_full}}** inclui a autenticação para o seu dispositivo móvel e apps da web e protege os seus sistemas de backend.

O **App móvel de amostra** permite visualizar o status e se comunicar com um dispositivo simulado usando seu dispositivo móvel, como um telefone inteligente ou tablet. Descubra como conseguir o aplicativo móvel em
[Usando o aplicativo móvel](iotelectronics_config_mobile.html).
