---



copyright:

  years: 2015, 2017
lastupdated: "2017-04-12"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Cómo se le carga
{: #charges}

Los cargos varían en función de los recursos utilizados por un servicio concreto, el tiempo de ejecución, el contenedor o la opción de soporte. Los recursos pueden ser el número de llamadas de API, el número de instancias,
memoria, almacenamiento, etc. {{site.data.keyword.Bluemix_notm}} también proporciona estimadores de coste detallado, y una calculadora de coste hasta el último céntimo para ayudarle a planificar los cargos. Puede comprobar el coste real después de crear sus apps en la página del Panel de control de uso. 

Con una cuenta facturable de {{site.data.keyword.Bluemix_notm}}, se le facturará por el cálculo, los contenedores y los servicios que se utilicen en su organización. Es posible que otros usuarios de {{site.data.keyword.Bluemix_notm}} le inviten a participar en organizaciones en una cuenta diferente. Si crea apps o utiliza servicios en las organizaciones las que está invitado, el uso que se produce se factura a la cuenta que contenga dichas organizaciones. Puede ver más información sobre unos cargos específicos en una página de detalles de recurso en el Catálogo de {{site.data.keyword.Bluemix_notm}}, o en la calculadora de precios en la página {{site.data.keyword.Bluemix_notm}} Precios.

Se aplicarán distintos tipos de cargos en función de las características de {{site.data.keyword.Bluemix_notm}} que utilice. En la tabla siguiente se proporciona una visión general de alto nivel:

| Tipo de cargo | Descripción | Características de {{site.data.keyword.Bluemix_notm}} que utilizan este tipo de cargo | Ejemplo |
|------------------|------------------|--------------------------|--------------------------|
| Corregido | El precio de tasa fija se basa en un acuerdo sobre el cargo mensual que no está ajustado. | Servicios  | La memoria caché de datos tiene un plan fijo que se cargará en una tasa mensual fija. |
| Medido | El precio de uso medido se basa en el número de GB hora consumidos para los entornos de ejecución, y en el número de GB hora consumidos y en el número de direcciones IP y el almacenamiento para contenedores. | Servicios, cálculo y contenedores | Para el servicio Push, cualquier uso que supere la concesión mensual gratuita se factura. |
|  Por niveles   |  Algunos planes también están basados en un modelo de precios por niveles, para poder acceder a descuentos por volumen, según su uso actual. Los servicios pueden ofrecer planes de precios de capas de bloques, graduados y simples. | Servicios | El precio escalonado se utiliza normalmente para medidas de carga que tienen previsto tener cantidades muy altas por mes, tales como llamadas a la API. |
| Reservado | El precio reservado se basa en un compromiso a largo plazo para un servicio, por lo que puede obtener un precio de descuento. Con un plan reservado, obtendrá una instancia de servicio dedicada que es fácil de configurar, desplegar y entregar en el entorno {{site.data.keyword.Bluemix_notm}} público. | Servicios | DB2 on Cloud tiene planes reservados.|

## Cargos por recursos de cálculo
{: #compute}

Se le facturará por el tiempo que las apps se ejecuten y la memoria que se utilice, calculados como *GB por hora*. GB por hora es el cálculo del número de instancias de la app, multiplicado por la memoria por instancia, multiplicado por las horas que se ejecutaron las instancias. Puede personalizar el número de instancias y la cantidad de memoria por instancia según sus necesidades. Posteriormente puede añadir memoria o instancias para escalar a más usuarios. La carga final es por GB por hora: las instancias de app, multiplicado por memoria por instancia, multiplicado por horas de ejecución.

Por ejemplo, supongamos que tenemos un tiempo de ejecución que cuesta 0,07 dólares por GB por hora en dos instancias de 512 MB que se ejecutan durante 30 días (720 horas). Estos recursos costarían unos 24,15 dólares, incluida la concesión gratuita de 375 GB por hora, según el siguiente cálculo:

```
2 instancias x 0,5 GB x 720 horas = 720 GB hora.
(720 - 375) GB por hora x 0,07 dólares por GB por hora = 24,15 dólares
```

## Cargos por servicios
{: #services}

Muchos servicios incluyen concesiones gratuitas mensuales. El uso de servicios que no está incluido como parte de la concesión gratuita se factura de una de las maneras siguientes:
<dl>
<dt>Cargos fijos</dt>
    <dd>Selecciona un plan y paga en función de una tarifa plana. Por ejemplo, el servicio de memoria caché de datos se cargará a una tarifa plana.</dd>
<dt>Cargos con medición</dt>
    <dd>Paga en función del consumo de tiempo de ejecución y de servicio. Por ejemplo, con el servicio Push, cualquier uso que supere la concesión mensual gratuita se factura.</dd>
<dt>Cargos reservados</dt>
    <dd><p>Como propietario de la cuenta de una cuenta de Pago según uso o una cuenta de Suscripción, puede reservar una instancia de servicio, con un compromiso a largo plazo, para obtener un precio con descuento. Por ejemplo, puede reservar la oferta de DB2 on Cloud grande estándar para 12 meses.</p>
    <p>Algunos servicios de {{site.data.keyword.Bluemix_notm}} ofrecen planes reservados. Puede solicitar un plan reservado desde el {{site.data.keyword.Bluemix_notm}} <strong>Catálogo</strong> pulsando el mosaico del servicio. A continuación, seleccione el plan de servicio que se ajuste mejor a sus necesidades. Si hay disponible un plan reservado, pulse <strong>Solicitud</strong>, y siga las instrucciones para enviar la solicitud. Recibirá un correo electrónico que contiene la información del precio del plan reservado. Un representante de ventas de {{site.data.keyword.Bluemix_notm}} también se pondrá en contacto con usted pronto para finalizar la compra.</p></dd>
<dt>Cargos escalonados</dt>
    <dd>De forma similar a los cargos con medición, pagará en función del consumo de servicios y de tiempo de ejecución. Sin embargo, los cargos por capas añaden capas de precios adicionales, ofreciendo a menudo cargos descontados en capas con un consumo más grande. El precio por niveles se ofrece de forma simple, graduada o de bloque.</dd>
</dl>

### Nivel sencillo
{: #simple_tier}

En el modelo de nivel sencillo, el precio unitario se determina
mediante el nivel al que corresponde la cantidad que utilice. El precio
total es su cantidad multiplicado por el precio unitario de dicho nivel. Por ejemplo:

| Cantidad de elementos | Precio unitario para todos los elementos |
|-------------------|--------------------------|
| Nivel 1: 1 - 1000  | $1 USD                   |
| Nivel 2: 1001 - 2000    |    $0,90 USD                      |
| Nivel 3: 2001 - 3000                  |   $0,75 USD                       |
| Nivel 4: 3001 - 4000           |      $0,60 USD                    |
|Nivel 5: &gt; 4000 | $0,40 USD |
{:caption="Tabla 1. Tabla de preciso de nivel sencillo" caption-side="top"}

En la tabla siguiente se muestra lo que
se pagaría con un plan basado en un modelo de precios de nivel sencillo:

| Cantidad de elementos | Cálculo del cargo | Precio total |
|-------------------|--------------------|-------------|
|500 |	500 × 1 = 500 |	$500 USD|
|1500 |	1500 × 0,90 = 1350 |	$1350 USD|
|2500 |	2500 × 0,75 = 1875 |	$1875 USD|
|... |	... |	...|
|5200 |	5200 × 0,40 = 2080 |$2080 USD|
{:caption="Tabla 2. Cálculo de cargos usando el modelo de precios del nivel sencillo" caption-side="top"}

### Nivel graduado
{: #graduated_tier}

En el modelo de nivel graduado, el precio de unidad por nivel disminuye
según aumenta su nivel de uso. El precio total son los cargos acumulados para
cada nivel de uso, y consta de su cantidad multiplicado por el precio unitario
de dicho nivel. Por ejemplo:

| Cantidad de elementos |	Precio unitario para los elementos en el nivel|
|-------------------|------------------------------------|
|    Nivel 1: 1 - 1000 |	$1 USD |
|   Nivel 2: 1001 - 2000 |	$0,90 USD |
|    Nivel 3: 2001 - 3000 |	$0,75 USD |
|    Nivel 4: 3001 - 4000 |	$0,60 USD |
|    Nivel 5: &gt; 4000 |	$0,40 USD |
{:caption="Tabla 3. Tabla de precios del nivel graduado" caption-side="top"}

En la tabla siguiente se muestra lo que
se pagaría con un plan basado en un modelo de precios de nivel graduado:

|Cantidad de elementos | Cálculo del cargo | Precio total|
|------------------|--------------------|------------|
|500 |	500 × 1 (precio unitario para Nivel 1) = 500 |	$500 USD|
|1500 |	(1000 × 1 (precio unitario para Nivel 1)) + (500 × 0,90 (precio unitario para Nivel 2)) = 1450 |	$1450 USD|
|2500 |	(1000 × 1 (precio unitario para Nivel 1)) + (1000 × 0,90 (precio unitario para Nivel 2)) + (500 × 0,75 (precio unitario para Nivel 3)) = 2275 |	$2275 USD |
|... |	... |	...|
|5200 |	(1000 × 1 (precio unitario para Nivel 1)) + (1000 × 0,90 (precio unitario para Nivel 2)) + (1000 × 0,75 (precio unitario para Nivel 3)) + (1000 × 0,60 (precio unitario para Nivel 4)) + (1200 × 0,40 (precio unitario para Nivel 5)) = 3730 |	$3730 USD|
{:caption="Tabla 4. Cálculo de cargos usando el modelo de precios del nivel graduado" caption-side="top"}

### Nivel Bloque
{: #block_tier}

En el modelo de nivel por bloque, el precio es un cargo establecido
para la cantidad que utilicen dentro de un nivel de uso. El precio total
es el cargo de su nivel de uso, independientemente del uso real. Cada nivel
sucesivo proporciona una tasa menor entre precio y cantidad. Por ejemplo:

|Cantidad de elementos |	Precio total para todos los elementos|
|------------------|-----------------------------|
| Nivel 1: &lt;= 1000 |	$1000 USD|
| Nivel 2: &lt;= 2000 |	$1900 USD|
| Nivel 3: &lt;= 3000 |	$2800 USD|
| Nivel 4: &lt;= 4000 |	$3500 USD|
| Nivel 5: &lt;= 10000 |	$5000 USD|
{:caption="Tabla 5. Tabla de precios del nivel por bloques" caption-side="top"}

En la tabla siguiente se muestra lo que
se pagaría con un plan basado en un modelo de precios de nivel por bloque:

|Cantidad de elementos |	Cálculo del cargo |	Precio total|
|------------------|-----------------------|---------------|
|500 |	El número de elementos cae en el Nivel 1, por lo que el precio total es $1000 USD. |	$1000 USD|
|1500 |	El número de elementos cae en el Nivel 2, por lo que el precio total es $1900 USD. |	$1900 USD|
|... |	... |	...|
|5200 |	El número de elementos cae en el Nivel 5, por lo que el precio total es $5000 USD. |	$5000 USD|
{:caption="Tabla 6. Cálculo de cargos usando el modelo de precios del nivel por bloque" caption-side="top"}
