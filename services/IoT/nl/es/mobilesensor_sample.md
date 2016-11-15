---

copyright:
  years: 2016

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}

# Ejemplo de Mobile Device Sensor

El ejemplo de Mobile Device Sensor utiliza JavaScript para conectar el teléfono al {{site.data.keyword.iot_full}} y publicar datos de sensor en su organización {{site.data.keyword.iot_short}}.
{:shortdesc}

La biblioteca de cliente de Python de {{site.data.keyword.iot_short}} se utiliza para suscribirse a los mandatos y visualizar los datos del sensor que publica su teléfono. La visualización de datos se presenta en un sitio web que se crea en la infraestructura de Web Server Gateway Interface (WSGI).

Esta aplicación muestra un enfoque para controlar el acceso de usuario a los datos de sensores desde dispositivos específicos. Cuando se pulsa **Let's Play (Juguemos)**, la aplicación crea un registro de usuario en una base de datos {{site.data.keyword.cloudantfull}} e invoca la API de gestión de dispositivos de {{site.data.keyword.iot_short}} para registrar el dispositivo.

## Requisitos previos

Antes de desplegar este ejemplo:

- Cree una cuenta de {{site.data.keyword.bluemix_notm}} e inicie la sesión. Para obtener más información sobre {{site.data.keyword.bluemix_notm}}, consulte [Inicie su prueba gratuita](https://apps.admin.ibmcloud.com/manage/trial/bluemix.html).
- Descargue e instale la interfaz de línea de mandatos de Cloud Foundry. La interfaz de línea de mandatos de Cloud Foundry le permite modificar y desplegar instancias de servicio en {{site.data.keyword.bluemix_notm}}. Para obtener más información, consulte [Empiece la codificación con la interfaz de línea de mandatos de cf](https://www.ng.bluemix.net/docs/#starters/install_cli.html)

## Despliegue de este ejemplo

Para desplegar su propia copia de este ejemplo en {{site.data.keyword.bluemix_notm}}, utilice los pasos siguientes:

1. Cree una nueva aplicación Python en {{site.data.keyword.bluemix_notm}}.
  a. En el panel de control de {{site.data.keyword.bluemix_notm}}, pulse **Crear app** y, a continuación, pulse **Web**.
  b. Seleccione **Python** y pulse **Continuar**.
  c. Elija un nombre de aplicación y pulse **Finalizar**.
  Su aplicación Python se está transfiriendo ahora.
2. Cree una instancia del servicio de {{site.data.keyword.cloudant_short_notm}}.
  a. En el panel de control de {{site.data.keyword.bluemix_notm}}, pulse **Utilizar servicios o API**.
  b. Seleccione **Datos y análisis** en el menú y pulse **Cloudant NoSQL DB**.
  c. Pulse **Crear**.
3. Enlace la instancia de {{site.data.keyword.cloudant_short_notm}} NoSQL DB y la instancia de {{site.data.keyword.iot_short}} a su aplicación Python.
  a. Pulse **Enlazar un servicio o API**.
  b. Seleccione el servicio de {{site.data.keyword.cloudant_short_notm}} NoSQL DB y la instancia de {{site.data.keyword.iot_short}} y pulse **Añadir**.
4. Clone el repositorio de [{{site.data.keyword.iot_short}} Python Github](https://github.com/ibm-messaging/iot-python.git). Para clonar el repositorio desde una interfaz de línea de mandatos, vaya al directorio que será el destino de la clonación del repositorio y ejecute el mandato siguiente:
```
$ git clone https://github.com/ibm-messaging/iot-python.git
```
5. En la interfaz de línea de mandatos, cambie el directorio al ejemplo de Mobile Device Sensor utilizando el mandato siguiente:
```
$ cd iot-python/samples/bluemixZoneDemo
```
6. Envíe su aplicación por push a {{site.data.keyword.bluemix_notm}} utilizando el mandato siguiente, sustituyendo `app_name` por el nombre de su aplicación Python:
```
$ cf push app_name -m 32M -b https://github.com/cloudfoundry/cf-buildpack-python.git -c "python server.py"
```
7. Abra `http://app_name.mybluemix.net/` en un navegador web en el teléfono. Debería ver una página que ilustra cómo

Verá una página que ilustra cómo, utilizando la mensajería MQTT, los datos del acelerómetro del teléfono
se envían al <keyword conref="cloudoeconrefs.dita#cloudoeconrefs/iot_short"/>, y una aplicación 
<keyword conref="cloudoeconrefs.dita#cloudoeconrefs/bluemix_short"/> utiliza estos datos para duplicar
los movimientos. Especifique el ID de dispositivo, pulse <uicontrol>Conectar</uicontrol>, y continúe, intentando
mover el teléfono.
