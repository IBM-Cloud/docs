---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-08"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}



# Estendendo o serviço com APIs
{: #iot4i_extending_service}
O {{site.data.keyword.iotinsurance_full}} fornece APIs para customizar e estender sua solução {{site.data.keyword.iotinsurance_short}}.
{:shortdesc}

O {{site.data.keyword.iotinsurance_short}} vem com suporte integrado para sensores de vazamento de água Wink. Usando as APIs fornecidas, é possível customizar a solução {{site.data.keyword.iotinsurance_short}} para suportar novos tipos de dispositivo fornecedores. O {{site.data.keyword.iotinsurance_short}} depende da comunicação de nuvem para
nuvem para obter dados do sensor dos dispositivos. Ao criar novos microsserviços de
transformação, é possível customizar o {{site.data.keyword.iotinsurance_short}}
para ler os dados do sensor dos novos dispositivos, passá-los ao restante do sistema por
meio do serviço do {{site.data.keyword.iot_short_notm}} e, em seguida, tomar
ações conforme apropriado.

Para obter um conjunto completo do código de exemplo, veja o [repositório
GitHub de exemplos de API ![Ícone de link externo](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){: new_window}.

Para obter informações completas sobre as APIs, veja a [documentação da API ![Ícone de link externo](../../icons/launch-glyph.svg)](https://iot4i-api-docs.mybluemix.net/){: new_window}.
