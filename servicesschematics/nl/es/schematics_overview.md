---

copyright:
  years: 2017
lastupdated: "2017-05-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Acerca de 
{: #about}

{{site.data.keyword.bplong}} puede utilizarse para crear bloques de construcción de infraestructura. Puede juntar servicios de {{site.data.keyword.IBM_notm}} Cloud para crear una infraestructura que sea desplegable y reutilizable.
{:shortdesc}

{{site.data.keyword.bpshort}} utiliza Terraform para simplificar la gestión de la infraestructura. Por ejemplo, si desea aplicar varias copias de seguridad del servicio que utiliza un clúster de servidores de apps, un equilibrador de carga y un servidor de base de datos, puede escribir un script bash para ejecutar mandatos que generen estos componentes. Pero resulta más fácil y rápido, así como más ordenado, tener una configuración con un ejecutador que tome la configuración y la convierta en recursos reales. Con Terraform, puede utilizar varios recursos a la vez, como grupo colectivo, con las dependencias correlacionadas. 

## Motivos para utilizar {{site.data.keyword.bpshort}}
{: #reasons}

Es posible que desee utilizar una infraestructura codificada en los siguientes casos de ejemplo:
{:shortdesc}

| Caso de ejemplo     | Motivos    |
| :------------- | :------------- |
| Desea volver a crear y reutilizar su infraestructura.  | Puede utilizar {{site.data.keyword.bpshort}} para la gestión de infraestructuras. Con {{site.data.keyword.bpshort}}, puede suministrar, modificar y destruir recursos mediante programación. Cuando codifique y configure recursos, puede crear bibliotecas de recursos que se pueden volver a utilizar repetidamente para obtener los mismos resultados.|
| Desea transparencia en la configuración de los entornos.  | {{site.data.keyword.bpshort}} trabaja con configuraciones en control de origen, lo que habilita la colaboración, la revisión y le proporciona un seguimiento de auditoría para ver cómo y cuándo se han realizado los cambios. También puede consultar los cambios si necesita retrotraer a una configuración anterior. |
| Desea simplificar la ejecución de los cambios del entorno.  | {{site.data.keyword.bpshort}} sigue el modelo declarativo que proporciona una única fuente fiable. Cuando planifique un cambio en su entorno, indique el resultado que desea. |
| Ya utiliza una herramienta de gestión de la configuración (CM), pero quiere un método más automatizado para configurar los entornos.  | {{site.data.keyword.bpshort}} trabaja junto con herramientas de CM. Los entornos que se despliegan con {{site.data.keyword.bpshort}} son abstracciones de alto nivel, que pueden crear recursos de infraestructura. Puede utilizar las herramientas de CM para instalar y configurar software en los recursos que ha suministrado {{site.data.keyword.bpshort}}.  
  
## Cómo funciona
{: #how}

Puede desplegar recursos en los entornos utilizando {{site.data.keyword.bpshort}}.
{:shortdesc}

{{site.data.keyword.bpshort}} utiliza Terraform como herramienta subyacente para habilitar la infraestructura como código, de manera que pueda definir los recursos de {{site.data.keyword.IBM}} Cloud como código. Los recursos de nube pueden ser distintos componentes de su infraestructura, como servidores nativos, servidores virtuales, equilibradores de carga, componentes de red definidos por software. 

### Configuraciones para definir recursos
{: #how-define}

Una configuración, o configuración de Terraform, es un archivo que define los recursos que componen su infraestructura. Las configuraciones son arquitecturas desplegables que pueden aplicarse a uno o más entornos. El siguiente diagrama muestra qué compone una configuración y cómo trabajan conjuntamente las distintas piezas para crear un entorno desplegable en {{site.data.keyword.bpshort}}.


![Diagrama de la arquitectura de {{site.data.keyword.bpshort}}](/images/anatomy_of_a_schematic.png)

Figura 1. Diagrama de la arquitectura de {{site.data.keyword.bpshort}} 

### Control de origen para habilitar la colaboración
{: #how-collaborate}

Las configuraciones se almacenan en GitHub, de manera que los equipos puedan revisar el código y colaborar. GitHub le proporciona seguimiento de auditoría integrado y le permite consultar un historial de confirmación completo de los cambios realizados en sus configuraciones. Puede guardar la información de uso en archivos readme para compartir la configuración y que puedan utilizarla varios equipos. 

### Entornos de {{site.data.keyword.bpshort}} para suministrar recursos
{: #how-provision}

Puede utilizar {{site.data.keyword.bpshort}} para explorar el código en GitHub y desplegar los recursos en un entorno. Los entornos pueden compartir configuraciones comunes. Por ejemplo, puede utilizar un entorno de control de calidad temporal que se parezca al de producción y destruirlo al finalizar las pruebas. Puede crear una biblioteca de configuraciones de entorno comunes, en la que todos los usuarios de su cuenta de {{site.data.keyword.Bluemix_notm}} puedan etiquetar y realizar búsquedas.
