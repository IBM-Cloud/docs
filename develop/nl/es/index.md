{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:new_window: target="_blank"}

#Desarrollo de apps 
{: #develop-apps-IDS}

*Última actualización: 7 de diciembre de 2015*  

Puede desarrollar apps mediante un entorno de desarrollo integrado
(IDE) o un editor de texto, o bien utilizando {{site.data.keyword.jazzhub}}.
{: shortdesc}

##Desarrollo de apps con Bluemix DevOps Services
{: #dev_ops}

Puede utilizar {{site.data.keyword.jazzhub_short}} para
desarrollar, planificar y efectuar un seguimiento de una aplicación en la nube. Posteriormente, puede desplegarla
en {{site.data.keyword.Bluemix_notm}}. En cuestión de minutos puede ir del código fuente a una aplicación en ejecución.  

{{site.data.keyword.jazzhub_short}}
proporciona dos servicios: {{site.data.keyword.trackplan}} y {{site.data.keyword.deliverypipeline}}. El servicio {{site.data.keyword.trackplan}} se
utiliza para agilizar la planificación. El servicio {{site.data.keyword.deliverypipeline}} automatiza las compilaciones y los despliegues. Encontrará estos servicios en el catálogo de {{site.data.keyword.Bluemix_notm}}. Para obtener más información sobre cómo utilizarlos, consulte [Iniciación a Track & Plan](../services/TrackPlan/index.html#gettingstartedtemplate) e [Iniciación a Conducto de entrega](../services/DeliveryPipeline/index.html#getstartwithCD). 

{{site.data.keyword.jazzhub_short}} también proporciona alojamiento de Git para el control de origen y un IDE Web en el que puede editar, gestionar y desplegar el código. En una app, puede habilitar el alojamiento de Git pulsando el enlace **AÑADIR GIT**, que se encuentra en la esquina superior derecha de la página Visión general de la app. A continuación, puede editar el código de la app en el IDE Web; para ello, pulse **EDITAR CÓDIGO**. Desde el shell de IDE Web puede ejecutar mandatos cf con ayuda de contenido. Por ejemplo, para obtener una lista de todos los mandatos de Cloud Foundry, escriba el siguiente mandato:  
```
help cfo
```
{:pre}
