---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Sobre {{site.data.keyword.vpn_short}}
{: #vpn_overview}  
*Última atualização: 17 de março de 2016*

O serviço {{site.data.keyword.vpn_full}} (VPN) fornece um canal de comunicação segura entre o datacenter corporativo e os recursos no ambiente de nuvem IBM Bluemix&reg;. A conexão é estabelecida por meio da Internet.
{:shortdesc}

O serviço {{site.data.keyword.vpn_short}} fornece os recursos a seguir:  
##Privacidade 
O serviço IBM VPN usa o conjunto de protocolo padrão de mercado Internet Protocol Security (IPSec) para autenticar e criptografar a comunicação IP entre o datacenter corporativo e o ambiente de nuvem IBM Bluemix. O IPSec fornece autenticação de peer de nível de rede, integridade de dados e confidencialidade de dados (criptografia).

O serviço IBM VPN suporta os protocolos e conversões IPSec a seguir:

* Algoritmo de Autenticação:
	* HMAC-SHA1-96; o comprimento da chave compartilhada é 160 bits (padrão)  
* Algoritmo de Criptografia:
	* 3DES-CBC; o comprimento da chave compartilhada é 192 bits
	* AES-CBC; os comprimentos da chave compartilhada são 128 (padrão), 192, 256 bits
* Protocolos de autenticação e criptografia:
	* Os protocolos Authentication Header (AH) e Encapsulating Security Payload (ESP) são suportados. O AH é usado somente para autenticação. O ESP é usado para fornecer autenticação e criptografia.
* Grupos do IKEv1 Diffie-Hellman (DH) Key Exchange 2 (padrão), 5 e 14

O serviço IBM VPN suporta o modo de túnel IPSec. Neste modo, o IPSec protege o pacote IP original inteiro. O IPSec criptografa o pacote, que fica contido em um novo pacote IP, e encaminha o novo pacote para o peer IPSec. 

O serviço IBM VPN usa o Diffie-Hellman Key Exchange e a chave pré-compartilhada para assegurar a associação entre dois peers. A autenticação falhará se uma das partes não fornecer a chave pré-compartilhada. 
 
O serviço IBM VPN é compatível com as RFCs do IETF a seguir:

* RFCs 2407, 2408 e 2409 para IKEv1
* RFC 4301 para segurança IPv4   
* RFC 4302 para o cabeçalho de autenticação IPv4  
* RFC 4303 para o Encapsulating Security Payload (ESP) IPv4  
* RFC 2104 HMAC e RFC 2404 HMAC-SHA-1-96 para autenticação  
* RFC 2451 3DES-CBC; RFC 3602 AES128-CBC, AES192-CBC e AES256-CBC para criptografia
##Simplicidade
É possível criar o serviço IBM VPN usando uma interface gráfica simples e intuitiva. É possível especificar seu endereço IP do gateway e suas sub-redes do datacenter. É possível usar as políticas IPSec e IKE padrão ou customizar as políticas para adequar às suas necessidades.  
##Management
É possível gerenciar o serviço IBM VPN usando uma interface gráfica, um [interface da linha de comandos](../../cli/plugins/vpn/index.html) ou [APIs](https://new-console.ng.bluemix.net/apidocs/101).

