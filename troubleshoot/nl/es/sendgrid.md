{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}

# Resolución de problemas de SendGrid
{: #ts_sendgrid}

*Última actualización: 9 de diciembre de 2015*

Esta es la respuesta a la pregunta sobre el uso de SendGrid en {{site.data.keyword.Bluemix}}.
{:shortdesc}


## No se pueden enviar correos electrónicos mediante SendGrid
{: #ts_sendgrid_email}

Si no puede enviar correos electrónicos utilizando el servicio SendGrid, es posible que haya alcanzado el límite de correos electrónicos que se permiten por instancia de servicio.
{:shortdesc}


Una vez que haya enviado el número máximo de correos electrónicos permitidos, no podrá utilizar el servicio SendGrid para enviar más correos.
{: tsSymptoms}


Si utiliza el servicio SendGrid para enviar correos electrónicos, puede enviar hasta 25.000 por instancia de servicio cada mes. Cuando haya alcanzado el límite, SendGrid deja de enviar correos y no se incurre en cargos adicionales por utilizar el servicio.
{: tsCauses}

Para comprobar el número de correos permitidos que queda, pulse en la instancia del servicio SendGrid desde el panel de control de {{site.data.keyword.Bluemix_notm}} y, a continuación, pulse **ABRIR PANEL DE CONTROL DE SENDGRID**. Puede ver el número en el campo **Crédito restante**.


Si quiere enviar más correos electrónicos cuando haya alcanzado el límite de 25.000 correos por instancia de servicio cada mes, puede añadir otra instancia de servicio. Para obtener más información sobre SendGrid, consulte [Iniciación a SendGrid](https://sendgrid.com/docs/index.html){: new_window}.    
{: tsResolve}

