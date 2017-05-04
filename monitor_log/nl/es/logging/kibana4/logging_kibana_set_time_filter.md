---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Establecimiento de un filtro de tiempo
{: #set_time_filter}

Vea y filtre registros de {{site.data.keyword.Bluemix}} comprendidos en un periodo de tiempo configurando el *Selector de tiempo*.
{:shortdesc}

Puede configurar el *Selector de tiempo* en la página Descubrir. De forma predeterminada, está establecido en los últimos 15 minutos. 

Siga estos pasos para buscar entradas que incluyan un determinado tiempo:


1. En la barra de menús de la página Descubrir, pulse Selector de tiempo ![Selector de tiempo](images/k4_time_picker_icon.jpg "Selector de tiempo").

2. Configure el intervalo de tiempo. 

    Puede definir cualquiera de los siguientes tipos de intervalos de tiempo:
    
    * Rápido: son intervalos de tiempo predefinidos que incluyen los casos más comunes de los intervalos de tiempo Relativo y Absoluto; por ejemplo *Hoy* y *Este mes*. 
    
        ![Opciones rápidas del Selector de tiempo](images/k4_time_picker_quick.jpg "Opciones rápidas del Selector de tiempo")
    
    * Relativo: son intervalos de tiempo en los que puede especificar la fecha y hora de inicio y la fecha y hora final. Las puede redondear por hora. 
    
        ![Opciones relativas del Selector de tiempo](images/k4_time_picker_relative.jpg "Opciones relativas del Selector de tiempo")
    
    * Absoluto: son intervalos de tiempo entre una fecha inicial y una fecha final.
    
        ![Opciones relativas del Selector de tiempo](images/k4_time_picker_absolute.jpg "Opciones absolutas del Selector de tiempo")
      

Después de configurar un intervalo de tiempo, los datos que aparecen en Kibana corresponden a las entradas comprendidas en dicho rango de tiempo. 



