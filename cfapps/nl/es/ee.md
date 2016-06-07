---

 

copyright:

  years: 2015 2016

 

---

{:shortdesc: .shortdesc} 
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Caso de ejemplo: Desarrollo completo
{: #ee}

*Última actualización: 18 de abril de 2016*

Puede utilizar la interfaz de usuario y la plataforma de {{site.data.keyword.Bluemix}} y una selección de herramientas para compilar, ejecutar y desplegar sus apps. Para empezar, puede seguir este caso de ejemplo completo de desarrollo.
{:shortdesc}

## Registro
{: #ee_start}

Para poder empezar a trabajar, debe registrarse para obtener un ID de IBM en [https://console.ng.bluemix.net/](https://console.ng.bluemix.net/). A continuación,
puede iniciar una sesión en {{site.data.keyword.Bluemix_notm}} e iniciar su prueba
gratuita de 30 días. {{site.data.keyword.Bluemix_notm}}
proporciona 2 GB de memoria en tiempo de ejecución y 10 instancias de servicio
para la prueba gratuita.

## Creación de una app web mediante la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}
{: #ee_appui}

Después de iniciar la sesión, puede empezar a crear la primera app mediante la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}.

En {{site.data.keyword.Bluemix_notm}}, las apps están asociados a organizaciones y espacios. Una organización es propiedad de varios colaboradores, quienes la utilizan. Inicialmente, obtiene una organización predeterminada que se llama como su nombre de usuario y cuyo único colaborador es usted. También obtiene un espacio dentro de esta organización. El espacio es un entorno en el que ejecutar sus apps; por ejemplo, puede tener un espacio dev como entorno de desarrollo, un espacio test como entorno de prueba y un espacio production como entorno de producción. Además, cada uno de los entornos pertenece a una región. Con {{site.data.keyword.Bluemix_notm}}, puede desplegar las apps en una determinada región geográfica para reducir la latencia de la red, y mejorar la privacidad de los datos y la disponibilidad. Consulte Regiones para obtener detalles.

En este caso de ejemplo, va a desarrollar una app web utilizando Node.js. Supongamos que está en EE. UU. y la mayoría de los usuarios de su app también están en los EE. UU. Decide para crear y ejecutar su app cerca de la base de usuarios, para poder beneficiarse de una menor latencia de la red. Después de iniciar la sesión en {{site.data.keyword.Bluemix_notm}}, pulse el nombre de cuenta en la parte superior derecha y seleccione la región **EE. UU. sur**. A continuación, puede llevar a cabo los
siguientes pasos para crear una app:

  1. Pulse el botón más.
  2. Seleccione **Calcular**>**Aplicaciones CF**>**SDK for Node.js**.
  3. Escriba un nombre exclusivo para la app, como por ejemplo NodoPrueba, y pulse **Crear**. El nombre de la app debe ser exclusivo en todo el entorno {{site.data.keyword.Bluemix_notm}}.
  
Ahora puede ver las instrucciones **Empezar a escribir código**. Puede seguir las instrucciones para descargar el código del iniciador de NodoPrueba, modificarlo y desplegarlo.

Se asigna a la app 1 instancia y 512 MB de cuota de memoria de forma predeterminada. Puede aumentar la memoria o añadir más instancias para obtener una alta disponibilidad de la app, por ejemplo 3 instancias con 1 GB memoria por instancia. Pulse **Ver visión general de la app** para especificar las instancias de la app y cuota de memoria. Por ejemplo, escriba 3 para instancias y 1 GB para cuota de memoria y pulse **Guardar**. También puede ver los archivos, los registros y las variables de entorno que resolver los problemas.

## Enlace de un servicio mediante la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}
{: #ee_bindui}

Después de crear la app, desea conectar a una base de datos a la app. De esta forma, puede almacenar y observar los datos de la app utilizando el lenguaje de consulta de la base de datos. En este caso de ejemplo, opta por utilizar el servicio {{site.data.keyword.cloudant}} que proporciona {{site.data.keyword.Bluemix_notm}}.

Para utilizar servicios dentro de la app, debe crear una instancia de servicio y enlazar la app a la instancia de servicio siguiendo estos pasos:
  1. Pulse **Añadir un servicio o API** en la página Visión general de la app.
  2. En el catálogo de {{site.data.keyword.Bluemix_notm}}, seleccione el servicio {{site.data.keyword.cloudant}}.
  3. Escriba un nombre exclusivo para la instancia de servicio o utilice el nombre predeterminado que ha generado {{site.data.keyword.Bluemix_notm}} y pulse **Crear**.
  4. Se muestra la ventana Volver a transferir aplicación. Pulse **Volver a transferir** para volver a transferir la app.
  
Ahora la app está enlazada al servicio {{site.data.keyword.cloudant}}. Encontrará todos los datos necesarios para que la app se comunique con la instancia de servicio en la variable de entorno VCAP_SERVICES. Por ejemplo, como {{site.data.keyword.Bluemix_notm}} aloja varias apps en la misma máquina virtual, las apps no pueden utilizar el mismo número de puerto HTTP para recibir las solicitudes entrantes. Para evitar conflictos, se asigna un número de puerto exclusivo a cada app. Este número de puerto está disponible bajo la variable VCAP_APP_PORT.

Pulse **Variables de entorno** en la página Visión general de la app para ver toda la lista completa de VCAP_SERVICES para obtener más información:
```
{
   "cloudantNoSQLDB": [
      {
         "name": "Cloudant NoSQL DB-tx",
         "label": "cloudantNoSQLDB",
         "plan": "Shared",
         "credentials": {
            "username": "d72837bb-b341-4038-9c8e-7f7232916197-bluemix",
            "password": "b6fc4708942b70a88853177ee52a528d07a43fa8575a69abeb8e044a7b0a7424",
            "host": "d72837bb-b341-4038-9c8e-7f7232916197-bluemix.cloudant.com",
            "port": 443,
            "url": "https://d72837bb-b341-4038-9c8e-7f7232916197-bluemix:b6fc4708942b70a88853177ee52a528d07a43fa8575a69abeb8e044a7b0a7424@d72837bb-b341-4038-9c8e-7f7232916197-bluemix.cloudant.com"
         }
      }
   ]
}
```

**Nota:** Esta variable de entorno es la serialización de un objeto JSON con una entrada para cada instancia de servicio al que la app está enlazada. La cantidad y el tipo de datos que proporciona cada instancia de servicio dependen del servicio. Cuando la app no utiliza ningún servicio, VCAP_SERVICES es un objeto JSON vacío. Esta variable de entorno solo se utiliza cuando se añade un servicio a la app.

## Creación de una app con la cli cf
{: #ee_cf}

{{site.data.keyword.Bluemix_notm}} proporciona varias herramientas para que empiece a escribir el código de su app, como por ejemplo la interfaz de línea de mandatos cf y herramientas Eclipse. Puede elegir la interfaz de línea de mandatos cf para empezar a escribir el código de la app TestNode.

  1. En primer lugar, descargue y desarrolle el código de la app.
  
    1. Vaya a la página Empezar a escribir código de la app. Pulse el botón **Descargar código del iniciador** para descargar el código de la app.
    2. Extraiga el archivo descargado en un directorio, por ejemplo `C:\test`.
    3. Desarrolle el código con el entorno de desarrollo integrado.
	
  2. Instale la interfaz de línea de mandatos (CLI) **cf**.
  
    1. Descargue el programa de instalación de la herramienta de línea de mandatos cf correspondiente a su sistema operativo.
    2. Siga el asistente de la herramienta para completar la instalación.
    3. Utilice el mandato **cf -v** para verificar la versión de la interfaz de línea de mandatos cf. Por ejemplo:
	
	```
	cf -v
	```
	
    **Requisito:** Asegúrese de utilizar siempre la última versión de la herramienta de línea de mandatos cf.
  3. Después de instalar la interfaz de línea de mandatos **cf**, debe especificar la región de {{site.data.keyword.Bluemix_notm}} con la que desea trabajar mediante el mandato **cf api**. La interfaz de línea de mandatos **cf** utiliza *https://api.URL_Bluemix*, donde *URL_Bluemix* es el URL de la región. El URL de la Región EE.UU. sur es {{Domain}}. Especifique el mandato siguiente para conectarse a {{site.data.keyword.Bluemix_notm}}:
  
  ```
  cf api https://api.ng.bluemix.net
  ```
  
  Para obtener más información sobre cómo conectarse a otras regiones de {{site.data.keyword.Bluemix_notm}}, consulte Regiones de {{site.data.keyword.Bluemix_notm}}. Después de especificar la región de {{site.data.keyword.Bluemix_notm}}, la información sobre ubicación que ha especificado se guarda.
  
  4. A continuación puede iniciar sesión en {{site.data.keyword.Bluemix_notm}} con el mandato cf login.
  
  ```
  cf login -u ID_usuario -p ***** -o nombre_org -s nombre_espacio
  ```
  
  5. Después de iniciar una sesión de {{site.data.keyword.Bluemix_notm}}, estará listo para desplegar la app en {{site.data.keyword.Bluemix_notm}}. Desde el directorio de la app `C:\test`, especifique el siguiente mandato:
  
  ```
  cf push TestNode
  ```
  
  Para obtener más información sobre el mandato **cf push**, consulte Carga de la app.
  
  6. Ahora puede acceder a la app especificando el siguiente URL de app en un navegador:
  ```
  http://TestNode.mybluemix.net
  ```

También puede elegir otras herramientas para crear la
app, como por ejemplo herramientas Eclipse. Para obtener más información, consulte la página Empezar a escribir código de la app en la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}.

## Enlace de un servicio mediante la cli cf
{: #ee_cfbind}

Con {{site.data.keyword.Bluemix_notm}}, puede añadir un servicio utilizando la interfaz de usuario de Bluemix, tal como se describe ha descrito en este caso de ejemplo. Pero también puede enlazar un servicio utilizando la interfaz de línea de mandatos **cf**. Supongamos que desea añadir el servicio {{site.data.keyword.cloudant}} a la app TestNode mediante la interfaz de línea de mandatos cf.

Para utilizar el servicio {{site.data.keyword.cloudant}} dentro de la app, debe crear una instancia del servicio Cloudant, enlazar la app a la instancia de servicio y luego utilizar la instancia de servicio. El mismo procedimiento se aplica a todos los demás servicios.

  1. Cree una instancia de servicio de Cloudant NoSQL DB.
  
  Utilice el mandato cf create-service para crear una nueva instancia de un servicio. Por ejemplo:
  
  ```
  cf create-service cloudantNoSQLDB Shared cloudant100
  ```
  
  También puede utilizar el mandato cf services para ver la lista de las instancias de servicio que ha creado.
  
  ```
  cf services
  ```
  
  Una vez creada la instancia del servicio, cualquiera de sus apps puede enlazar con la misma y utilizarla.
  
  2. Enlazar una instancia de servicio a la app.
  
  Para utilizar una instancia de servicio, debe enlazarla a la app. Utilice el mandato cf bind-service para enlazar una instancia de servicio a una app especificando el nombre de la app y la instancia de servicio que ha creado.
  
  ```
  cf bind-service TestNode cloudant100
  ```
  
  El hecho de enlazar una instancia de servicio a una app permite que {{site.data.keyword.Bluemix_notm}} se comunique con el servicio y permite especificar que una nueva app se comunicará con dicha instancia de servicio. Es posible que para distintos servicios {{site.data.keyword.Bluemix_notm}} procese la app y el servicio de forma diferente durante el enlace. Por ejemplo, es posible que algunos servicios creen un nuevo arrendatario para cada app que se comunica con la instancia de servicio. El servicio responde a {{site.data.keyword.Bluemix_notm}} con información, como credenciales, que se debe pasar a la app para establecer comunicación entre la app y el servicio.

  **Nota:** Si la app se está ejecutando cuando se enlaza a una instancia de servicio, la variable de entorno VCAP_SERVICES no se actualiza hasta que se reinicia la app. Para reiniciar la app, utilice el mandato cf restart.
  
  3. Utilizar la instancia de servicio.
  
  En este caso de ejemplo, la variable de entorno VCAP_SERVICES incluye información, como por ejemplo los elementos siguientes, que una app puede utilizar para conectar con esta instancia de {{site.data.keyword.cloudant}}:
  
  <dl><dt>username</dt>
  <dd>d72837bb-b341-4038-9c8e-7f7232916197-bluemix</dd>
  <dt>password</dt>
  <dd>b6fc4708942b70a88853177ee52a528d07a43fa8575a69abeb8e044a7b0a7424</dd>
  <dt>url</dt>
  <dd>https://d72837bb-b341-4038-9c8e-7f7232916197-bluemix:b6fc4708942b70a88853177ee52a528d07a43fa8575a69abeb8e044a7b0a7424@d72837bb-b341-4038-9c8e-7f7232916197-bluemix.cloudant.com</dd></dt></dl>
  
  Por ejemplo, una app Node.js puede acceder a esta información del siguiente modo:
  ```
  if (process.env.VCAP_SERVICES) {
        var env = JSON.parse(process.env.VCAP_SERVICES);
        var cloudant = env['"cloudantNoSQLDB'][0].credentials;
  } else {
        var cloudant = {
                "username" : "user1",
                "password" : "secret",
                "url" : "https://user1:secret@localhost:25002"
                }
        };
  ```
  
  **Nota:** Tal como muestra el código de ejemplo, para conectarse a una instancia de servicio de {{site.data.keyword.cloudant}}, primero puede comprobar si la variable de entorno VCAP_SERVICES existe. Si existe, la app puede utilizar las propiedades de la variable cloudant para acceder a la base de datos. Sin embargo, si la variable de entorno VCAP_SERVICES no está presente, se utiliza la instancia de servicio {{site.data.keyword.cloudant}} local con los valores predeterminados que se proporcionan.
  
  4. Interactuar con la instancia de servicio.
  
  Puede interactuar con la instancia de servicio utilizando la información sobre credenciales. Las acciones que puede llevar a cabo incluyen leer, escribir y actualizar. El ejemplo siguiente muestra cómo insertar un objeto JSON en la instancia de servicio {{site.data.keyword.cloudant}}:
  ```
  // create a new message
var create_message = function(req, res) {
  require('cloudantdb').connect(cloudant.url, function(err, conn) {
    var collection = conn.collection('messages');

    // create message record
    var parsedUrl = require('url').parse(req.url, true);
    var queryObject = parsedUrl.query;
    var name = (queryObject["name"] || 'Bluemix');
    var message = { 'message': 'Hello, ' + name, 'ts': new Date()
};
    collection.insert(message, {safe:true}, function(err){
      if (err) { console.log(err.stack); }
      res.writeHead(200, {'Content-Type': 'text/plain'});
      res.write(JSON.stringify(message));
      res.end('\n');
    });
  });
}
  ```
  
  5. **Opcional:** Desenlazar o suprimir una instancia de servicio.
  
  Es posible que desee desenlazar o suprimir una instancia de servicio cuando ya no se utilice o cuando desee liberar espacio. Para desenlazar una instancia de servicio de la app, utilice el mandato **cf unbind-service**; para suprimir una instancia de servicio, utilice el mandato **cf delete-service**.

  Para obtener más información sobre los servicios, consulte Servicios. Para obtener más información sobre las opciones **cf** que puede utilizar para gestionar las apps en el entorno {{site.data.keyword.Bluemix_notm}}, emita el mandato **cf --help** en la interfaz de línea de mandatos de **cf**.

  **Nota:** Asegúrese de que ya no necesita una instancia de servicio antes de suprimirla. Al suprimir una instancia de servicio se borran todos los datos asociados a dicha instancia de servicio. Cualquier app enlazada a un servicio suprimido no puede actualizar su variable de entorno VCAP_SERVICES hasta que se reinicia la app.

## Cálculo del coste de la app
{: #ee_billing}

Su prueba gratuita de 30 días ha vencido, pero desea continuar utilizando {{site.data.keyword.Bluemix_notm}}. Debe añadir la información de su tarjeta de crédito para una cuenta de tipo Pague según uso o crear
una cuenta de suscripción para seguir utilizando {{site.data.keyword.Bluemix_notm}}. Sin embargo, {{site.data.keyword.Bluemix_notm}} sigue proporcionando concesiones gratuitas para la mayoría
de las infraestructuras y servicios en tiempo de ejecución, incluso si se pasa a una cuenta de pago. {{site.data.keyword.Bluemix_notm}} no le cargará ningún importe a menos que el uso sobrepase las concesiones gratuitas.

{{site.data.keyword.Bluemix_notm}} proporciona
un estimador y una calculadora para que calcule el coste de su app. Puede ver el coste de TestNode de las siguientes maneras:

  * En el panel de control, pulse TestNode. A continuación, en la página Visión general, pulse **Estimar el coste de esta app** para ver el precio del tiempo de ejecución **SDK para Node.js** y del soporte y el precio mensual total de la app.
  
  * En la página Hoja de precios también puede escribir el uso mensual del tiempo de ejecución y de los
servicios de su app. Por ejemplo, 3 instancias de **SDK para Node.js** con 1 GB memoria para cada instancia. El precio mensual se calcula y se muestra.

También puede calcular el coste de su app de forma manual; para ello, añada el precio
de los tiempos de ejecución y servicios y deduzca la concesión gratuita. Para obtener más información, consulte Cálculo manual de los costes.

## Eliminación de apps
{: #ee_removing}

A medida que crea más apps, la cuota puede llegar al límite. Sin embargo, algunas apps que puede que ya no utilice siguen ocupando la cuota. Es fácil suprimir apps en cualquier momento para liberar un poco de espacio en {{site.data.keyword.Bluemix_notm}}.

En la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}, vaya a la página Visión general de la app, pulse el icono **Menú** y suprima la app que ya no utiliza. También puede utilizar el mandato **cf delete** para suprimir apps.
