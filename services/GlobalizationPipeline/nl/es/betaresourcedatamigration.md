---

copyright:
  years: 2015, 2017
lastupdated: "2016-10-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Migración de datos de recursos de la versión beta
{: #globalizationpipeline_betaresourcedatamigration}

La versión beta de {{site.data.keyword.GlobalizationPipeline_full}} se interrumpirá transcurrido un determinado periodo después del release de la versión GA. Los datos de usuario en instancias beta no se moverán a las instancias de servicio GA. Para conservar los datos después de GA, puede exportar los datos de recursos en los archivos y, a continuación, importar a la instancia nueva. Tenga en cuenta que no puede realizar esta operación utilizando el panel de control del servicio. Además, exportar los datos de recursos en un formato de archivo de recursos no conservará otros metadatos asociados con las entradas de recursos.

Para dar soporte a la migración de datos de beta a GA, se ha añadido una característica a la herramienta de línea de mandatos de Java de {{site.data.keyword.GlobalizationPipeline_short}}. El origen de la herramienta está alojado en https://github.com/IBM-Bluemix/gp-java-tools y su release binario también estará disponible en el repositorio github. Se publicará la instantánea de desarrollo más reciente. [Descargar.](https://w3-connections.ibm.com/communities/service/html/communityview?communityUuid=589d87cf-d0c7-4e06-ab95-4108547f90aa#fullpageWidgetId=Wa22bb771e29b_4aa9_a114_cfe53fda2cc8&file=5cdaf089-ec7c-4881-b5a0-7ab651491237)

La herramienta utiliza una API REST mejorada tras el release beta para ***cargar entradas de recursos***, por lo tanto, la instancia de servicio del destino debe ser la versión GA. 
* Origen: beta o GA
* Destino: solo GA

Para copiar todos los datos de paquete de una instancia de servicio de Globalización a otra instancia, utilice el mandato siguiente:

```> java -jar gp-cli.jar copy-all-bundles -s <source-service-url> -i <source-instance-id> -u <source-user-id> -p <source-password> --dest-url <dest-service-url> --dest-instance-id <dest-instance-id> --dest-user-id <dest-user-id> --dest-password <dest-password>```


`source/target-service-url`, y otros valores de parámetro se encuentran en las credenciales de servicio de origen/destino, por ejemplo: 

```
{
  "gp-beta": [
    {
      "name": "Globalization Pipeline-7x",
      "label": "gp-beta",
      "plan": "gp-beta-plan",
      "credentials": {
 

      "url": "https://gp-beta-rest.ng.bluemix.net/translate/rest",
        "userId": "bd0b84362c6934d222c3a0a40fc1443b",
        "password": "OGxp6jDqCLCL1ui8kQSPTt1mZDi4EQwu",
        "instanceId": "bd0b84362c6934d222c3a0a40fc1233e"
      }
    }
  ]
}
```
Además, todos los GP CLI se actualizan para que den soporte a las credenciales en formato json además de las opciones individuales `(-s / -i / -u / -p)`. Puede crear un archivo json con contenido como el siguiente: 

creds.json 
```
 {

        "url": "https://gp-rest.stage1.ng.bluemix.net/translate/rest",
        "userId": "36cad58b3a65dc9fe0183208305be137",
        "password": "43F9MRMu9Q8BWRXMLctunUsAe8LTdwq1",
        "instanceId": "b157e3fc63e62d76c50d9f689d7fc965"

} 
```
A continuación, puede especificar el archivo por `-j <json-file>`. En el mandato `copy/copy-all-bundles`, puede sustituir

```-s https://gp-rest.stage1.ng.bluemix.net/translate/rest -i b157e3fc63e62d76c50d9f689d7fc965 -u 36cad58b3a65dc9fe0183208305be137 -p 43F9MRMu9Q8BWRXMLctunUsAe8LTdwq1```

por

`-j creds.json `
 
Como alternativa, puede copiar el paquete de un lugar a otro utilizando el mandato: 

```> java -jar gp-cli.jar copy -s <source-service-url> -i <source-instance-id> -u <source-user-id> -p <source-password> -b <source-bundle-id> --dest-url <dest-service-url> --dest-instance-id <dest-instance-id> --dest-user-id <dest-user-id> --dest-password <dest-password> -d <dest-bundle-id>```


**Nota:** Dos parámetros más: `-b <source-bundle-id>` y `-d <dest-bundle-id>` que puede utilizar además de los copy-all-bundles. Este mandato se puede utilizar para copiar un paquete en la misma instancia. En este caso, puede soltar los parámetros de credenciales de servicio de destino `(--dest-*)`.


Los mandatos anteriores extraen los datos de paquetes existentes y datos de entrada de recursos y los sube a la nueva ubicación. Durante el proceso, se actualizarán algunos campos controlados por el servidor REST (como por ejemplo el campo updatedBy/updatedAt). Además, debido a que estos mandatos no copian datos de configuración ni de enlace de servicio, es posible que tenga que configurar servicios MT en la instancia de destino.


Por ejemplo, la versión beta da soporte a la traducción en árabe a través de Watson Language Translator. En la versión GA, la traducción en árabe ya no se proporciona de forma gratuita. Al transferir datos beta a la nueva instancia de GA, se conservará el contenido en árabe ya traducido. Ningún cambio en el idioma de origen desencadenará la traducción en árabe de forma automática, a menos que configure el enlace Watson para habilitar la traducción en árabe. Este también es el caso cuando la instancia de origen en la versión de GA. El enlace de servicio MT externo es específico de una instancia GP; el enlace/configuración a otra instancia no se transferirá de forma automática. 

