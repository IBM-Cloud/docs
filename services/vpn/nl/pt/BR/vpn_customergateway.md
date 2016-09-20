---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configurando o gateway em seu datacenter ou servidor SoftLayer
{: #vpn_yourdatacenter}
*Última atualização: 17 de março de 2016*

É necessário um gateway IPSec VPN em seu datacenter ou servidor SoftLayer para formar uma conexão segura com o serviço {{site.data.keyword.vpn_short}}. As configurações de gateway VPN a seguir são necessárias em seu datacenter ou servidor SoftLayer:

* Ative a passagem de Conversão de Endereço de Rede (NAT) no gateway VPN somente se ele estiver atrás de NAT. 
* Use a mesma chave pré-compartilhada que você usou ao configurar o serviço IBM VPN.
* Inclua a sub-rede a seguir como a sub-rede remota:
	* Se você criou contêineres únicos no espaço do IBM Bluemix, inclua 172.31.0.0/16.
	* Se você criou grupos de contêineres no espaço do IBM Bluemix, inclua 172.30.0.0/16.
	* Se você criou contêineres únicos e grupos de contêineres no espaço do IBM Bluemix, inclua 172.31.0.0/16 e 172.30.0.0/16.
* Assegure-se de que as configurações de criptografia, autenticação e grupo PFS sejam as mesmas no gateway IBM VPN e em seu gateway VPN.
