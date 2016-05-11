---

copyright:
 años: 2015, 2016

---

{:new_window: target="_blank"}
# Modalidades de pruebas y de producción

{: #push-sandboxandproduction-modes}

Puede utilizar las Notificaciones push en una de las modalidades siguientes: prueba o
                producción. El recinto de pruebas es un entorno de prueba autocontenido para desarrollar y probar la integración de API push
                con el servicio push de la aplicación de servidor. Configure en primer lugar las modalidades de pruebas y de producción utilizando el Panel de instrumentos Push. Conmute la modalidad de operación del servicio push entre pruebas y producción utilizando la [API REST de Push](https://mobile.{DomainName}/imfpushrestapidocs/){: new_window}. De forma predeterminada,
                estará habilitada la modalidad de pruebas. Sin embargo, cuando se cambia entre modalidades, las etiquetas, los dispositivos y las suscripciones no se comparten entre estas modalidades.


Cuando esté listo para desplegar la aplicación en un entorno activo, seleccione la modalidad PRODUCTION utilizando la API REST de Push. Para obtener información sobre la API REST, consulte la API REST.

Para conmutar la modalidad de operación del servicio push de pruebas a producción:

1. Utilice la llamada de la API PUT ApplicationID Settings REST
2. En el cuerpo de JSON, confirme que la modalidad se ha cambiado utilizando la llamada de la API [GET ApplicationID Settings REST](https://mobile.{DomainName}/imfpushrestapidocs/){: new_window}. La respuesta esperada es "mode": "PRODUCTION
 
 ```
 { 
 "mode": "PRODUCTION"
 }
 ```
1. Una vez que se haya conmutado la modalidad del entorno, ejecute el código del cliente de nuevo para registrar el dispositivo en la modalidad de PRODUCTION.

Para obtener información sobre la API REST, consulte la API REST.
