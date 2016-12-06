---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Red empresarial de alta seguridad
{: #etn_overview}
Última actualización: 13 de octubre de 2016
{: .last-updated}

La Red empresarial de alta seguridad de IBM Blockchain se ejecuta en un entorno aislado y altamente seguro que lo distingue de otras ofertas alojadas en la nube. El sistema operativo, el entramado y los nodos están en IBM Secure Service Container, lo que proporciona los niveles de seguridad e impregnabilidad que los clientes empresariales esperan de la tecnología de z Systems.  IBM Secure Service Container también proporciona optimización del rendimiento para la comunicación de igual a igual, disponibilidad, escalabilidad, cifrado de hardware, claves de cifrado a prueba de manipulaciones y VM cifrada de forma segura.  
{:shortdesc}

El entorno (LinuxONE en z) consta de una red de cuatro iguales que implementa PBFT con Servicios de pertenencia habilitado, ejecutándose en un contenedor de aplicaciones.  El contenedor de aplicaciones protege el software de cadena de bloques, el código de cadena y los datos que se ejecutan dentro del sistema. El software de blockchain dentro del arranque seguro se puede firmar, certificar y cifrar, y una vez instalado en el contenedor de aplicaciones, está a prueba de manipulación.  Los usuarios root de la plataforma y los administradores del sistema no pueden acceder ni ver contenido de contenedores seguros.  LinuxONE en z proporciona la conformidad con FIPS, alta protección de nivel de garantía de evaluación, un entorno operativo altamente auditable y una optimización de cifrado.

Consulte la sección [IBM Secure Service Container](etn_ssc.html) para obtener más información sobre las características de seguridad.
