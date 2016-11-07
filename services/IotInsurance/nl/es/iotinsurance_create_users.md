---

copyright:
  years: 2016

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# Creación de asociaciones de usuarios y coberturas
{: #gettingstartedtemplate}
Última actualización: 15 de septiembre de 2016
{: .last-updated}

Después de crear el servicio {{site.data.keyword.iotinsurance_short}} y desplegar los servicios y apps de soporte necesarios, puede probar el servicio creando un usuario autorizado y una asociación de coberturas.
{:shortdesc}

**Requisitos previos:** Antes de comenzar, asegúrese de que se cumplan los siguientes requisitos previos:

- [Node.js](https://nodejs.org/en/) instalado en su sistema.  
- Un entorno de ejecución habilitado para Node.js como Eclipse.
- Software Git y acceso al [repositorio de código fuente de GitHub para los ejemplos de API](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs).   También puede descargar el [archivo con los archivos del código fuente](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/archive/master.zip).
- Código fuente preparado.  
  Para preparar el código fuente, realice estos pasos:
  1. Clone o descargue el [repositorio de código fuente de GitHub](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs) a su sistema.
  2. Instale los requisitos previos de fuente abierta del proyecto utilizando una indicación de mandatos para ir a la carpeta que contiene los archivos de código fuente clonados, y ejecutando el mandato `npm install`.

Cree un usuario que pueda utilizar para probar las características del panel de control y la app para móvil de ejemplo.

1. Cree un usuario en el sistema {{site.data.keyword.iotinsurance_short}}.
  1. Edite el archivo createUser.js para sustituir los valores en la variable **user** con información exclusiva del usuario.
  2. Guarde el archivo.
  3. Ejecute `node createUser.js`. El proceso tarda unos momentos en completarse.
  4. Tome nota del nombre de usuario. Es necesario en el siguiente paso.
2. Cree una asociación de coberturas para el usuario.
  1. Edite el archivo createUserShieldAssociation.js para añadir el nombre de usuario del paso anterior en la variable **username**.
  2. Guarde el archivo.
  3. Ejecute `node createUserShieldAssociation.js`. Para obtener más información sobre las coberturas, consulte [Componentes](iotinsurance_overview.html#components).
3. (opcional) El motor de analíticas se actualiza automáticamente. Sin embargo, si no se muestran los datos correctos, puede actualizar el motor de analíticas ejecutando `node updateAnalyticsEngine.js`.
4. (opcional) Simule un suceso de riesgo para el usuario.
  1. Edite el archivo simulateHazard.js para añadir el nombre de usuario de los pasos anteriores en la variable **usr**.
  2. Guarde el archivo.
  3. Ejecute `node simulateHazard.js`.
5. (opcional) Cree un conjunto de datos históricos simulados ejecutando `node createHistoricalData.js`.


# Enlaces relacionados
{: #rellinks}

## Referencia de API
{: #api}
* [Ejemplos de API de {{site.data.keyword.iotinsurance_short}}](https://iot4i-docs-api.mybluemix.net/dist/){:new_window}

## Enlaces relacionados
{: #general}
* [Foro de soporte para desarrolladores](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
* [Foro de soporte de Stack Overflow](http://stackoverflow.com/questions/tagged/ibm-bluemix)
