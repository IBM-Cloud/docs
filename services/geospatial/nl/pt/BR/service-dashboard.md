---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#Painel de administração de serviços
{: #service-dashboard}


É possível ver o status de sua instância de serviço do {{site.data.keyword.geospatialshort_Geospatial}} e parar ou reiniciá-la
a partir do painel de administração de serviços. É possível obter o painel de administração de serviços clicando na tela
do {{site.data.keyword.geospatialshort_Geospatial}} no painel do {{site.data.keyword.geospatialshort_Geospatial}}. Se você estiver usando
o aplicativo de amostra e sua instância de serviço atingir o limite de eventos e for interrompida, será possível reiniciar o
serviço. Parar o serviço remove o limite de eventos. Ele continua a receber eventos até que você pare o serviço. O painel de administração de serviços exibe também o status de sua instância de serviço e
as estatísticas.
{:shortdesc}

##Verificações de
região
do {{site.data.keyword.geospatialshort_Geospatial}}

O
{{site.data.keyword.geospatialshort_Geospatial}}
monitora os dispositivos em movimentação da Internet das Coisas. Cada
dispositivo monitorado envia mensagens do dispositivo que contém um
identificador exclusivo junto com sua posição atual, abrangendo
latitude e longitude. A posição do dispositivo é verificada com
relação às coordenadas de cada região geográfica definida. O serviço produz eventos quando os dispositivos entram, saem ou estão "em hangout" em uma região específica.

Uma Verificação de região é usada como uma unidade para medir o uso do {{site.data.keyword.geospatialfull}}. Para
cada mensagem do dispositivo, uma verificação de região é realizada
se entrada, saída ou detecção de ambos for especificada para a
região. Para cada mensagem do dispositivo, uma verificação de região
é realizada, se a detecção de hangout foi especificada para a
região. Se nenhuma região for definida, para cada mensagem do dispositivo,
uma verificação de região é contada como se fosse uma região. Isso significa que se você tivesse 100 regiões com a verificação, a entrada, a saída e o hangout definidos, uma única mensagem do
dispositivo produziria 200 verificações de região.
