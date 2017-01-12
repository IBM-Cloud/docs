---

copyright:
  years: 2016
lastupdated: "2016-11-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Definición de políticas
{: #criteria}

Con {{site.data.keyword.DRA_short}}, es fácil definir las políticas para su aplicación. Para comenzar, realice estos pasos:
{:shortdesc}

1. En el menú lateral, pulse **Política**.

2. Pulse **Crear política (+)** y especifique un nombre y una descripción para la nueva política.

3. Pulse **Siguiente**.

4. Añada al menos una regla a la política:
  1. Pulse **Crear regla (+)**.
  2. Seleccione el tipo de regla.
  3. Especifique los detalles y las condiciones de la regla.
  4. Pulse **Guardar**.

5. Cuando haya acabado de añadir reglas a la política, pulse **Completado**.

Las políticas se crean en la organización de {{site.data.keyword.Bluemix_notm}} en que se ha añadido {{site.data.keyword.DRA_short}}. Cualquier aplicación que esté en la misma organización puede utilizar la política.

{{site.data.keyword.DRA_short}} da soporte a estos tipos de métricas y formatos:

* Prueba de verificación funcional (Mocha, JUnit)
* Prueba de unidad (Mocha, JUnit, Karma/Mocha)
* Cobertura de código (Istanbul como formato de informe de resumen de JSON, Blanket.js)

{{site.data.keyword.DRA_short}} también da soporte a las pruebas de Selenium y Jasmine. Estas pruebas deben estar incluidas dentro de las herramientas soportadas oficialmente, como JUnit, xUnit y Mocha. Para obtener más información sobre el uso de {{site.data.keyword.deliverypipeline}}, {{site.data.keyword.DRA_short}} y Selenium conjuntamente, consulte [Running Selenium tests from the command line on a delivery pipeline](https://developer.ibm.com/devops-services/2016/07/21/running-selenium-tests-command-line-delivery-pipeline/).

Para los elementos que tienen casos de prueba, puede especificar casos de prueba críticos, que son pruebas que deben pasar correctamente independientemente del porcentaje aceptable. Los nombres de los casos de prueba críticos deben coincidir con el atributo `full title` (título completo) del caso de prueba:    
* Para pruebas de Karma/Mocha, las series de descripción `describe()` e `it()` están enlazadas entre ellas con espacios
* Para pruebas de JUnit, el nombre de paquete, nombre de clase y nombre de función están enlazados entre ellos con espacios    

Puede utilizar Sauce Labs con {{site.data.keyword.DRA_short}} añadiendo la integración de Sauce Labs a su conducto. A continuación, incorpore las variables de entorno `SAUCE_USERNAME` y `SAUCE_ACCESS_KEY` en las pruebas de Selenium como credenciales.

Puede ver los títulos completos de todas las pruebas en los registros tras una ejecución.  

Notas:
* {{site.data.keyword.DRA_short}} no da soporte a las pruebas críticas que contienen un guión en el título completo.    
* Si cambia el nombre de su organización, debe recrear las políticas que estaban asociadas al nombre anterior. Perderá el acceso a los informes de decisión que se generaron antes del cambio de nombre.

## Creación de reglas de prueba de verificación funcional
{: #criteria_fvt}

1. Escriba una descripción y seleccione un formato.

2. Especifique el porcentaje de casos de prueba que deben pasar correctamente para considerarse satisfactorio.

3. Defina los casos de prueba que sean críticos.

4. Para supervisar las regresiones de casos de prueba, marque el recuadro de selección **Supervisar la regresión de casos de prueba**.

5. Pulse **Guardar**.


## Creación de reglas de prueba de unidad
{: #criteria_ut}

1. Escriba una descripción y seleccione un formato.

2. Especifique el porcentaje de casos de prueba que deben pasar correctamente para considerarse satisfactorio.

3. Defina los casos de prueba que sean críticos.

4. Para supervisar las regresiones de casos de prueba, marque el recuadro de selección **Supervisar la regresión de casos de prueba**.

5. Pulse **Guardar**.


## Creación de reglas de cobertura de código
{: #criteria_codecoverage}

1. Escriba una descripción y seleccione un formato.

2. Especifique el porcentaje de cobertura de código que es necesario para considerarse satisfactorio.

3. Para supervisar las regresiones de cobertura de código, marque el recuadro de selección **Supervisar la regresión de casos de prueba**.

4. Pulse **Guardar**.
