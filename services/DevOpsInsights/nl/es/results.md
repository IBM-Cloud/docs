---

copyright:
  years: 2016, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Visualización de resultados

## Evaluaciones de Deployment Risk

Tras ejecutarse un conducto, {{site.data.keyword.DRA_short}} empieza a recopilar y analizar los resultados de las pruebas para establecer una línea base. Los datos de cada ejecución posterior se recopila y se compara con los resultados anteriores. Las puertas de decisión utilizan estos datos para determinar cuándo se debe detener un despliegue. 

Puede ver los datos de evaluación de despliegue y de puertas desde el panel de control de Deployment Risk. Para abrir el panel de control, abra {{site.data.keyword.DRA_short}} y en el menú lateral, pulse **Deployment Risk**.

Si está utilizando un conducto de {{site.data.keyword.contdelivery_short}}, puede ver informes individuales de ejecución de las puertas desde el propio conducto. Para ver el informe de decisión de una puerta del conducto, siga estos pasos:

1. En la etapa que contiene la puerta que se debe comprobar, pulse **Ver registros e historial**.

2. Desde el trabajo que contiene la puerta, pulse el nombre de la puerta.

3. En la ventana de registros, busque el mensaje `Comprobar aquí informe de {{site.data.keyword.DRA_short}}` y pulse el enlace para abrir el informe.

## Informes de Developer Insights y Team Dynamics

Puede ver paneles de control sobre su código y equipo después de un periodo inicial de minería de datos. En el menú de navegación del servicio, pulse **Developer Insights** o **Team Dynamics** y, a continuación, seleccione una categoría de datos para ver esta información.
