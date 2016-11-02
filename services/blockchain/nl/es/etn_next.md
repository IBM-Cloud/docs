---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Prueba adicional
{: #etn_next}
Última actualización: 07 de octubre de 2016
{: .last-updated}

Las siguientes pruebas se ejecutaron en un entorno de Red empresarial de alta seguridad (a menos que se indique lo contrario) para probar la función de código de encadenamiento, libro mayor, ejecuciones largas, simultaneidad y transacciones complejas.  Los validadores y los nodos de servicios de pertenencia se ejecutaron como invitados de máquinas virtuales dentro del contenedor de servicios seguro en el sistema operativo LinuxONE OS.  Los valores utilizados a continuación se han elegido basándose en la entrada de cliente y no deben confundirse con los valores máximos. (Nota: algunas de estas pruebas se repiten en las secciones [SDK de Node.js](etn_txn.html) y [Realización de pruebas de consenso y disponibilidad](etn_pbft.html).)

{:shortdesc}

1. Función de código de encadenamiento: las interfaces de código de encadenamiento se han ejercido para asegurarse de que las transacciones `Desplegar`, `Invocar` y `Consultar` funcionan correctamente utilizando la API REST y la CLI. Tanto la API REST como la CLI se utilizaron para probar todas las funciones de puntos finales, incluidas Block, Blockchain, Chaincode, Network, Registrar y Transactions, tal como se describe en la especificación del protocolo de Hyperledger.
2. Libro mayor: la creación de 20.000 registros de cargas útiles de 1k en el libro mayor basándose en distintos entornos de conducción. Las pruebas incluían un cliente que crea registros de 20K de una forma serializada.
3. Ejecuciones largas: esta prueba se ha realizado enviando invocaciones, altura de cadena y consultas a lo largo de varios nodos durante 72 horas utilizando el código de encadenamiento demo Ejemplo 02.
4. SDK de Node.js: el SDK de Node.js mejorado se ha utilizado para registrar e inscribir usuarios y llevar a cabo despliegue, invocaciones y consulta en un igual en modalidad de desarrollo (iniciar igual con: `peer node start –peer -chaincodedev`) y modalidad de red (iniciar igual con: `peer node start`).
5. Simultaneidad básica: esta prueba se ha realizado enviando invocaciones simultáneas a cada uno de los cuatro iguales durante 10 minutos, con cargas útiles de 1 KB y midiendo la altura de cadena y consultando el estado del libro mayor.
6. Transacciones complejas: esta prueba se ha realizado enviando de forma aleatoria una mezcla de consultas e invocaciones de diversos tamaños de carga útil, que oscilan entre 10k y 500K, a iguales durante 10 minutos. La altura de cadena y la consulta del estado se han medido para asegurar la sincronización del libro mayor compartido en los iguales de red.
