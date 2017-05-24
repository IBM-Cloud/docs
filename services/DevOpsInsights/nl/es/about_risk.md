---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Acerca de Deployment Risk

{{site.data.keyword.DRA_short}} proporciona información diversa sobre los despliegues, especialmente su riesgo. Puede utilizarlo para automatizar la protección de la calidad en su conducto de entrega mediante el uso de políticas y puertas.  {:shortdesc}

Después de abrir {{site.data.keyword.DRA_short}} desde la cadena de herramientas, pulse **Deployment Risk**. Desde aquí, podrá obtener una visión general de las aplicaciones en los entornos de producción y transferencia y profundizar para comprender la cobertura de código, el rendimiento de las pruebas y los informes de seguridad. Los paneles de control se rellenan automáticamente con la información más reciente sobre las pruebas de {{site.data.keyword.DRA_short}} de sus conductos. 

Utilice Deployment Risk para imponer estándares de calidad en su cadena de herramientas mediante políticas y puertas. Las políticas comprenden conjuntos de reglas y las puertas que las imponen. Por ejemplo, podría crear una política denominada "Unit Testing and Test Coverage" que precisa que las compilaciones satisfagan estándares de realización de pruebas de unidad y estándares de cobertura de código. A continuación añadiría una puerta que haría referencia a la política de su proceso de entrega continua. Las compilaciones que no satisfagan la política se detendrán en la puerta.  

## Información de integración

Deployment Risk se integra con {{site.data.keyword.deliverypipeline}}, que es parte de {{site.data.keyword.contdelivery_full}}, y con proyectos de Jenkins. En un alto nivel, las instrucciones para utilizarlos son similares.  

Si está utilizando {{site.data.keyword.deliverypipeline}}, siga estos pasos:  

1. [Cree políticas y reglas](risk_policies.html) para que {{site.data.keyword.DRA_short}} las gestione.
2. [Prepare las etapas de su conducto](risk_cd.html) para la integración con {{site.data.keyword.DRA_short}}. 
3. [Cree o edite trabajos de pruebas](risk_cd.html) en el conducto para subir los resultados a {{site.data.keyword.DRA_short}}.
4. [Añada puertas](risk_cd.html) al conducto para que tomen decisiones de promoción en base a dichos resultados y a sus políticas. 
5. Ejecute el conducto y [visualice los resultados](results.html).

Si utiliza Jenkins, siga estos pasos: 

1. [Cree políticas y reglas](risk_policies.html) para que {{site.data.keyword.DRA_short}} las gestione.
2. [Instale y configure el plugin Jenkins](risk_jenkins.html).
3. [Cree trabajos de pruebas y puertas tal como se describe en las instrucciones del plugin](risk_jenkins.html). Las pruebas suben resultados para que {{site.data.keyword.DRA_short}} los analice y las puertas utilizan dichos resultados para tomar decisiones de promoción. 
4. Ejecute el proyecto y [visualice los resultados](results.html). 

Independientemente de cómo compila y despliega su código, los resultados serán los mismos: las compilaciones que satisfagan los estándares pasarán las puertas de Deployment Risk y las compilaciones que no lo hagan, serán detenidos.  

## Requisitos previos
{: #prerequisites}

Deployment Risk precisa una configuración adicional más allá de lo que se describe en [Iniciación con {{site.data.keyword.DRA_short}}](/docs/services/DevOpsInsights/index.html).

Para utilizar Deployment Risk, necesita dos cosas: 

* Una instancia de {{site.data.keyword.deliverypipeline}} o un proyecto de Jenkins 
* Pruebas que utilizará para evaluar su proyecto
