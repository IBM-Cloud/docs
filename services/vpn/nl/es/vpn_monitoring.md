---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Supervisión del estado y el flujo de tráfico
{: #monitor}  
*Última actualización: 17 de marzo de 2016*  

Utilice la característica de supervisión para ver el estado de conexión y el índice del flujo de tráfico entre la pasarela VPN de servidor SoftLayer y la pasarela {{site.data.keyword.vpn_short}}. 
{:shortdesc}  
##Supervisión del panel de control de servicio
{: #dashboard}

Seleccione el separador **Supervisión** para ver las siguientes estadísticas de conexión.

* **Estado de conexión:** estado de la conexión VPN entre la pasarela local o la pasarela VPN de servidor SoftLayer y la pasarela IBM VPN. Valores: 1=UP, -1=DOWN 
* **Velocidad de tráfico de salida en bytes/segundo y paquetes/segundo:** velocidad de tráfico desde la pasarela IBM VPN a la pasarela local o la pasarela VPN del servidor SoftLayer.  
* **Velocidad de tráfico de entrada en bytes/segundo y paquetes/segundo:** velocidad de tráfico desde la pasarela local o la pasarela VPN del servidor SoftLayer a la pasarela IBM VPN.  

Las estadísticas de supervisión se visualizan como gráficos con datos de las últimas 48 horas. Los gráficos se actualizan automáticamente cada 20 minutos. Sin embargo, puede captar los últimos datos en cualquier momento alejándose del separador de supervisión y volviendo al mismo.

**Nota:** los gráficos utilizan la hora UTC (Hora Universal Coordinada) y no la hora local.  
##Supervisión de Logmet
{: #logmet}

Utilice [Logmet](https://logmet.{DomainName}) para ver estadísticas de conexión detalladas. 

1. Inicie la sesión con las credenciales de Bluemix y el espacio y el nombre de organización donde ha creado la instancia del servicio IBM VPN.  
2. Seleccione el icono de carpeta (![](images/folder.png)) en la parte superior derecha.
3. Seleccione **Supervisión de servicio VPN** en la lista de paneles de control para ver los gráficos. Los gráficos utilizan la hora local.  

**Nota:** debe seleccionar el separador **Supervisión** en el panel de control del servicio IBM VPN como mínimo una vez para enviar una consulta a Logmet para crear el panel de control del servicio VPN en Logmet. Logmet tarda hasta 10 minutos después de establecer la conexión VPN en mostrar las estadísticas de conexión.


