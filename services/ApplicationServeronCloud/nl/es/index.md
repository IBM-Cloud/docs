---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-01"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Iniciación a IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}
{: #getting_started}

{{site.data.keyword.IBM}} WebSphere Application Server for {{site.data.keyword.Bluemix}} es un servicio que facilita una configuración rápida en una instancia pre-configurada de WebSphere Application Server Liberty, Traditional Network Deployment o Traditional WebSphere Java EE en un entorno de nube alojado en {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

## Visión general de WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}
{: #overview}

WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} proporciona a los consumidores servidores de WebSphere tradicional y Liberty Profile ya configurados. Está alojado en invitados de máquinas virtuales con acceso raíz al sistema operativo invitado. Cuando cree un servicio, elija entre *Liberty*, *Traditional ND* o *Traditional WebSphere*.

**Nota:** los clientes ahora pueden elegir entre V8.5 y V9.0 al crear una nueva instancia de *Traditional ND* o *Traditional WebSphere*.

Se le proporciona una experiencia de administración de WebSphere familiar y tiene acceso completo al sistema operativo subyacente. Puede reutilizar los scripts existentes y realizar los pequeños ajustes necesarios en el sistema para trabajar con infraestructuras propias o de terceros. El centro de administración y las consolas de administración se proporcionan para administrar su servicio de WebSphere Application Server Liberty, ND o tradicional, igual que las configuraciones de WebSphere locales.

El Plan de WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} Network Deployment consiste en un entorno de células de WebSphere Application Server Network Deployment con dos o más máquinas virtuales. La primera máquina virtual contiene el Gestor de despliegue e IBM HTTP Server y las demás máquinas virtuales contienen nodos personalizados (agentes de nodo) federados en el Gestor de despliegue. Utilice sus scripts wsadmin existentes para crear su configuración de WebSphere o utilizar WebSphere Admin Console para configurar manualmente el entorno. Estas nuevas funciones permiten a los usuarios configurar un entorno en clúster, lo que constituye un aspecto básico para cualquier aplicación de empresa de middleware. 
Ahora los clientes pueden optar por agrupar en clúster una topología para cargar solicitudes de carga en dos o más instancias.


El plan de WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} Liberty Core incluye el uso de un Liberty Collective. Liberty Collective es un dominio administrativo para un grupo de perfiles de Liberty (servidores) y consta de dos o más máquinas virtuales. La
primera máquina virtual contiene el servidor Collective Controller liberty, que es un punto de control
para Liberty Collective. Además del liberty collective, esta máquina virtual también
contiene el servidor HTTP de IBM, que permite el acceso a sus aplicaciones desde un navegador web. Las
máquinas virtuales restantes son hosts colectivos donde residen los miembros colectivos (servidores de perfil
liberty). La función Liberty Admin Center también está activada en el servidor controlador de liberty.

En la figura siguiente se muestra la arquitectura de los entornos WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} Network Deployment Cell y Liberty Collective.

Figura 1. Arquitectura de la célula de despliegue de red y Liberty colectivo

![Figura 1. Arquitectura de la célula de despliegue de red y de Liberty colectivo](images/CellCollectiveDiagram.gif)

**Nota**: en la *Figura 1* anterior, el patrón que muestra la colocación de Deployment Manager o del controlador colectivo con IBM HTTP Server está pensado para entornos de desarrollo y de prueba. WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} también le ofrece la libertad de volver a configurar el software preinstalado para que se ajuste a sus requisitos operativos y de las aplicaciones de producción; al igual que lo haría con el entorno local. Además, para los requisitos de producción más estrictos, póngase en contacto con el representante de ventas de IBM, quien le dará información sobre la oferta IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} de un solo arrendatario, que ofrece recursos aislados de red y de cálculo. 


## Entorno operativo
{: #operational_environment}

IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} es un servicio que devuelve invitados (máquinas virtuales) en un entorno compartido para que los consumidores desplieguen aplicaciones. Una VPN protege el servicio público de exploraciones de puerto genéricas y otros ataques basados en red no solicitado. Sin embargo, es importante tener en cuenta que la VPN del servicio que se utiliza para acceder a la instancia de servicio puede compartirse entre varias organizaciones y usuarios de {{site.data.keyword.Bluemix_notm}}. Las máquinas virtuales proporcionan recursos de cálculo, memoria y E/S, que vienen de una agrupación compartida de recursos de IaaS.

Puesto que los recursos específicos de cálculo, memoria y E/S los ejecutan máquinas virtuales en un entorno compartido, las configuraciones de servicio pueden variar. Las configuraciones para cada instancia de servicio determinada se pueden visualizar a través de los paneles de control y portales del servicio IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}.

IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} ofrece instancias de máquina virtual. Con estas instancias, los clientes utilizan un portal simple para crear y gestionar despliegues de WebSphere Application Server de forma repetible y coherente y con gran flexibilidad para ajustar sus aplicaciones. Los usuarios pueden empezar a trabajar con sus máquinas virtuales WebSphere Application Server Liberty, ND o tradicional ya configuradas en un entorno de nube alojado. Los usuarios pueden migrar las aplicaciones existentes de WebSphere Application Server a {{site.data.keyword.Bluemix_notm}} y tener un control total del sistema operativo y el middleware subyacentes.

## Estrategia de fijación de precios
{: #pricing_strategy}

IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} proporciona instancias de tamaños de camisetas para clientes con aplicaciones que utilizan mucha memoria con el objeto de dimensionar adecuadamente el entorno con máquinas virtuales de mayor tamaño. Los clientes pueden seleccionar el tamaño de recurso específico de un componente de WebSphere Application Server específico o un único sistema hasta una máquina virtual con 32 GB de RAM.

Las siguientes tablas representan los precios de planes de IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} desde el 1 de abril de 2016 que se representan en Dólares de EE UU (USD).

*Tabla 1. Plan de Liberty Core*

| **Camiseta** | **vCPU** | **RAM (GB)** | **HD (GB)** | **Precio/Hora** |       
|:-------------:|:----------:|:--------------:|:-------------:|:--------------:|
| S | 1 | 2 | 12 | $0.21 |
| M | 2 | 4 | 25 | $0.42 |
| L | 4 | 8 | 50 | $0.84 |
| XL | 8 | 16 | 100 | $1.68 |
| XXL | 16 | 32 | 200 | $3.36 |

*Tabla 2. Plan base de WebSphere Application Server*

| **Camiseta** | **vCPU** | **RAM (GB)** | **HD (GB)** | **Precio/Hora** |       
|:-------------:|:----------:|:--------------:|:-------------:|:--------------:|
| S | 1 | 2 | 12 | $0.30 |
| M | 2 | 4 | 25 | $0.60 |
| L | 4 | 8 | 50 | $1.20 |
| XL | 8 | 16 | 100 | $2.40 |
| XXL | 16 | 32 | 200 | $4.80 |

*Tabla 3. Plan de WebSphere Application Server ND*

| **Camiseta** | **vCPU** | **RAM (GB)** | **HD (GB)** | **Precio/Hora** |       
|:-------------:|:----------:|:--------------:|:-------------:|:--------------:|
| S | 1 | 2 | 12 | $0.70 |
| M | 2 | 4 | 25 | $1.40 |
| L | 4 | 8 | 50 | $2.80 |
| XL | 8 | 16 | 100 | $5.60 |
| XXL | 16 | 32 | 200 | $11.20 |

<p></p>

IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} se ofrece de conformidad con la siguiente métrica de cargos:

*  *Instancia-hora*: una instancia se define como acceso a una configuración específica del servicio IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}. Los clientes deben pagar por cada hora completa o parcial para cada instancia del servicio que se despliegue durante el período de facturación. Cada hora de instancia se factura mensualmente y, si una instancia solo se utiliza una parte del mes, la tarifa de uso se prorratea.

Por ejemplo, si utiliza el plan ND, una instancia equivale a 1vCPU con 2 GB de RAM y HD de 12 GB. Por consiguiente, si opta por configurar su célula con un nodo de control y ocho nodos personalizados, se le cobrarán nueve nodos (instancias).

**Nota**: la facturación mínima se establece en 0,25 de hora de instancia por nodo personalizado o host Liberty. En el ejemplo anterior, un nodo de control y un nodo personalizado configurado para un mínimo de 15 minutos equivaldría a un cargo mínimo de (0,25 * número de instancias).

**Nota**: debido a una cantidad específica de recursos de cálculo, memoria y entrada y salida, los clientes tienen un cargo para instancias acumuladas en el estado DETENIDO a una tasa reducida del 5%. Los clientes se gestionan en un número fijo de instancias DETENIDAS con no más de 10 direcciones IP o 64 GB de memoria.

# rellinks
{: #rellinks}
## general
{: #general}
* [WASdev](https://developer.ibm.com/wasdev/){: new_window}
* [Documentación de WebSphere Application Server V9](http://www.ibm.com/support/knowledgecenter/SSEQTP_9.0.0/as_ditamaps/was900_welcome_base.html){: new_window}
