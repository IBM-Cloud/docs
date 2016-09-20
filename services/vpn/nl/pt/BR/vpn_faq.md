---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Perguntas mais frequentes do {{site.data.keyword.vpn_short}}
{: #vpn_faq}
*Última atualização: 17 de março de 2016*

A seguir estão algumas perguntas mais frequentes.
{:shortdesc}

1. Quais dispositivos de fornecedores de terceiros estão qualificados em laboratórios IBM para interoperabilidade com o serviço IBM VPN?

	O laboratório IBM testou os dispositivos de gateway VPN a seguir para interoperação com o serviço IBM VPN:

	* Cisco Adaptive Security Appliance (ASA) Software Version 8.2(1). [Veja o exemplo de configuração](vpn_onpremises.html#cisco) 
	* Brocade Vyatta 5415 vRouter 6.7 R7. [Veja o exemplo de configuração](vpn_onpremises.html#vyatta){: new_window}
	* Linux StrongSwan U5.1.2/K3.13.0-55-generic. [Veja o exemplo de configuração](vpn_onpremises.html#strongswan){: new_window}
	* Linux StrongSwan U5.2.2/K3.13.0-55-generic. [Veja o exemplo de configuração](vpn_onpremises.html#strongswan){: new_window}

	Além disso, um dispositivo de gateway VPN compatível com as normas do IPSec de qualquer outro fornecedor deve funcionar bem com o serviço IBM VPN.

2. Em quanto tempo uma falha de peer será detectada?
 
	Um peer com falha é detectado no valor de tempo limite de keep-alive configurado. A definição padrão é 60 segundos.

3. Quantos gateways e conexões VPN posso criar por serviço VPN?
 
	É possível criar um dispositivo de gateway VPN por serviço VPN em um espaço do Bluemix. É possível definir até 16 conexões para diferentes destinos por gateway VPN. 

4. Quando devo usar o serviço IBM VPN versus o serviço Bluemix Secure Gateway?

	Ambos os serviços são usados para fornecer conectividade segura entre os recursos do Bluemix e seu datacenter no local. 

	Use o serviço IBM VPN quando você estiver procurando assegurar a conectividade entre quaisquer dois terminais. O serviço VPN forma uma conexão IPSec de Camada 3 segura entre as redes no local e o ambiente de nuvem IBM Bluemix. O serviço IBM VPN está disponível para acessar seguramente somente contêineres IBM (contêineres Docker). 

	Use o serviço Bluemix Secure Gateway se desejar estabelecer uma conexão segura de um terminal de aplicativo específico no Bluemix com outro terminal dentro de seu datacenter no local. 

5. Posso usar o serviço IBM VPN para acessar meus contêineres e servidores virtuais dentro do ambiente de nuvem IBM Bluemix usando seus endereços IP privados?
 
	Atualmente, o serviço IBM VPN está disponível para acessar somente contêineres Bluemix.

6. Posso definir o serviço IBM VPN no nível de organização do Bluemix?

	Atualmente, o serviço IBM VPN está disponível somente no nível de espaço do Bluemix. Se a sua organização do Bluemix tiver vários espaços, um serviço VPN separado poderá ser definido para cada espaço.

7. Como conectar o serviço IBM VPN ao SoftLayer Gateway Appliance Service (GaaS)?

	É possível construir um túnel IPSec para estabelecer uma comunicação segura entre o serviço IBM VPN e o SoftLayer GaaS. [Veja o exemplo de configuração.](vpn_onpremises.html#gaas){: new_window}
