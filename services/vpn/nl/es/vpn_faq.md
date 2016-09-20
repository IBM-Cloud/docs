---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Preguntas más frecuentes sobre {{site.data.keyword.vpn_short}}
{: #vpn_faq}
*Última actualización: 17 de marzo de 2016*

A continuación se muestran algunas preguntas frecuentes.
{:shortdesc}

1. ¿Qué dispositivos de otros proveedores reúnen los requisitos en los laboratorios de IBM para su interoperatividad con el servicio IBM VPN?

	El laboratorio de IBM ha comprobado los siguientes dispositivos de pasarela VPN para su interoperación con el servicio IBM VPN:

	* Cisco Adaptive Security Appliance (ASA) Software Versión 8.2(1). [Consulte el ejemplo de configuración](vpn_onpremises.html#cisco) 
	* Brocade Vyatta 5415 vRouter 6.7 R7. [Consulte el ejemplo de configuración](vpn_onpremises.html#vyatta){: new_window}
	* Linux StrongSwan U5.1.2/K3.13.0-55-generic. [Consulte el ejemplo de configuración](vpn_onpremises.html#strongswan){: new_window}
	* Linux StrongSwan U5.2.2/K3.13.0-55-generic. [Consulte el ejemplo de configuración](vpn_onpremises.html#strongswan){: new_window}

	Además, un dispositivo de pasarela VPN que cumpla con los estándares de IPSec de cualquier otro proveedor se espera que funcione bien con el servicio IBM VPN.

2. ¿Con qué rapidez se detectará una anomalía de igual?
 
	Un igual erróneo se detecta en el valor de tiempo de espera de estado activo configurado. El valor predeterminado es 60 segundos.

3. ¿Cuántas pasarelas VPN y conexiones puedo crear por servicio VPN?
 
	Puede crear un dispositivo de pasarela VPN por servicio VPN en un espacio Bluemix. Puede definir hasta 16 conexiones a diferentes destinos por pasarela VPN. 

4. ¿Cuándo debo utilizar el servicio IBM VPN en comparación con el servicio Bluemix Secure Gateway?

	Los dos servicios se utilizan para proporcionar conectividad segura entre los recursos de Bluemix y el centro de datos local. 

	Utilice el servicio IBM VPN cuando busque garantizar la conectividad entre dos puntos finales. El servicio VPN forma una conexión Layer 3 IPSec segura entre las redes locales y el entorno de nube de IBM Bluemix. El servicio IBM VPN está disponible para acceder de forma segura solamente a IBM Containers (contenedores de Docker). 

	Utilice el servicio Bluemix Secure Gateway si desea establecer una conexión segura desde un punto final de aplicación específico en Bluemix a otro punto final dentro del centro de datos local. 

5. ¿Puedo utilizar el servicio IBM VPN para acceder a mis contenedores y servidores virtuales dentro del entorno de nube de IBM Bluemix utilizando sus direcciones IP privadas?
 
	Actualmente, el servicio IBM VPN está disponible para acceder únicamente a Bluemix Containers.

6. ¿Puedo definir el servicio IBM VPN a nivel de organización de Bluemix?

	Actualmente, el servicio IBM VPN solamente está disponible a nivel de espacio de Bluemix. Si la organización de Bluemix tiene varios espacios, se puede definir un servicio VPN aparte para cada espacio.

7. ¿Cómo conecto el servicio IBM VPN con el servicio GaaS (SoftLayer Gateway Appliance Service)?

	Puede crear un túnel IPSec para establecer la comunicación segura entre el servicio IBM VPN y SoftLayer GaaS. [Consulte el ejemplo de configuración.](vpn_onpremises.html#gaas){: new_window}
