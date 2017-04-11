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



# Extension du service avec des API
{: #iot4i_extending_service}
{{site.data.keyword.iotinsurance_full}} fournit des API que vous pouvez utiliser pour personnaliser et étendre votre solution {{site.data.keyword.iotinsurance_short}}.
{:shortdesc}

{{site.data.keyword.iotinsurance_short}} est fourni avec une prise en charge intégrée des détecteurs de fuite d'eau Wink. Vous pouvez utiliser les API fournies pour personnaliser la solution {{site.data.keyword.iotinsurance_short}} afin de prendre en charge les nouveaux types et fournisseurs de terminal. {{site.data.keyword.iotinsurance_short}} repose sur la communication cloud-à-cloud pour obtenir des données de capteur des terminaux. En créant de nouveaux microservices de transformation, vous pouvez personnaliser{{site.data.keyword.iotinsurance_short}} afin que les données de capteur des nouveaux terminaux soient lues, puis transmises au reste du système via le service {{site.data.keyword.iot_short_notm}}, et que les actions appropriées soient exécutées.

Pour obtenir un jeu complet d'exemple de code, voir le [référentiel GitHub des exemples d'API ![Icône de lien externe](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){: new_window}.

Pour obtenir des informations complètes sur les API, voir la [documentation relative aux API ![Icône de lien externe](../../icons/launch-glyph.svg)](https://iot4i-api-docs.mybluemix.net/){: new_window}.
