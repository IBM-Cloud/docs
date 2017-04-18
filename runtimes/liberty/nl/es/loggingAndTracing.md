---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-09"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Registro y rastreo
{: #logging_tracing}

## Archivos de registro
{: #log_files}

Los registros estándares de Liberty, como messages.log o el directorio ffdc, están disponibles en IBM Bluemix en el directorio de registros de cada instancia de aplicación. Se puede acceder a estos registros desde la consola de IBM Bluemix o mediante los mandatos cf logs y cf files.
Por ejemplo, para ver el archivo messages.log, ejecute el mandato:
```
    $ cf files <yourappname> logs/messages.log
```
{: codeblock}

El nivel de registro y otras opciones de rastreo se pueden establecer mediante el archivo de configuración de Liberty. Para obtener más información, consulte el tema sobre [Perfil de Liberty: rastreo y registro](http://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/rwlp_logging.html?cp=SSAW57_8.5.5%2F3-17-0-0). El rastreo también se puede ajustar en una instancia de aplicación en ejecución mediante la consola de IBM Bluemix.

## Utilización de las funciones de rastreo y volcado
{: #using_trace_and_dump}

En la interfaz de usuario de IBM Bluemix, dispone de funciones de rastreo y volcado.
* Utilice Trace para ver y actualizar el registro de Liberty
traceSpecification en instancias de la aplicación en ejecución.
* Utilice Dump para crear volcados de hebras y de almacenamiento dinámico en instancias de la aplicación en ejecución.

Para realizar esta acción, seleccione una aplicación de Liberty en la interfaz de usuario. En la categoría Tiempo de ejecución en la navegación, puede abrir los detalles de la instancia. Seleccione una o varias instancias. En el menú Acciones, puede elegir TRACE o DUMP.

## Descargue archivos de volcado
{: #download_dumps}

<strong>Requisito previo:</strong>
* [Instale la CLI de CF](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html)
* [Instale el plugin Diego-Enabler](https://github.com/cloudfoundry-incubator/Diego-Enabler) si la aplicación se ejecuta en Diego

<strong>Si la aplicación se ejecuta en DEA, siga los pasos siguientes:</strong>
  
1. obtenga app_guid
```
$ cf app <app_name> --guid
```

2. descargue el archivo de volcado
```
$ cf curl /v2/apps/<app_guid>/instances/<instance_id>/files/dumps/<dump_file_name> --output <local_dump_file_name>
```

<strong>Si la aplicación se ejecuta en Diego, siga los pasos siguientes:</strong>
  
1. obtenga app_guid
```
$ cf app <app_name> --guid
```

2. obtenga app_ssh_endpoint(host and port) and app_ssh_host_key_fingerprint
```
$ cf curl /v2/info
```

3. obtenga ssh-code para mandato scp
```
$ cf ssh-code
```

4. archivo de volcado remoto scp en local, utilice ssh-code cuando se le solicite una contraseña
```
$ scp -P <app_ssh_endpoint_port> -o User=cf:<app_guid>/<instance_id> <app_ssh_endpoint_host>:/home/vcap/dumps/<dump_file_name> <local_dump_file_name>
```

Consulte [Cómo acceder a apps con SSH](https://docs.cloudfoundry.org/devguide/deploy-apps/ssh-apps.html) para obtener más información


# rellinks
{: #rellinks}
## general
{: #general}
* [Tiempo de ejecución de Liberty](index.html)
* [Visión general del perfil de Liberty](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)

