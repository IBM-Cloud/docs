---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Ejemplos de configuración local
{:#onpremises}
*Última actualización: 17 de marzo de 2016*

La pasarela VPN local se conecta con la pasarela {{site.data.keyword.vpn_short}}. Es posible que sea necesario modificar la configuración de la pasarela local que está utilizando. 
{:shortdesc}

* [Configuración de IBM VPN con strongSwan](vpn_onpremises.html#strongswan)
* [Configuración de IBM VPN con Vyatta](vpn_onpremises.html#vyatta)
* [Configuración de IBM VPN con GaaS (SoftLayer Gateway Appliance Service)](vpn_onpremises.html#gaas)
* [Configuración de IBM VPN con Cisco ASA](vpn_onpremises.html#cisco)

##Configuración del servicio IBM VPN con strongSwan
{: #strongswan} 

La configuración de IBM VPN utiliza la siguiente configuración de ejemplo:

* Subred de contenedores individuales: 172.31.0.0/16
* Subred de grupos de contenedores: 172.30.0.0/16
* Dirección IP de pasarela IBM VPN: 134.168.8.164

La configuración de strongSwan local utiliza la siguiente configuración de ejemplo:

* Dirección IP de pasarela VPN (IP de pasarela de cliente): 169.55.254.166
* Dirección de subred a la que están conectados los puntos finales (subred de cliente): 10.121.33.192/26 

###Para utilizar el servicio IBM VPN con strongSwan, configure lo siguiente:

1. [Configure la pasarela](index.html#gateway).  
2. [Configure la conexión de sitio](index.html#site).  
3. Configure strongSwan.  
	**Nota:** el siguiente ejemplo se basa en Ubuntu 14.10.  
	1. Instale strongSwan:  
		```
		root@rdmnm:~# sudo apt-get install strongswan  
		root@rdmnm:~# ipsec version  
		```
		{: codeblock}
		
		```
		Linux strongSwan U5.1.2/K3.13.0-55-generic  
		Institute for Internet Technologies and Applications  
		University of Applied Sciences Rapperswil, Switzerland  
		See 'ipsec --copyright' for copyright information.		
		```  
		{: screen}

	2. Configure IPSec:  
		* Edite el archivo: /etc/ipsec.conf  
			```
			root@rdmnm:~# more /etc/ipsec.conf  
						
			config setup
					  
			conn %default  
			 ikelifetime=60m  
			 keylife=20m  
			 rekeymargin=3m  
			 keyingtries=1  
			 mobike=no  
			 keyexchange=ikev1  
			 dpdaction=clear  
			 dpddelay=2s  
			include /etc/ipsec.all.conf  
			```
			{: codeblock}

		* Añada el archivo: /etc/ipsec.all.conf  
			```
			root@rdmnm:~# more /etc/ipsec.all.conf  
							
			conn all  
			  auto=add  
			  esp=aes128-sha1-modp1024!  
			  ike=aes128-sha1-modp1024!  
			  right=134.168.8.164  
			  left=169.55.254.166  
			  leftauth=psk  
			  rightauth=psk  
			  rightsubnet=172.31.0.0/16,172.30.0.0/16  
			  leftsubnet=10.121.33.0/24  
			  rightid=%any  
			  leftid=169.55.254.166  
			  ikelifetime=3600s  
			  aggressive=no  
			  keyexchange=ikev1  
			  lifetime=3600s  
			  dpddelay=30s  
			  dpdaction=hold  
			  dpdtimeout=120s  
			```
			{: codeblock}

		* Edite el archivo: /etc/ipsec.secrets 
 
			```  
			root@rdmnm:~# more   /etc/ipsec.secrets  
				  : PSK "567890"
			```
			{: codeblock}

	3. Reinicie IPSec:

		```
		root@rdmnm:~# ipsec restart
		```  
		{: codeblock}

	4. Verifique la configuración:
		* Ejecute el siguiente mandato en el servidor strongswan para verificar el estado IPSec:

			```  
			root@rdmnm:~# ipsec status
			```
			{: codeblock}

			```
			Security Associations (1 up, 0 connecting):
			         all[1914]: ESTABLISHED 48 minutes ago, 169.55.254.166[169.55.254.166]...134.168.8.164[134.168.8.164]
			         all{20}:  INSTALLED, TUNNEL, ESP in UDP SPIs: cb9c3056_i 1595f835_o
			         all{20}:   10.121.33.0/24 === 172.30.0.0/16 
			         all{19}:  INSTALLED, TUNNEL, ESP in UDP SPIs: c6e4ed78_i 8765e42d_o
			         all{19}:   10.121.33.0/24 === 172.31.0.0/16
			```
			{: screen}

		* Verifique el estado de conexión IPSec de IBM VPN en el panel de control del servicio de IBM Bluemix. En la sección **Conexiones de sitios VPN**, el campo de estado debería mostrarse como **ACTIVO**.

	5. Compruebe el syslog de strongSwan, si es necesario:

		```
		tail -f /var/log/syslog
		```
		{: codeblock}
		
		```
		Nov 25 08:03:40 rdmnm charon: 12[IKE] received draft-ietf-ipsec-nat-t-ike-03 vendor ID
		Nov 25 08:03:40 rdmnm charon: 12[IKE] received draft-ietf-ipsec-nat-t-ike-02\n vendor ID
		Nov 25 08:03:40 rdmnm charon: 12[IKE] received draft-ietf-ipsec-nat-t-ike-02 vendor ID
		Nov 25 08:03:40 rdmnm charon: 12[IKE] received draft-ietf-ipsec-nat-t-ike-00 vendor ID
		Nov 25 08:03:40 rdmnm charon: 12[IKE] 129.41.253.120 is initiating a Main Mode IKE_SA
		```
		{: screen}  

##Configuración del servicio IBM VPN con Vyatta
{: #vyatta} 

La configuración de IBM VPN utiliza la siguiente configuración de ejemplo:

* Subred de contenedores individuales: 172.31.0.0/16
* Subred de grupos de contenedores: 172.30.0.0/16
* Dirección IP de pasarela IBM VPN: 129.41.255.27

La configuración de Vyatta local utiliza la siguiente configuración de ejemplo:

* Dirección IP de pasarela VPN (IP de pasarela de cliente): 173.192.83.82
* Dirección de subred a la que están conectados los puntos finales (subred de cliente): 192.168.201.0/24 

###Para utilizar el servicio IBM VPN con Vyatta, configure lo siguiente:

1. [Configure la pasarela](index.html#gateway).
2. [Configure la conexión de sitio](index.html#site). 
3. Configure Vyatta.  

	1. Utilice SSH para iniciar la sesión en el dispositivo de Vyatta:  
		```
		ssh vyatta@173.192.83.82  
		vyatta@vpn:~$ show version  
		```
		{: codeblock}
		
		```
		Version:      VSE6.7R7  
		Description:  Brocade Vyatta 5415 vRouter 6.7 R7  
		Copyright:    2006-2015 Vyatta, Inc.  
		Built by:     autobuild@vyatta.com  
		Built on:     Thu Mar 26 23:12:48 UTC 2015  
		Build ID:     1503262314-56309bf  
		System type:  Intel 64bit  
		Boot via:     image  
		HW model:     X9SCI/X9SCA  
		HW S/N:       0123456789  
		HW UUID:      002590D2-A0A8-0607-0025-90D2A0A80E0F  
		Uptime:       20:12:17 up 2 days, 23:28,  2 users,  load average: 0.33, 0.27, 0.24  
		```  
		{: screen}

	2. Especifique la modalidad de configuración:  
		```
		vyatta@vyatta: configure
		vyatta@vyatta#
		```  
		{: codeblock}

	3. Configure las direcciones IP de acomplamiento de interfaz:  
		```
		Set interface bonding bond0 address 192.168.201.2/24
		Set interface bonding bond1 address 173.192.83.82/29
		```  
		{: codeblock}

	4. Habilite VPN en bond1:  
		```
		set vpn ipsec ipsec-interfaces interface bond1
		```  
		{: codeblock}

	5. Configure el grupo IKE:  
		```
		set vpn ipsec ike-group bm-ike lifetime 28800  
		set vpn ipsec ike-group bm-ike proposal 1 dh-group 2  
		set vpn ipsec ike-group bm-ike proposal 1 encryption aes128  
		set vpn ipsec ike-group bm-ike proposal 1 hash sha1  
		```  
		{: codeblock}

	6. Configure el grupo ESP:  
		```
		set vpn ipsec esp-group bm-esp compression disable  
		set vpn ipsec esp-group bm-esp lifetime 3600  
		set vpn ipsec esp-group bm-esp mode tunnel  
		set vpn ipsec esp-group bm-esp pfs dh-group2  
		set vpn ipsec esp-group bm-esp proposal 2 encryption aes128  
		set vpn ipsec esp-group bm-esp proposal 2 hash sha1  
		```  
		{: codeblock}

	7. Establezca la conexión con el sitio remoto:   
		```
		set vpn ipsec site-to-site peer 129.41.255.27 authentication id 173.192.83.82  
		set vpn ipsec site-to-site peer 129.41.255.27 authentication remote-id 129.41.255.27  
		set vpn ipsec site-to-site peer 129.41.255.27 authentication mode pre-shared-secret  
		set vpn ipsec site-to-site peer 129.41.255.27 authentication pre-shared-secret 567890  
		set vpn ipsec site-to-site peer 129.41.255.27 connection-type response  
		set vpn ipsec site-to-site peer 129.41.255.27 default-esp-group bm-esp  
		set vpn ipsec site-to-site peer 129.41.255.27 ike-group bm-ike  
		set vpn ipsec site-to-site peer 129.41.255.27 local-address any  
		set vpn ipsec site-to-site peer 129.41.255.27 tunnel 1 local prefix 192.168.201.0/24  
		set vpn ipsec site-to-site peer 129.41.255.27 tunnel 1 remote prefix 172.31.0.0/16  
		```
		{: codeblock}

		```
		Donde:  
			129.41.255.27 es la pasarela IBM;  
			172.31.0.0/16 es el subred de contenedor detrás de la pasarela IBM.
		```
		{: screen}

	8. Comprometa y confirme la configuración:  
		```  
		vyatta@vpn# show vpn  
		```
		{: codeblock}

		```
		 ipsec {
		     esp-group bm-esp {
		         compression disable
		         lifetime 3600
		         mode tunnel
		         pfs dh-group2
		         proposal 2 {
		             encryption aes128
		             hash sha1
		         }
		     }
		     ike-group bm-ike {
		         lifetime 28800
		         proposal 1 {
		             dh-group 2
		             encryption aes128
		             hash sha1
		         }
		     }
		     ipsec-interfaces {
		         interface bond1
		     }
		     nat-networks {
		     }
		     site-to-site {
		         peer 129.41.255.27 {
		             authentication {
		                 id 173.192.83.82
		                 mode pre-shared-secret
		                 pre-shared-secret 567890
		                 remote-id 129.41.255.27
		             }
		             connection-type initiate
		             default-esp-group bm-esp
		             ike-group bm-ike
		             local-address any
		             tunnel 1 {
		                 local {
		                     prefix 192.168.201.0/24
		                 }
		                 remote {
		                     prefix 172.31.0.0/16
		                 }
		             }
		         }
		     }
		 }
		[edit]
		```
		{: screen}

		```
		vyatta@vpn# commit
		vyatta@vpn# confirm   
		```
		{: codeblock}

	9. Verifique la configuración:  
		```
		vyatta@vpn:~$ show vpn  ipsec status  
		```
		{: codeblock}

		```
		IPSec Process Running PID: 5633  
		  
		1 Active IPsec Tunnels  
		  
		Interfaces IPsec :  
		        bond1   (no IP on interface statically configured as local-ip for any VPN peer)  
		```
		{: screen}

		```
		vyatta@vpn:~$ show vpn  ipsec policy  
		```
		{: codeblock}

		```
		src 192.168.201.0/24 dst 172.31.0.0/16   
		        dir out priority 1891 ptype main  
		        tmpl src 173.192.83.82 dst 129.41.255.27  
		                proto esp reqid 16384 mode tunnel  
		src 172.31.0.0/16 dst 192.168.201.0/24  
		        dir fwd priority 1891 ptype main  
		        tmpl src 129.41.255.27 dst 173.192.83.82  
			                proto esp reqid 16384 mode tunnel  
		src 172.31.0.0/16 dst 192.168.201.0/24  
		        dir in priority 1891 ptype main   
		        tmpl src 129.41.255.27 dst 173.192.83.82  
		                proto esp reqid 16384 mode tunnel  
		src ::/0 dst ::/0  
		        socket out priority 0 ptype main  
		src ::/0 dst ::/0  
		        socket in priority 0 ptype main  
		src ::/0 dst ::/0  
		        socket out priority 0 ptype main  
		src ::/0 dst ::/0  
		        socket in priority 0 ptype main  
		src 0.0.0.0/0 dst 0.0.0.0/0  
		        socket out priority 0 ptype main  
		src 0.0.0.0/0 dst 0.0.0.0/0  
		        socket in priority 0 ptype main  
		src 0.0.0.0/0 dst 0.0.0.0/0  
		        socket out priority 0 ptype main  
		src 0.0.0.0/0 dst 0.0.0.0/0  
		        socket in priority 0 ptype main  
		src 0.0.0.0/0 dst 0.0.0.0/0  
		        socket out priority 0 ptype main  
		src 0.0.0.0/0 dst 0.0.0.0/0  
		        socket in priority 0 ptype main  
		src 0.0.0.0/0 dst 0.0.0.0/0  
		        socket out priority 0 ptype main  
		src 0.0.0.0/0 dst 0.0.0.0/0  
		        socket in priority 0 ptype main  
		src 0.0.0.0/0 dst 0.0.0.0/0  
		        socket out priority 0 ptype main  
		src 0.0.0.0/0 dst 0.0.0.0/0  
		        socket in priority 0 ptype main  
		src 0.0.0.0/0 dst 0.0.0.0/0  
		        socket out priority 0 ptype main  
		src 0.0.0.0/0 dst 0.0.0.0/0  
		        socket in priority 0 ptype main  
		src 0.0.0.0/0 dst 0.0.0.0/0  
		        socket out priority 0 ptype main  
		src 0.0.0.0/0 dst 0.0.0.0/0  
		        socket in priority 0 ptype main   
		vyatta@vpn:~$   
		```
		{: screen}

		```
		vyatta@vpn:~$ show vpn ipsec sa   
		```
		{: codeblock}

		```
		Peer ID / IP							Local ID / IP               
		------------  							-------------
		129.41.255.27                           173.192.83.82                          
		  
		Tunnel  State  Bytes Out/In   Encrypt  Hash  NAT-T  A-Time  L-Time  Proto
		------  -----  -------------  -------  ----  -----  ------  ------  -----
		1       up     0.0/0.0        aes128   sha1  no     1359    3600    all  
		```  
		{: screen}

	10. Compruebe el estado de conexión de servicio IBM VPN:

		Verifique el estado de conexión IPSec de IBM VPN en el panel de control del servicio de IBM Bluemix. En la sección **Conexiones de sitios VPN**, el campo de estado debería mostrarse como **ACTIVO**.

	11. Compruebe el syslog de Vyatta, si es necesario:
		
		```
		vyatta@vpn# run show log vpn ipsec 
		```
		{: codeblock}

		```
		Nov 19 00:26:07 vpn pluto[5876]: failed to load pkcs11 module '/usr/lib/opensc-pkcs11.so'
		Nov 19 00:26:07 vpn pluto[5876]: including NAT-Traversal patch (Version 0.6c) [disabled]
		Nov 19 00:26:07 vpn pluto[5876]: loaded plugins: test-vectors curl ldap aes des sha1 sha2 md5 random x509 pkcs1 pgp dnskey pem openssl gmp hmac xauth attr kernel-netlink resolve 
		Nov 19 00:26:07 vpn pluto[5876]: fe80::200:5eff:fe00:101
		Nov 19 00:26:07 vpn pluto[5876]: 10.41.203.130
		Nov 19 00:26:07 vpn pluto[5876]: bond0v1
		Nov 19 00:26:07 vpn pluto[5876]: fe80::200:5eff:fe00:101
		Nov 19 00:26:07 vpn pluto[5876]: 173.192.83.86
		```
		{: screen}  

##Configuración del servicio IBM VPN con el servicio GaaS (SoftLayer Gateway Appliance Service)
{: #gaas} 

La configuración de IBM VPN utiliza la siguiente configuración de ejemplo:

* Subred de contenedores individuales: 172.31.0.0/16
* Subred de grupos de contenedores: 172.30.0.0/16
* Dirección IP de pasarela IBM VPN: 134.168.0.244

La configuración de SoftLayer GaaS local utiliza la siguiente configuración de ejemplo:

* Dirección IP de pasarela VPN (IP de pasarela de cliente): 75.126.122.46
* Dirección de subred a la que están conectados los puntos finales (subred de cliente): 10.86.88.128/26
* Serie de clave compartida previamente: 567890 

###Para utilizar el servicio IBM VPN con SoftLayer GaaS, configure lo siguiente:

1. Configure SoftLayer GaaS:

	1. Abra [https://gateway-as-a-service.com/gaas/ui/](https://gateway-as-a-service.com/gaas/ui/).  
	2. Inicie la sesión utilizando las credenciales de cuenta de SoftLayer. Se visualiza la página **Gestionar pasarelas**. 
	3. Seleccione la acción **Gestionar túneles** para la pasarela que desea configurar. Se visualiza la página **Gestionar configuración de túnel de pasarela**. 
	4. Seleccione **Añadir túnel**. La página subsiguiente requiere detalles de pasarela y red. 
	5. No cambie la configuración predeterminada de la pasarela y la red. Seleccione **Siguiente**.
	6. Establezca **Tipo de VLAN** en privada para la subred local. Seleccione **Siguiente**.  
	7. Edite los detalles de configuración de red como se indica a continuación:  
		* Dirección IP pública en pasarela local: escriba la dirección IP pública de pasarela IBM VPN.  
		* Subred local: especifique la subred de pasarela IBM VPN.  
		* Suprima la dirección de subred de túnel GRE.   
		* Seleccione **Configuración IPSec avanzada**. Configúrela de la forma siguiente:  
			* Cifrado de IPSec: aes-128  
			* Grupo Diffie-Hellman: 2  
			* ESP - Perfect Forward Security: Habilitar  
			* Clave secreta compatida previamente: especifique la clave secreta compartida previamente que ha utilizado al configurar IBM VPN.  
		* Seleccione **Siguiente**.
	8. Seleccione la zona de cortafuegos y la opción **Configuración avanzada del cortafuegos**. Seleccione **Siguiente**.  
	9. Marque el recuadro de selección para indicar que está de acuerdo en sobrescribir la configuración de la pasarela.
	10. Seleccione **Siguiente**.  
	11. Seleccione **Finalizar**. Se visualiza la página **Ver solicitudes pendientes**.   
	12. Seleccione el botón **Detalles** para ver el estado de solicitud. Se visualiza la página **Ver detalles de solicitud**. 
	13. Espere a que el estado de todos los parámetros de configuración se visualicen como completo.  
2. [Configure la pasarela](index.html#gateway).
3. [Configure la conexión de sitio](index.html#site).
4. Verifique la configuración.
	1. Ejecute el siguiente mandato en Vyatta para verificar el estado de la conexión IPSec:  
		```
		vyatta@gateway# run show vpn ipsec sa
		```
		{: codeblock}

		```
		Peer ID / IP                            Local ID / IP               
		------------                            -------------
		134.168.0.224                           75.126.122.46                          
		
		    Tunnel  State  Bytes Out/In   Encrypt  Hash  NAT-T  A-Time  L-Time  Proto
		    ------  -----  -------------  -------  ----  -----  ------  ------  -----
		    1       up     0.0/0.0        aes128   sha1  yes    978     3600    all
		    2       up     0.0/0.0        aes128   sha1  yes    768     3600    all

		[edit]
		```
		{: screen}

		```
		vyatta@gateway# run show vpn ipsec policy 
		```
		{: codeblock}

		```
		src 10.86.88.128/26 dst 172.31.0.0/16 
		        dir out priority 1883 ptype main 
		        tmpl src 75.126.122.46 dst 134.168.0.224
		                proto esp reqid 16384 mode tunnel
		src 172.31.0.0/16 dst 10.86.88.128/26 
		        dir fwd priority 1883 ptype main 
		        tmpl src 134.168.0.224 dst 75.126.122.46
		                proto esp reqid 16384 mode tunnel
		src 172.31.0.0/16 dst 10.86.88.128/26 
		        dir in priority 1883 ptype main 
		        tmpl src 134.168.0.224 dst 75.126.122.46
		                proto esp reqid 16384 mode tunnel
		src 10.86.88.128/26 dst 172.30.0.0/16 
		        dir out priority 1883 ptype main 
		        tmpl src 75.126.122.46 dst 134.168.0.224
		                proto esp reqid 16388 mode tunnel
		src 172.30.0.0/16 dst 10.86.88.128/26 
		        dir fwd priority 1883 ptype main 
		        tmpl src 134.168.0.224 dst 75.126.122.46
		                proto esp reqid 16388 mode tunnel
		src 172.30.0.0/16 dst 10.86.88.128/26 
		        dir in priority 1883 ptype main 
		        tmpl src 134.168.0.224 dst 75.126.122.46
		                proto esp reqid 16388 mode tunnel
		src ::/0 dst ::/0 
		        socket out priority 0 ptype main 
		src ::/0 dst ::/0 
		        socket in priority 0 ptype main 
		src ::/0 dst ::/0 
		        socket out priority 0 ptype main 
		src ::/0 dst ::/0 
		        socket in priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket out priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket in priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket out priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket in priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket out priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket in priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket out priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket in priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket out priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket in priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket out priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket in priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket out priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket in priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket out priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket in priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket out priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket in priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket out priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket in priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket out priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket in priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0 
		        socket out priority 0 ptype main 
		src 0.0.0.0/0 dst 0.0.0.0/0
		        socket in priority 0 ptype main
		src ::/0 dst ::/0
		        socket in priority 0 ptype main
		src ::/0 dst ::/0
		        socket out priority 0 ptype main
		src ::/0 dst ::/0
		        socket in priority 0 ptype main
		src ::/0 dst ::/0
		        socket out priority 0 ptype main
		src ::/0 dst ::/0
		        socket in priority 0 ptype main
		src ::/0 dst ::/0
		        socket out priority 0 ptype main
		src 0.0.0.0/0 dst 0.0.0.0/0
		        socket in priority 0 ptype main
		src 0.0.0.0/0 dst 0.0.0.0/0
 	        socket out priority 0 ptype main
		src 0.0.0.0/0 dst 0.0.0.0/0
		        socket in priority 0 ptype main
		src 0.0.0.0/0 dst 0.0.0.0/0
		        socket out priority 0 ptype main
		src 0.0.0.0/0 dst 0.0.0.0/0
		        socket in priority 0 ptype main
		src 0.0.0.0/0 dst 0.0.0.0/0
		        socket out priority 0 ptype main
		```
		{: screen}

		```
		vyatta@gateway# run ping 172.31.0.1 interface 10.86.88.129
		```
		{: codeblock}

		```
		PING 172.31.0.1 (172.31.0.1) from 10.86.88.129 : 56(84) bytes of data.
		64 bytes from 172.31.0.1: icmp_req=1 ttl=64 time=1.99 ms
		64 bytes from 172.31.0.1: icmp_req=2 ttl=64 time=1.79 ms
		^C
		--- 172.31.0.1 ping statistics ---
		2 packets transmitted, 2 received, 0% packet loss, time 1001ms
		rtt min/avg/max/mdev = 1.794/1.896/1.998/0.102 ms
		```
		{: screen}

	2. Verifique el estado de conexión IPSec de IBM VPN en el panel de control del servicio de IBM Bluemix. En la sección **Conexiones de sitios VPN**, el campo de estado debería mostrarse como **ACTIVO**.  
5. Compruebe el syslog de Vyatta, si es necesario:  

	```
	vyatta@gateway# tail -f /var/log/messages 
	```
	{: codeblock}

	```
	Dec  4 08:03:31 gateway pluto[24560]:  "peer-134.168.0.224-tunnel-1" #1: Peer ID is ID_IPV4_ADDR: '134.168.0.224'
	Dec  4 08:03:31 gateway pluto[24560]:  "peer-134.168.0.224-tunnel-1" #1: ISAKMP SA established
	Dec  4 08:03:31 gateway pluto[24560]:  "peer-134.168.0.224-tunnel-2" #5: initiating Quick Mode PSK+ENCRYPT+TUNNEL+PFS+UP {using isakmp#1}
	Dec  4 08:03:31 gateway pluto[24560]:  "peer-134.168.0.224-tunnel-1" #6: initiating Quick Mode PSK+ENCRYPT+TUNNEL+PFS+UP {using isakmp#1}
	Dec  4 08:03:31 gateway pluto[24560]:  "peer-134.168.0.224-tunnel-2" #5: sent QI2, IPsec SA established {ESP=>0x03d9db46 <0xcb02ea03 NATOA=0.0.0.0}
	Dec  4 08:03:31 gateway pluto[24560]:  "peer-134.168.0.224-tunnel-1" #6: sent QI2, IPsec SA established {ESP=>0x21605ff5 <0xc69ae517 NATOA=0.0.0.0}
	Dec  4 08:03:33 gateway Keepalived_vrrp: Warning: Failed to connect to the agentx master agent ([NIL]):
	Dec  4 08:04:34 gateway Keepalived_vrrp: last message repeated 9 times
	Dec  4 08:05:34 gateway Keepalived_vrrp: last message repeated 8 times
	Dec  4 08:06:34 gateway Keepalived_vrrp: last message repeated 8 times
	```
	{: screen}

##Configuración del servicio IBM VPN con Cisco ASA
{: #cisco}

La configuración de IBM VPN utiliza la siguiente configuración de ejemplo:

* Subred de contenedores individuales: 172.31.0.0/16
* Subred de grupos de contenedores: 172.30.0.0/16
* Dirección IP de pasarela IBM VPN: 134.168.6.5

La configuración local utiliza la siguiente configuración de ejemplo:

* Dirección IP de pasarela VPN (IP de pasarela de cliente): 62.95.35.53
* Dirección de subred a la que están conectados los puntos finales (subred de cliente): 10.2.0.0/16

###Para utilizar el servicio IBM VPN con Cisco ASA, configure lo siguiente:

1. [Configure la pasarela](index.html#gateway).
2. [Configure la conexión de sitio](index.html#site).
3. Configure Cisco ASA. Consulte el siguiente ejemplo de configuración.
		
		object network 10.2-network 
		 subnet 10.2.0.0 255.255.0.0
		http 10.2.0.0 255.255.0.0 inside
		ssh 10.2.0.0 255.255.0.0 inside
		
		interface Ethernet0/0
		 nameif outside
		 security-level 0
		 ip address 62.95.35.53 255.255.255.248 
		
		object network A_62.95.35.53 
		 host 62.95.35.53
		
		access-list out-in extended permit gre any host 62.95.35.53 
		access-list out-in extended permit tcp any host 62.95.35.53 eq pptp 
		access-list outside_1_cryptomap extended permit ip object 10.2-network 
		object network NETWORK_OBJ_172.31.0.0_16 
		 subnet 172.31.0.0 255.255.0.0
		object network Bluemix31 
		 subnet 172.31.0.0 255.255.0.0
		 description Bluemix 172.31.0.0 VPN 
		
		nat (inside,outside) source static 10.2-network 10.2-network destination static NETWORK_OBJ_172.31.0.0_16 NETWORK_OBJ_172.31.0.0_16
		nat (outside,inside) source static NETWORK_OBJ_172.31.0.0_16 NETWORK_OBJ_172.31.0.0_16 destination static 10.2-network 10.2-network
		
		crypto ipsec transform-set ESP-AES-256-MD5 esp-aes-256 esp-md5-hmac 
		crypto ipsec security-association lifetime seconds 28800
		crypto ipsec security-association lifetime kilobytes 4608000
		crypto map outside_map0 1 set transform-set ESP-AES-128-SHA
		crypto map outside_map 1 match address outside_1_cryptomap
		crypto map outside_map 1 set pfs group5
		crypto map outside_map 1 set peer 134.168.6.5 
		crypto map outside_map 1 set transform-set ESP-AES-128-SHA
		crypto map outside_map 1 set nat-t-disable
		crypto map outside_map interface outside
		crypto isakmp identity address
		crypto isakmp enable outside
		crypto isakmp policy 1
		 authentication pre-share
		 encryption aes
		 hash sha
		 group 1
		 lifetime 86400
		
		group-policy IPsec internal
		group-policy IPsec attributes
		 vpn-tunnel-protocol IPSec l2tp-ipsec 
		
		tunnel-group 134.168.6.5 type ipsec-l2l
		tunnel-group 134.168.6.5 general-attributes
		 default-group-policy IPsec
		tunnel-group 134.168.6.5 ipsec-attributes
		 pre-shared-key bluemix

