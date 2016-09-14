---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configuración de la pasarela en el centro de datos o el servidor SoftLayer
{: #vpn_yourdatacenter}
*Última actualización: 17 de marzo de 2016*

Es necesario una pasarela IPSec VPN en el centro de datos o servidor SoftLayer para formar una conexión segura con el servicio {{site.data.keyword.vpn_short}}. Las siguientes configuraciones de pasarela VPN son necesarias en el centro de datos o servidor SoftLayer:

* Habilite el cruce de Network Address Translation (NAT) en la pasarela VPN solamente si la pasarela VPN está detrás de NAT. 
* Utilice el nombre compartido previamente que ha utilizado al configurar el servicio IBM VPN.
* Añada la siguiente subred como subred remota:
	* Si ha creado contenedores individuales en el espacio de IBM Bluemix, añada 172.31.0.0/16.
	* Si ha creado grupos de contenedores en el espacio de IBM Bluemix, añada 172.30.0.0/16.
	* Si ha creado contenedores individuales y grupos de contenedores en el espacio de IBM Bluemix, añada 172.31.0.0/16 y 172.30.0.0/16.
* Asegúrese de que los valores de cifrado, autenticación y grupo PFS son los mismos en la pasarela IBM VPN y en la pasarela VPN.
