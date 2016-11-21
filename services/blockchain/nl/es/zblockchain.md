---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Blockchain en z
{: #zblockchain}
Última actualización: 8 de julio de 2016
{: .last-updated}



Puede utilizar el servicio de blockchain en la oferta dedicada de Bluemix con z/OS para crear activos digitales privados y seguros, que podrán comercializarse de forma rápida y segura por las redes autorizadas.  *(Información adicional como parte de la descripción breve)*
{:shortdesc}


* ¿Está justificado que la cantidad de contenido esté en su propia sección, o preferimos dejarla como tema incluido bajo "Acerca de"?
* Espere información en relación con PBFT, Seguridad, Rendimiento, Soporte.


## PBFT
{: #PBFT}

Practical Byzantine Fault Tolerance (PBFT) es un protocolo de consenso trascendental que puede conectarse y configurarse para el despliegue. El paquete `obcpbft` es una implementación del protocolo de consenso [PBFT](http://dl.acm.org/citation.cfm?id=571640 "PBFT") fundamental, que proporciona consenso entre los validadores a pesar de que un umbral de validadores actúen como *Bizantinos*, es decir, sean malintencionados o que fallen de una forma imprevista. En la configuración predeterminada, PBFT y Sieve se han diseñado para ejecutarse en al menos *3t+1* validadores (réplicas), tolerando hasta *t* réplicas defectuosas (incluidas las malintencionadas o *Bizantinas*). Para obtener más información sobre funciones PBFT, consulte la sección [especificación de protocolo](https://github.com/hyperledger/fabric/blob/master/docs/protocol-spec.md#fabric) de Hyperledger Project de Linux Foundation. 

Vea una [![vista previa](http://www.youtube.com/watch?v=EKa5Gh9whgU)(http://img.youtube.com/vi/EKa5Gh9whgU/0.jpg)]

*(Es necesario indicar una razón práctica por la que los usuarios necesitan conocer PBFT. ¿Qué función desempeña PBFT en el soporte de Blockchain en z y su relación con este soporte.)*


### Casos de anomalía soportados
{: #failure}

*A qué casos de anomalía se da soporte y a qué casos no se da soporte aquí.*

*(Barry Mosakowski/Raleigh/IBM o Tuan Dang/Raleigh/IBM pueden proporcionar más detalles.)*

### Disponibilidad de la oferta dedicada con z/OS
{: #Availability}

*Disponibilidad y expectativas acerca de la disponibilidad en base a las pruebas de PBFT.*

*(Se necesitan más detalles.)*

### Verificación de la funcionalidad básica de PBFT
{: #Test PBFT}

*(Información de Gari. Se necesitan más detalles de Jason sobre cómo realizar los pasos de prueba, incluidas las capturas de pantalla.)*

Para verificar la funcionalidad básica de PBFT, lleve a cabo los siguientes pasos:

1. Someta transacciones enviar través de uno o más iguales en la red.
2. Verifique que al menos *2f+1* (3 en este caso) iguales tienen el mismo estado. *(¿Cómo se verifica? Se necesitan detalles del caso de prueba.)*

  *Un ejemplo de la utilización de la API REST*
3. En el panel de control, pulse el botón para detener el igual 4. *(Utilice la funcionalidad "detener igual" del panel de control para detener el igual 4. Es necesario el caso de prueba para describir la operación en detalle.)*
4. Verifique que la red sigue procesándose. *(¿Cómo se verifica?)*
5. En el panel de control, pulse el botón para detener el igual 3.
6. Verifique que la red detiene su proceso.
7. En el panel de control, pulse el botón para reiniciar el igual 3.

Si el igual 3 se recupera y la red sigue procesándose, puede utilizar las funciones PBFT básicas.

**Notas:**
* Después de reiniciar el igual 3, es necesario esperar el tiempo de espera antes de someter nuevas transacciones al igual 3.

* Las transacciones, que se envían a iguales activos cuando la red detiene su proceso, se almacenan en búfer y se someten a la red después de que la red continúe su proceso.

## Entorno para Blockchain en z
{: #z environment}

Para utilizar el servicio de blockchain en la oferta dedicada de Bluemix con z/OS, asegúrese de que el entorno satisface los siguientes requisitos:

* Cuatro redes de iguales que están ejecutando PBFT con los servicios de pertenencia. Para obtener más información sobre servicios de pertenencia, consulte la sección [especificación de protocolo](https://github.com/hyperledger/fabric/blob/master/docs/protocol-spec.md#fabric) de Hyperledger Project de Linux Foundation. 
* Una red aislada que no tiene memoria o sistemas compartidos.
* Iguales aislados dentro de la red.
* Un sistema que está protegido de los administradores del sistema en nube.

El supervisor de blockchain proporciona una visión general del entorno de blockchain y recupera detalles sobre la red. Para obtener más información sobre el entorno de blockchain y cómo supervisarlo, consulte [Gestión del código de encadenamiento con el supervisor de blockchain](https://new-console.ng.bluemix.net/docs/services/blockchain/ibmblockchainmonitor.html) y [Apps de ejemplo y guías de aprendizaje para blockchain](https://new-console.ng.bluemix.net/docs/services/blockchain/ibmblockchain_tutorials.html).

## Seguridad

*¿No se proporciona información de seguridad en el documento?*

## Rendimiento

*¿No se proporciona información de rendimiento en el documento?*

## Obtención de soporte al cliente

Si tiene problemas con el servicio de blockchain en la oferta dedicada de Bluemix con z/OS, siga el proceso de resolución de problemas de IBM Bluemix. Consulte [Resolución de problemas](https://new-console.ng.bluemix.net/docs/troubleshoot/troubleshoot.html) para obtener más información sobre cómo obtener ayuda.
