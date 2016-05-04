---

copyright:
  años: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Iniciación a IBM WebSphere Application Server para Bluemix
{: #getting_started}

*Última actualización: 08 de abril 2016*

{{site.data.keyword.IBM}} WebSphere Application Server for {{site.data.keyword.Bluemix}} es un servicio que facilita la configuración rápida en una instancia de WebSphere Application Server Liberty, Network Deployment o tradicional ya configurada en un entorno de nube alojado en Bluemix.
{: shortdesc}

## Visión general de WebSphere Application Server for Bluemix
{: #overview}

WebSphere Application Server for Bluemix proporciona a los consumidores servidores de perfiles WebSphere y Liberty tradicionales ya configurados. Está alojado en invitados de máquinas virtuales con acceso raíz al sistema operativo invitado. Cuando cree un servicio, elija entre *Liberty*, *ND* o *WebSphere tradicional*.

Se le proporciona una experiencia de administración de WebSphere familiar y tiene acceso completo al sistema operativo subyacente. Puede reutilizar los scripts existentes y realizar los pequeños ajustes necesarios en el sistema para trabajar con infraestructuras propias o de terceros. El centro de administración y las consolas de administración se proporcionan para administrar su servicio de WebSphere Application Server Liberty, ND o tradicional, igual que las configuraciones de WebSphere locales. 

**Nota**: el plan de despliegue en red de WebSphere Application Server for Bluemix incluye ahora más funciones. El plan consiste en un entorno de células de WebSphere Application Server Network Deployment con dos o más máquinas
virtuales. La primera máquina virtual contiene el gestor de despliegue y el servidor HTTP de IBM
y las máquinas virtuales restantes contiene los nodos personalizados (agentes de nodo) federados para el
gestor de despliegue. Utilice sus scripts wsadmin existentes para crear su configuración de WebSphere o utilizar WebSphere Admin Console para configurar manualmente el entorno. Estas nuevas funciones permiten a los usuarios configurar un entorno en clúster para obtener alta
disponibilidad, migración tras error y escalabilidad. La agrupación en clúster
es un aspecto crítico de cualquier aplicación empresarial de middleware y los clientes ahora pueden elegir agrupar en clúster una topología para cargar solicitudes de carga en dos o más instancias.

El plan núcleo de WebSphere Application Server for Bluemix Liberty incluye ahora más funciones. El plan incluye
la utilización de Liberty Collective, que es un dominio administrativo para un grupo de perfiles de Liberty
(servidores) y consta de dos o más máquinas virtuales. La
primera máquina virtual contiene el servidor Collective Controller liberty, que es un punto de control
para Liberty Collective. Además del liberty collective, esta máquina virtual también
contiene el servidor HTTP de IBM, que permite el acceso a sus aplicaciones desde un navegador web. Las
máquinas virtuales restantes son hosts colectivos donde residen los miembros colectivos (servidores de perfil
liberty). La función Liberty Admin Center también está activada en el servidor controlador de liberty.

En la figura siguiente se muestra la arquitectura de los entornos WebSphere Application Server for Bluemix Network Deployment Cell y Liberty Collective. 

![Figura 1. Arquitectura de la célula de despliegue de red y de Liberty colectivo](images/CellCollectiveDiagram.gif)

## Entorno operativo
{: #operational_environment}

IBM WebSphere Application Server for Bluemix es un servicio que devuelve invitados (máquinas virtuales) en un entorno compartido para que los consumidores desplieguen aplicaciones. Una VPN protege el servicio público de exploraciones de puerto genéricas y otros ataques basados en red no solicitado. Sin embargo, es importante tener en cuenta que la VPN del servicio que se utiliza para acceder a la instancia de servicio puede compartirse entre varias organizaciones y usuarios de Bluemix. Las máquinas virtuales proporcionan recursos de cálculo, memoria y E/S, que vienen de una agrupación compartida de recursos de IaaS. Si desea ejecutar sus aplicaciones en un entorno privado, póngase en contacto con su representante de Ventas de IBM, que puede hablarle de nuestra oferta dedicada de IBM WebSphere Application Server for Bluemix. 

Puesto que los recursos específicos de cálculo, memoria y E/S los ejecutan máquinas virtuales en un entorno compartido, las configuraciones de servicio pueden variar. Las configuraciones para cada instancia de servicio determinada se pueden visualizar a través de los paneles de control y portales del servicio IBM WebSphere Application Server for Bluemix. 

**Nota**: IBM WebSphere Application Server for Bluemix ahora proporciona una opción a los clientes con aplicaciones que utilizan mucha memoria para poder dimensionar adecuadamente el entorno con máquinas virtuales de mayor tamaño. Los clientes pueden seleccionar el tamaño de recurso específico de un componente de WebSphere Application Server específico o un único sistema hasta una máquina virtual con 32 GB de RAM. 

## Estrategia de fijación de precios
{: #pricing_strategy}

IBM WebSphere Application Server for Bluemix ofrece instancias de máquina virtual. Con estas instancias, los clientes utilizan un portal simple para crear y gestionar despliegues de WebSphere Application Server de forma repetible y coherente y con gran flexibilidad para ajustar sus aplicaciones. Los usuarios pueden empezar a trabajar con sus máquinas virtuales WebSphere Application Server Liberty, ND o tradicional ya configuradas en un entorno de nube alojado. Los usuarios pueden migrar las aplicaciones existentes de WebSphere Application Server a Bluemix y tener un control total del sistema operativo y el middleware subyacentes. 

IBM WebSphere Application Server for Bluemix se ofrece de conformidad con la siguiente métrica de cargos: 

*  *Instancia-hora*: una instancia se define como acceso a una configuración específica del servicio IBM WebSphere Application Server for Bluemix. Los clientes deben pagar por cada hora completa o parcial para cada instancia del servicio que se despliegue durante el período de facturación. Cada hora de instancia se factura mensualmente y, si una instancia solo se utiliza una parte del mes, la tarifa de uso se prorratea. 

Por ejemplo, si utiliza el plan ND, una instancia equivale a 1vCPU con 2 GB de RAM y HD de 12 GB. Por consiguiente, si opta por configurar su celda con un nodo de control y ocho nodos personalizados, se le cobrarán nueve nodos (instancias). 

**Nota**: la facturación mínima se establece en 0,25 de hora de instancia por nodo personalizado o host Liberty. En el ejemplo anterior, un nodo de control y un nodo personalizado configurado para un mínimo de 15 minutos equivaldría a un cargo mínimo de (0,25 * número de instancias). 

# rellinks
## general
* [WASdev](https://developer.ibm.com/wasdev/){: new_window}
* [Documentación de WebSphere Application Server](http://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/as_ditamaps/was855_welcome_ndmp.html){: new_window}
* [Documentación de WebSphere Application Server tradicional v9 Beta](http://www.ibm.com/support/knowledgecenter/SSEQTP_9.0.0/as_ditamaps/was900_welcome_base.html){: new_window}
