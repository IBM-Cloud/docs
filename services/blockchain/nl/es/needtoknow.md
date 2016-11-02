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
Última actualización: 13 de octubre de 2016
{: .last-updated}

**ATENCIÓN:** Debe revisar la siguiente información antes de utilizar un plan de IBM Blockchain en Bluemix: Desarrollador inicial (Beta) o Red empresarial de alta seguridad (GA).
<br><br>

## Sentencia de soporte de IBM

IBM tiene una larga historia de liderazgo en innovación, que continúa con las ofertas más recientes de IBM Blockchain. Blockchain es una tecnología de progreso rápido proyectada para interrumpir varios sectores, desde finanzas hasta logística. Mediante varios programas de adopción anteriores, los clientes y los socios empresariales de IBM ya están influyendo en la dirección futura de blockchain. IBM Blockchain on Bluemix es uno de tales programas. **Igual que con cualquier nueva tecnología, los usuarios de IBM Blockchain on Bluemix deben estar preparados para cambios rápidos y fundamentales**.  
{:shortdesc}

La arquitectura que hay detrás de IBM Blockchain es el Hyperledger Project de Linux Foundation. Hyperledger Fabric es un proyecto de código abierto bajo el desarrollo activo, actualmente en el estado *Incubación*. Cada contribución a la comunidad de código abierto hace a Hyperledger Fabric más sólido, pero puede presentar solicitudes de adopción. Durante el ciclo de *Incubación*, los clientes pueden utilizar Hyperledger Fabric v0.5 para la prueba y la simulación de red, pero **IBM le advierte frente a la ejecución de activos financieros de valor directamente en una red blockchain de Hyperledger Fabric v0.5**.  
<br>

## Sentencia de código abierto

IBM Blockchain on Bluemix&mdash;tanto el plan Desarrollador inicial como el plan Red empresarial de alta seguridad&mdash;utilizan el código abierto de Hyperledger Fabric v0.5 de Linux Foundation. Los miembros de Hyperledger Project, incluido IBM, aportan código al entramado, después de que es revisado, evaluado y probado por la comunidad. Hyperledger Fabric v0.5 está en este momento en el estado *Incubación*; los detalles sobre el estado de *Incubación*, y de todo el ciclo de vida de Hyperledger Project, están disponibles en https://github.com/hyperledger/hyperledger/wiki/Project-Lifecycle.
<br><br>

## Sentencia de soporte de chaincode

IBM Blockchain no da soporte al [código de encadenamiento no determinista](ibmblockchain_tutorials.html#ndcc), lo que representa un riesgo en la coherencia e integridad de los datos en cualquier red de blockchain. Antes de desplegar nuevo chaincode en la red de IBM Blockchain en Bluemix, revise los detalles en [código de encadenamiento no determinista](ibmblockchain_tutorials.html#ndcc).

Además del [código de encadenamiento no determinista](ibmblockchain_tutorials.html#ndcc), las siguientes prácticas de codificación NO están soportadas en las redes de IBM Blockchain:

1. Uso de matrices asociativas con iteración (el orden es aleatorio en Go).
2. Lectura de una lista de elementos desde una tabla KVS (el orden no está garantizado).
3. Grabación del código de encadenamiento de hebras no seguras (se pueden invocar la consulta y la invocación en paralelo).
4. Sustitución de la memoria global o del almacenamiento de memoria caché para los vars de estado de libro mayor en el código de encadenamiento.
5. Acceso a servicios externos, como por ejemplo bases de datos, directamente desde el código de encadenamiento.
6. Uso de bibliotecas o de variables globales que podrían introducir el no determinismo (como utilizar “random” o "time").
<br><br>

## Obtención de ayuda

Para el soporte y la ayuda con la red de IBM Blockchain on Bluemix, consulte [Obtención de soporte](ibmblockchain_support.html).
