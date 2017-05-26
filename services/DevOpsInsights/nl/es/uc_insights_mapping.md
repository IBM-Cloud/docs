---

copyright:
  years: 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Correlación de entornos para informes
{: #uc_insights_mapping}

La información que ve en Delivery Insights se agrupa mediante *entornos lógicos*, que son conjuntos de entornos de IBM UrbanCode Deploy (y que también se denominan *entornos físicos*). Puede agrupar sus entornos en entornos lógicos de la forma que desee para que tenga sentido para su organización.
{:shortdesc}

## Entornos lógicos

Delivery Insights agrupa sus entornos IBM UrbanCode Deploy en uno o varios entornos lógicos. De este modo, puede recopilar entornos en grupos que tengan un significado para organización. Por ejemplo, si tiene varios entornos de producción de varias aplicaciones, puede agrupar todos esos entornos en un único entorno lógico y combinar las métricas de todos de esos entornos en un único panel de control del entorno de producción. La correlación se crea mediante una serie de búsqueda, que permite agrupar entornos de la forma que tenga sentido para sus servidores IBM UrbanCode Deploy. 

## Entornos lógicos predeterminados

De forma predeterminada, los informes incluyen entornos lógicos que coinciden con series de texto de los entornos de IBM UrbanCode Deploy. Por ejemplo, todos los entornos con "dev" en el nombre se correlacionan con el entorno lógico DEV, y todos los entornos con "prod" en el nombre se correlacionan con el entorno lógico PROD. 

![Los entornos lógicos predeterminados](images/uc_insights_mapping.gif)

## Correlación de entornos con entornos lógicos

Puede correlacionar de forma manual entornos físicos con entornos lógicos o puede utilizar patrones para asociar entornos físicos con entornos lógicos de forma dinámica. 

Para correlacionar entornos físicos con entornos lógicos mediante un patrón, siga estos pasos:

1. En {{site.data.keyword.DRA_short}}, pulse **Delivery Insights > Correlacionar entornos**.
1. Pulse un entorno lógico existente o pulse **Añadir entorno lógico**.
1. En los valores para el entorno lógico, bajo **Patrones**, pulse **Añadir patrón**.
1. Especifique un patrón para los nombres de entorno. Puede utilizar el asterisco (*) como comodín. Por ejemplo, el patrón `env` coincide con los entornos `env1`, `env2` y `env`.
1. Verifique que el entorno lógico contiene los entornos que desee.

Para correlacionar entornos con entornos lógicos de forma manual, pulse **Añadir manualmente** y seleccione los entornos a añadir o eliminar.

![Configuración de la integración en DevOps Connect](images/uc_insights_mapping_manually.gif)

Ahora que ha correlacionado entornos con entornos lógicos, puede ver la información de los informes agregada por dichos entornos lógicos.
