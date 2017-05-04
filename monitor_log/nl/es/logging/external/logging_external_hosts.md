---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Configuración de hosts de registro externo
{: #thirdparty_logging}

{{site.data.keyword.Bluemix_notm}} mantiene una cantidad limitada de información de registro en la memoria. Cuando se registra información, la información antigua se sustituye por la nueva. Para mantener toda la información de registro, puede guardar los registros de la aplicación Cloud Foundry en un host de registro externo, como un servicio de gestión de registros de terceros o en otro host.{:shortdesc}

Para enviar la secuencia de los registros de su app CF y del sistema a un host de registro externo, realice los pasos siguientes:

  1. Determine el punto final de registro.

	 Puede enviar registros a un agregador de registros de terceros, como Papertrail, Splunk o Sumologic. También puede enviar
registros a un host de syslog, un host de syslog encriptado con TLS (Seguridad de la capa de transporte) o un punto final POST de HTTPS. Los métodos para
obtener los puntos finales del registro varían para los distintos hosts de registro.

  2. Cree un a instancia de servicio proporcionada por el usuario.

	 Utilice el mandato `cf create-user-provided-service` (o `cups`, una versión abreviada del mismo)
para crear una instancia de servicio proporcionado por el usuario:
	 ```
	 cf create-user-provided-service <nombre_servicio> -l <punto_final_registro>
	 ```
	 &lt;nombre_servicio&gt;

	 El nombre de la instancia de servicio proporcionado por el usuario.

	 &lt;punto_final_registro&gt;

	 El punto final del registro al que {{site.data.keyword.Bluemix_notm}} envía los registros. Consulte la tabla siguiente
para sustituir *punto_final_registro* por su valor:

	 <table>
	 <caption>Tabla 1. Valores de punto final de registro</caption>
     <thead>
     <tr>
     <th>Punto final de registro</th>
     <th>Mandato</th>
	 <th>Notas</th>
     </tr>
     </thead>
     <tbody>
     <tr>
     <td>host de syslog</td>
     <td>`cf cups my-logs -l syslog://HOST:PORT`</td>
	 <td>Por ejemplo, para habilitar el registro en Papertrail, escriba `cf cups my-logs -l syslog://<papertrail-url>`. Sustituya
`<papertrail-url>` por el URL de su punto final de registro de Papertrail.</td>
     </tr>
	 <tr>
     <td>syslog-tls host</td>
     <td>`cf cups my-logs -l syslog-tls://HOST:PORT`</td>
	 <td>El certificado debe ser de confianza para una autoridad de certificados. No utilice certificados autofirmados.</td>
     </tr>
	 <tr>
     <td>HTTPS POST</td>
     <td>`cf cups my-logs -l https://HOST:PORT`</td>
	 <td>Este punto final debe estar en Internet de forma pública, y accesible por {{site.data.keyword.Bluemix_notm}}</td>
     </tr>
     </tbody>
     </table>
  3. Enlazar una instancia de servicio a la app.

	 Utilice el mandato siguiente para enlazar la instancia de servicio a su app:

	 ```
	 cf bind-service <appname> <nombre_servicio>
	 ```
	 &lt;nombre_app&gt;

	 El nombre de su app.

	 &lt;nombre_servicio&gt;

	 El nombre de la instancia de servicio proporcionado por el usuario.

  4. Vuelva a transferir la app. Escriba `cf restage appname` para que se apliquen los cambios.

