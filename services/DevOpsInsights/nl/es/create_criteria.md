---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-24"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Definición de políticas
{: #policies}

Las políticas controlan las puertas en un conducto de entrega continua. Si su código no satisface o excede una política instaurada en una puerta concreta, se detiene el despliegue para evitar que se liberen cambios con un riesgo elevado. {:shortdesc}

Las políticas se definen en {{site.data.keyword.DRA_short}}. Las políticas se crean en la organización (org) de {{site.data.keyword.Bluemix_notm}} que contiene {{site.data.keyword.DRA_short}}. Todas las aplicaciones que se encuentran en la misma organización puede utilizar la política.  

Para definir una política:

1. En la navegación izquierda, pulse **Valores**.

2. Pulse **Política**.

3. Pulse **Crear política** y, a continuación, especifique un nombre y una descripción para la nueva política.  

4. Pulse **Siguiente**.

4. Añada al menos una regla a la política:
  1. Pulse **Añadir regla a política**.
  2. Seleccione el tipo de regla.
  3. Especifique los detalles y las condiciones de la regla.
  4. Pulse **Guardar**.

5. Cuando haya acabado de añadir reglas a la política, pulse **Completado**.

## Creación de reglas
{: #criteria}

Las reglas definen los criterios que utilizarán las políticas para juzgar el cumplimiento o incumplimiento de la misma. Podría crear una política "Unit Testing and Test Coverage" que contenga una regla de prueba de unidad que requiera al menos un éxito del 80% de la misma y una regla de cobertura que precise el 100% de la cobertura de código. Si añade una puerta que haga referencia a esta regla en un conducto, la puerta impide que las compilaciones que no satisfacen ambas reglas continúen.  

Puede exigir una prueba satisfactoria sea como sea marcándola como crítica. Para crear una regla, seleccione una política y, a continuación, pulse **Añadir regla a política**.  

### Creación de reglas de prueba de verificación funcional
{: #criteria_fvt}

1. Escriba una descripción y seleccione un formato.

2. Especifique el porcentaje de casos de prueba que deben pasar correctamente para considerarse satisfactorio.

3. Defina los casos de prueba que sean críticos.

4. Para supervisar las regresiones de casos de prueba, marque el recuadro de selección **Supervisar la regresión de casos de prueba**.

5. Pulse **Guardar**.


### Creación de reglas de prueba de unidad
{: #criteria_ut}

1. Escriba una descripción y seleccione un formato.

2. Especifique el porcentaje de casos de prueba que deben pasar correctamente para considerarse satisfactorio.

3. Defina los casos de prueba que sean críticos.

4. Para supervisar las regresiones de casos de prueba, marque el recuadro de selección **Supervisar la regresión de casos de prueba**.

5. Pulse **Guardar**.


### Creación de reglas de cobertura de código
{: #criteria_codecoverage}

1. Escriba una descripción y seleccione un formato.

2. Especifique el porcentaje de cobertura de código que es necesario para considerarse satisfactorio.

3. Para supervisar las regresiones de cobertura de código, marque el recuadro de selección **Supervisar la regresión de casos de prueba**.

4. Pulse **Guardar**.

### Creación de reglas de exploración de seguridad estática
{: #criteria_static}

1. Especifique una descripción.

2. Especifique el número máximo de problemas de seguridad baja, media o elevada que esta regla permite.  

3. Pulse **Guardar**.

### Creación de reglas de exploración de seguridad dinámica
{: #criteria_dynamic}

1. Especifique una descripción.

2. Especifique el número máximo de problemas de seguridad baja, media o elevada que esta regla permite.  

3. Pulse **Guardar**.

## Herramientas y formatos de resultados de pruebas

{{site.data.keyword.DRA_short}} da soporte a estos tipos de métricas y formatos:

* Prueba de verificación funcional (Mocha, xUnit)
* Prueba de unidad (Mocha, xUnit, Karma/Mocha)
* Cobertura de código (Istanbul como formato de informe de resumen de JSON, Blanket.js)

{{site.data.keyword.DRA_short}} también da soporte a las pruebas de Selenium y Jasmine. Estas pruebas deben estar incluidas dentro de las herramientas soportadas oficialmente como, por ejemplo, xUnit y Mocha. Para obtener más información sobre el uso de {{site.data.keyword.deliverypipeline}}, {{site.data.keyword.DRA_short}} y Selenium conjuntamente, consulte [Running Selenium tests from the command line on a delivery pipeline](https://developer.ibm.com/devops-services/2016/07/21/running-selenium-tests-command-line-delivery-pipeline/). 

Para los elementos que tienen casos de prueba, puede especificar casos de prueba críticos, que son pruebas que deben pasar correctamente independientemente del porcentaje aceptable. Los nombres de los casos de prueba críticos deben coincidir con el atributo `full title` (título completo) del caso de prueba.     
* Para pruebas de Karma/Mocha, las series de descripción `describe()` e `it()` están enlazadas entre ellas con espacios. 
* Para pruebas de xUnit, el nombre de paquete, nombre de clase y nombre de función están enlazados entre ellos con espacios. Esto se muestra en el ejemplo siguiente:
  ```
  <testsuites package="test">
    <testsuite package="otc-api" name="PUT Service Instances - Test Setup" tests="2" failures="0" errors="0">
      <testcase name="#1 Authorization passed for mock user: idsb3t1@us.ibm.com"/>
      <testcase name="#2 Authorization passed for mock user: idsb3t4@us.ibm.com"/>
    </testsuite>
  </testsuite>
  ```
Este ejemplo genera estos nombres de casos de prueba:
  ```
  test otc-api PUT Service Instances - Test Setup #1 Authorization passed for mock user: idsb3t1@us.ibm.com
  test otc-api PUT Service Instances - Test Setup #2 Authorization passed for mock user: idsb3t1@us.ibm.com
  ```

Puede utilizar Sauce Labs con {{site.data.keyword.DRA_short}} añadiendo la integración de la herramienta Sauce Labs a su conducto. A continuación, incorpore las variables de entorno `SAUCE_USERNAME` y `SAUCE_ACCESS_KEY` en las pruebas de Selenium como credenciales.

Puede ver los títulos completos de todas las pruebas en los registros tras una ejecución.  

**Notas:**
* {{site.data.keyword.DRA_short}} no da soporte a las pruebas críticas que contienen un guión en el título completo.    
* Si cambia el nombre de su organización, debe recrear las políticas que estaban asociadas al nombre anterior. Perderá el acceso a los informes de decisión que se generaron antes del cambio de nombre.

## Visualización de informes de decisión    
{: #DI_decision_reports}

Tras ejecutarse un conducto, {{site.data.keyword.DRA_short}} empieza a recopilar y analizar los resultados de las pruebas para establecer una línea base. Los datos de cada ejecución posterior se recopila y se compara con los resultados anteriores. Las puertas de decisión utilizan estos datos para determinar cuándo se debe detener un despliegue. 

Para ver el informe de decisión de una puerta del conducto, siga estos pasos:

   1. En la etapa que contiene la puerta que se debe comprobar, pulse **Ver registros e historial**.

   2. Desde el trabajo que contiene la puerta, pulse el nombre de la puerta. 

   3. En la ventana de registros, busque el mensaje `Comprobar aquí informe de {{site.data.keyword.DRA_short}}` y pulse el enlace para abrir el informe. 
