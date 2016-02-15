{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}


# Problemas de servicios generales
{: #general}

*Última actualización: 9 de diciembre de 2015*

Entre los problemas de los servicios de {{site.data.keyword.Bluemix}}
se pueden incluir los errores de tiempo de espera agotado de pasarela que se producen al suprimir
una instancia de servicio. Sin embargo, en muchos de los casos, puede solucionar estos problemas siguiendo unos sencillos pasos.
{:shortdesc}

## Se muestra un mensaje de error de tiempo de espera excedido de pasarela cuando suprime una instancia de servicio
{: #ts_service_broker}

Es posible que reciba un mensaje de error cuando intente suprimir una instancia de servicio que ya se ha suprimido desde el controlador de la nube.
{:shortdesc}


Cuando intenta suprimir una instancia de servicio, ve el mensaje de error del intermediario de servicios, ```Tiempo de espera excedido de pasarela```.
{: tsSymptoms}


Este problema sucede si la instancia de servicio ya se ha suprimido desde el controlador de la nube.
{: tsCauses}


Para resolver este problema, cree una instancia de servicio con el mismo nombre de servicio y luego enlácela a las apps. Después puede suprimir la instancia de servicio y las apps que utilizan el servicio.   
{: tsResolve}


