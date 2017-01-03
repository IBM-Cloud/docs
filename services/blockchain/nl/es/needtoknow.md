---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Información que necesita saber
{: #etn_overview}
Última actualización: 10 de noviembre de 2016
{: .last-updated}

**ATENCIÓN:** Debe revisar la siguiente información antes de utilizar un plan de IBM Blockchain en Bluemix: Desarrollador inicial (Beta) o Red empresarial de alta seguridad (GA).
<br><br>

## Sentencia de soporte de IBM

IBM tiene una larga historia de liderazgo en innovación, que continúa con las ofertas más recientes de IBM Blockchain. Blockchain es una tecnología de progreso rápido proyectada para interrumpir varios sectores, desde finanzas hasta logística. Mediante varios programas de adopción anteriores, los clientes y los socios empresariales de IBM ya están influyendo en la dirección futura de blockchain. IBM Blockchain on Bluemix es uno de tales programas. **Igual que con cualquier nueva tecnología, los usuarios de IBM Blockchain on Bluemix deben estar preparados para cambios rápidos y fundamentales**.  
{:shortdesc}

La arquitectura que hay detrás de IBM Blockchain es el Hyperledger Project de Linux Foundation. Hyperledger Fabric es un proyecto de código abierto bajo el desarrollo activo, actualmente en el estado *Incubación*. Cada contribución a la comunidad de código abierto hace a Hyperledger Fabric más sólido, pero puede presentar solicitudes de adopción. Durante el ciclo de *Incubación*, los clientes pueden utilizar Hyperledger Fabric v0.6 para la prueba y la simulación de red, pero **IBM le advierte frente a la ejecución de activos financieros de valor directamente en una red blockchain de Hyperledger Fabric v0.6 (o anterior)**.  
<br>

## Sentencia de código abierto

IBM Blockchain on Bluemix&mdash;tanto el plan Desarrollador inicial como el plan Red empresarial de alta seguridad&mdash;utilizan el código abierto de Hyperledger Fabric v0.6.1 de Linux Foundation. Los miembros de Hyperledger Project, incluido IBM, aportan código al entramado, después de que es revisado, evaluado y probado por la comunidad. Hyperledger Fabric v0.6.1 está en este momento en el estado *Incubación*; los detalles sobre el estado de *Incubación*, y de todo el ciclo de vida de Hyperledger Project, están disponibles en https://github.com/hyperledger/hyperledger/wiki/Project-Lifecycle.
<br><br>

## Sentencia de soporte de chaincode

IBM Blockchain no da soporte al código de encadenamiento no determinista, lo que representa un riesgo en la coherencia e integridad de los datos en cualquier red de blockchain. Antes de desplegar nuevo chaincode en la red de IBM Blockchain en Bluemix, revise los detalles en [código de encadenamiento no determinista](nondeterministic.html).

Además del [código de encadenamiento no determinista](nondeterministic.html), las siguientes prácticas de codificación NO están soportadas en las redes de IBM Blockchain:

1. Uso de matrices asociativas con iteración (el orden es aleatorio en Go).
2. Lectura de una lista de elementos desde una tabla KVS (el orden no está garantizado).
3. Grabación del código de encadenamiento de hebras no seguras (se pueden invocar la consulta y la invocación en paralelo).
4. Sustitución de la memoria global o del almacenamiento de memoria caché para los vars de estado de libro mayor en el código de encadenamiento.
5. Acceso a servicios externos, como por ejemplo bases de datos, directamente desde el código de encadenamiento.
6. Uso de bibliotecas o de variables globales que podrían introducir el no determinismo (como utilizar "random" o "time").
7. Iteración mediante GetRows.  

Consulte la biblioteca de ejemplos para ver los ejemplos de códigos de encadenamiento soportados; el directorio contiene ejemplos escritos en Go y Java.
<br><br>

## Consideraciones sobre migración

Existen varios cambios de programación que deben implementarse para que el código desarrollado en Hyperledger Fabric v0.5-developer-preview funcione con el programa de fondo de Bluemix (creado en Hyperledger Fabric v0.6.1).  Consulte la sección [Consideraciones sobre migración](http://hyperledger-fabric.readthedocs.io/en/v0.6/v0.6_migration/) de la documentación de Hyperledger Fabric para obtener más información detallada sobre nuevas funciones y cambios de código.  

## Problemas conocidos de HSBN

1. Al utilizar la Red empresarial de alta seguridad, que utiliza Hyperledger Fabric v0.6.1, se recomienda el restablecimiento de la red periódicamente durante una fase de desarrollo si ha habido más de aproximadamente cincuenta despliegues de códigos de encadenamiento. Al restablecer la red se elimina el código encadenado desplegado y los datos que se han recopilado. Esto ofrece la oportunidad de quitar el código de encadenamiento antiguo que haya sido reemplazado por mejoras realizadas durante una fase de desarrollo iterativo.  Si está en una fase posterior al desarrollo, debería supervisar el número de despliegues de código de encadenamiento para dejar capacidad para el código de encadenamiento más importante.
2. Se han recibido errores esporádicos "503 Servicio no disponible" y "502 Pasarela errónea" al realizar una consulta de estado de la red y los iguales.
3. Posibilidad de mensajes "Server.Serve no ha podido completar el reconocimiento de seguridad" en los registros para vp1. Se trata de un error no muy grave y no está relacionado con el funcionamiento de la red.
4. Las **credenciales de servicio** podrían no autorrellenarse; en este caso, genere las credenciales de la siguiente forma:

 a) Desde el Panel de control de servicio, pulse el separador **Credenciales de servicio**:

  ![Credenciales de servicio HSBN](images/hsbn.png "Credenciales de servicio HSBN")

 b) En el separador **Credenciales de servicio**, pulse el botón para **Nueva credencial**:

  ![Nueva credencial HSBN](images/hsbn1.png "Nueva credencial HSBN")

c) Aparece una nueva ventana titulada **Añadir credencial nueva**; pulse el botón **Añadir** en la parte inferior de esta ventana:

  ![Añadir nueva credencial HSBN](images/hsbn2.png "Añadir nueva credencial HSBN")

 d) Ahora su pantalla tendrá un aspecto similar al del siguiente ejemplo. Al pulsar en **Ver credenciales** aparecerá una carga útil JSON que contiene las credenciales de servicio de su instancia de HSBN.  

  ![Credenciales generadas HSBN](images/hsbn3.png "Credenciales generadas")



## Obtención de ayuda

Para el soporte y la ayuda con la red de IBM Blockchain on Bluemix, consulte [Obtención de soporte](ibmblockchain_support.html).
