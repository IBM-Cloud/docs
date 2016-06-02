---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# IBM VPN CLI
*Última atualização: 03 de maio de 2016*

É possível usar a interface da linha de comandos (CLI) para configurar e gerenciar o serviço IBM® Virtual Private Network (VPN). O IBM VPN CLI é um plug-in usado com o plug-in Cloud Foundry CLI. O plug-in está disponível para os sistemas operacionais Windows, MAC e Linux. Assegure-se de usar aquele que for aplicável a você.

Antes de iniciar, instale o Cloud Foundry CLI. Veja [Interface da linha de comandos do Cloud Foundry](https://console.{DomainName}/docs/cli/downloads.html) para obter detalhes. 

##Instalar o plug-in IBM VPN CLI
**Nota:** se você tiver uma versão anterior do plug-in IBM VPN CLI que esteja instalada, deverá desinstalá-la primeiramente. Utilize o comando: 

```
cf uninstall-plugin vpn
```  

**Instalar localmente**

1. Faça download do plug-in IBM VPN para a sua plataforma a partir de [Repositório de plug-in do IBM Bluemix CLI](http://plugins.ng.bluemix.net).
2. Instale o plug-in IBM VPN usando o comando a seguir:
**Nota:** alterne para o local do plug-in VPN ou especifique o caminho para o local do plug-in.  

	**Para o sistema operacional MS Windows:**

	```
	cf install-plugin vpn_windows64.exe
	```  

	**Para o sistema operacional Apple MAC:**

	```
	cf install-plugin vpn_mac_os_amd64
	```  

	**Para o sistema operacional Linux:**

	```
	cf install-plugin vpn_linuxamd64
	```  


**Instalar a partir do Repositório do Bluemix**  

1. Inclua o repositório do Bluemix nos repositórios do Cloud Foundry CLI. Utilize o comando a seguir:

	```
	cf add-plugin-repo bluemix http://plugins.ng.bluemix.net
	```  
2. Execute o seguinte comando:  

	```
	cf install-plugin vpn -r bluemix
	```
##Lista de comandos do serviço IBM VPN

### cf vpn-create connection

Cria uma conexão VPN.

```
cf vpn-create connection <connection name> -g <gateway name> -k <preshared key> -subnets ["<subnet/mask>"] -cip <customer gateway IP address> -d <description> -peer_id <peer ID> -admin_state <admin state> -dpd-action <action> -gateway_ip <IP address> -i <initiator state> -dpd-timeout <value> -dpd-interval <value> -ike <name> -ipsec <name>
```
#### Parameters
{: #p1}

**connection name:**
Nome da conexão.

**gateway name:**
Nome do gateway.

**-k:**
Chave pré-compartilhada.

**subnet/mask:**
Endereço de sub-rede remoto no formato CIDR. 

**customer gateway IP address:**
Endereço IP do terminal remoto do túnel VPN. 

##### Parâmetros opcionais:
{: #op1}

**-d:** Descrição dos parâmetros especificados.

**-peer_id:** ID do peer remoto. Outro terminal do túnel VPN.

**-admin_state:** Status da conexão VPN. Valores: UP ou DOWN.

**-dpd-action:** Ação a ser tomada quando o peer for detectado como inativo. Valores: hold; clear; disabled; restart; restart-by-peer. Valor padrão: hold

**-gateway_ip:** Endereço IP do terminal de túnel VPN local. 

**-i:** Estado do inicializador. Valor padrão: bi-directional.

**-dpd-timeout:** Valor de tempo limite, em segundos, após o qual a sessão é finalizada.  Intervalo: 6 a 86400 segundos. Valor padrão: 120 segundos. O valor de tempo limite de keep-alive deve ser maior que o valor do intervalo keep-alive.

**-dpd-interval:** Intervalo keep-alive em segundos. Envie mensagens keep-alive no intervalo configurado para verificar se o peer está ativo. Intervalo: 5 a 86399 segundos. Valor padrão: 15 segundos

**-ike:** Nome da política IKE.

**-ipsec:** Nome da política IPSec.


### cf vpn-create ike

Cria uma política IKE.

```
cf vpn-create ike <policy name> -g <gateway name> -d <description> -pfs <group> -e <encryption algorithm> -lv <lifetime value>
```
#### Parameters
{: #p2}

**policy name:**
Nome da política IKE.

**gateway name:**
Nome do gateway. 

##### Parâmetros opcionais:
{: #op2}

**-d:** Descrição dos parâmetros especificados.

**-pfs:** Identificador de grupo do Diffie-Hellman (DH). Valores: Group2; Group5; Group14. Valor padrão: Group2 

**-e:** Algoritmo de criptografia. Valores: aes-128; aes-192; aes-256; 3des. Valor padrão: aes-128

**-lv:** Valor de tempo de vida da associação de segurança do IKE. Intervalo: 60 a 86400 segundos. Valor padrão: 86400 segundos


### cf vpn-create ipsec

Cria uma política IPSec.

```
cf vpn-create ipsec <policy name> -g <gateway name> -d <description> -pfs <group> -e <encryption algorithm> -lv <lifetime value>
```
#### Parameters
{: #p3}

**policy name:**
Nome da política IPSec. 

**gateway name:**
Nome do gateway. 

##### Parâmetros opcionais:
{: #op3}

**-d:** Descrição dos parâmetros especificados.

**-pfs:** Identificador de grupo do Diffie-Hellman (DH). Valores: Group2; Group5; Group14. Valor padrão: Group2  

**-e:** Algoritmo de criptografia. Valores: aes-128; aes-192; aes-256; 3des. Valor padrão: aes-128

**-lv:** Valor de tempo de vida da associação de segurança. Intervalo: 60 a 86400 segundos. Valor padrão: 3600 segundos

### cf vpn-create gateway

Cria um gateway VPN.

```
cf vpn-create gateway <gateway name> -t <type> -gateway_ip <IP address> -subnets <subnet address>
```
#### Parameters
{: #p4}

**gateway name:**
Nome do gateway.

**-t:** Contêineres para os quais você deseja ativar o serviço. Valores: allSingleContainers; allContainerGroups; allContainers. Valor padrão: nenhum valor padrão; deve-se especificar um tipo. 

#####Parâmetros opcionais:
{: #op4}

**-gateway_ip:**
Endereço IP do gateway. 

**-subnets:**
Endereço de sub-rede no formato CIDR. 

### cf vpn-show gateways

Exibe informações sobre os gateways atuais.

```
cf vpn-show gateways
```
### cf vpn-show ikes

Exibe informações sobre as conexões IKE atuais.

```
cf vpn-show ikes
```
### cf vpn-show ipsecs

Exibe informações sobre as conexões IPSec atuais.

```
cf vpn-show ipsecs
```
### cf vpn-show connections

Exibe informações sobre todas as conexões atuais.

```
cf vpn-show connections
```
### cf vpn-show ike

Exibe informações sobre uma conexão IKE.

```
cf vpn-show ike <policy name>
```
### cf vpn-show ipsec

Exibe informações sobre uma conexão IPSec.

```
cf vpn-show ipsec <policy name>
```
### cf vpn-show gateway

Exibe informações de conexão de um gateway.

```
cf vpn-show gateway <gateway name>
```
### cf vpn-show connection

Exibe todas as informações sobre uma determinada conexão.

```
cf vpn-show connection <connection name>
```
### cf vpn-delete

Exclui uma conexão, política ou gateway existente.

```
cf vpn-delete ike <policy name>
```

```
cf vpn-delete ipsec <policy name>
```

```
cf vpn-delete connection <connection name>
```

```
cf vpn-delete gateway <gateway name>
```


### cf vpn-update connection

Atualiza uma conexão VPN existente.

```
cf vpn-update connection <connection name> -g <gateway name> -cip <customer gateway IP address> -subnets ["<subnet/mask>"] -k <preshared key> -d <description> -peer_id <peer ID> -admin_state <admin state> -dpd-action <action> -gateway_ip <IP address> -i <initiator state> -dpd-timeout <value> -dpd-interval <value> -ike <name> -ipsec <name>
```
#### Parameters
{: #p5}

**connection name:**
Nome da conexão.


##### Parâmetros opcionais:
{: #op5}

**gateway name:**
Nome do gateway.

**customer gateway IP address:**
Endereço IP do terminal remoto do túnel VPN. 

**subnet/mask:**
Endereço de sub-rede no formato CIDR. 

**-k:**
Chave pré-compartilhada.

**-d:** Descrição dos parâmetros especificados.

**-peer_id:** ID do peer remoto. Outro terminal do túnel VPN.

**-admin_state:** Status da conexão VPN. Valores: UP ou DOWN.

**-dpd-action:** Ação a ser tomada quando o peer for detectado como inativo. Valores: hold; clear; disabled; restart; restart-by-peer. Valor padrão: hold

**-gateway_ip:** Endereço IP do terminal de túnel VPN local. 

**-i:** Estado do inicializador. Valor padrão: bi-directional.

**-dpd-timeout:** Valor de tempo limite, em segundos, após o qual a sessão é finalizada. Intervalo: 6 a 86400 segundos. Valor padrão:
120 segundos

**-dpd-interval:** Intervalo keep-alive em segundos. Envie mensagens keep-alive no intervalo configurado para verificar se o peer está ativo. Intervalo: 5 a 86399 segundos. Valor padrão: 15 segundos

**-ike:** Nome da política IKE.

**-ipsec:** Nome da política IPSec.


### cf vpn-update ike

Atualiza uma política IKE.

```
cf vpn-update ike <policy name> -g <gateway name> -d <description> -pfs <group> -e <encryption algorithm> -lv <lifetime value>
```
#### Parameters
{: #p6}

**policy name:**
Nome da política IKE. 

##### Parâmetros opcionais:
{: #op6}

**gateway name:** Nome do gateway. 

**-d:** Descrição dos parâmetros especificados.

**-pfs:** Identificador de grupo do Diffie-Hellman (DH). Valores: Group2; Group5; Group14. Valor padrão: Group2 

**-e:** Algoritmo de criptografia. Valores: aes-128; aes-192; aes-256; 3des. Valor padrão: aes-128

**-lv:** Valor de tempo de vida da associação de segurança do IKE. Intervalo: 60 a 86400 segundos. Valor padrão: 86400 segundos


### cf vpn-update ipsec

Atualiza uma política IPSec.

```
cf vpn-update ipsec <policy name> -g <gateway name> -d <description> -pfs <group> -e <encryption algorithm> -lv <lifetime value>
```
#### Parameters
{: #p7}

**policy name:**
Nome da política IPSec.


##### Parâmetros opcionais:
{: #op7}

**gateway name:**
Nome do gateway.

**-d:** Descrição dos parâmetros especificados.

**-pfs:** Identificador de grupo do Diffie-Hellman (DH). Valores: Group2; Group5; Group14. Valor padrão: Group2 

**-e:** Algoritmo de criptografia. Valores: aes-128; aes-192; aes-256; 3des. Valor padrão: aes-128

**-lv:** Valor de tempo de vida da associação de segurança. Intervalo: 60 a 86400 segundos. Valor padrão: 3600 segundos

### cf vpn-update gateway

Atualiza um gateway VPN existente.

```
cf vpn-update gateway <gateway name> -t <type> -gateway_ip <IP address> -subnets <subnet address>
```
#### Parameters
{: #p8}

**gateway name:**
Nome do gateway.

#####Parâmetros opcionais:
{: #op8}

**-t:** Contêineres para os quais você deseja ativar o serviço. Valores: allSingleContainers; allContainerGroups; allContainers. Valor padrão: nenhum valor padrão; deve-se especificar um tipo.

**-gateway_ip:**
Endereço IP do gateway. 

**-subnets:**
Endereço de sub-rede no formato CIDR. 

# rellinks
## gerais  
{: #general}  
* [Serviço IBM VPN](../../../services/vpn/index.html)
* [Cloud Foundry CLI ](https://console.{DomainName}/docs/cli/downloads.html){: new_window}
