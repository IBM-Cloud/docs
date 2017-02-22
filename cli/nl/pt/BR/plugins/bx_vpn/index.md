---



copyright:

  years: 2015，2017

lastupdated: "2016-06-20"


---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.vpn_short}} plug-in para a CLI do {{site.data.keyword.Bluemix_notm}}

*Versão:* 1.4.0

É possível usar a interface da linha de comandos (CLI) para configurar e gerenciar o seu serviço do {{site.data.keyword.vpn_full}}. O plug-in da CLI do {{site.data.keyword.vpn_short}}
está disponível em duas versões: uma para uso com o plug-in da CLI do Cloud Foundry e a outra para uso com o plug-in da CLI do {{site.data.keyword.Bluemix}}. Ambas as versões do plug-in fornecem a
mesma funcionalidade.
{:shortdesc}

O plug-in do {{site.data.keyword.vpn_short}} está disponível para sistemas operacionais Windows, MAC e Linux. Assegure-se de usar aquele que for aplicável a você.

As instruções a seguir são para trabalhar com o plug-in da CLI do {{site.data.keyword.Bluemix_notm}}. Para usar o plug-in com o plug-in da CLI do Cloud Foundry (cf), consulte o plug-in da CLI do
[{{site.data.keyword.vpn_short}} para CLI cf](../vpn/index.html).


As informações a seguir listam todos os comandos que são suportados pelo plug-in do {{site.data.keyword.vpn_short}} para a Bluemix CLI e incluem seus nomes, opções, uso, pré-requisitos,
descrições e exemplos. Consulte [Estender a sua interface de linha de comandos do Bluemix](../../index.html#cli_bluemix_ext) sobre como instalar o plug-in de vpn.

**Nota:** *Pré-requisitos* listam quais ações são necessárias antes de usar o comando. Os pré-requisitos podem incluir uma ou mais das ações a seguir:
<dl>
<dt>**      Nó de Extremidade
**</dt>
<dd>Um terminal de API deve ser configurado por meio de `bluemix api` antes de usar o comando.</dd>
<dt>**Login**</dt>
<dd>É necessário efetuar login usando o comando `bluemix login` antes de usar esse comando.</dd>
<dt>**Destino **</dt>
<dd>O comando `bluemix target` deve ser usado para configurar uma organização e um espaço antes de usar esse comando.</dd>
</dl>


## bluemix vpn connection-create
Cria uma conexão VPN.

```
bluemix vpn connection-create CONNECTION_NAME -g GATEWAY_NAME -k PRESHARED_KEY -subnets "SUBNET/MASK" -cip CUSTOMER_GATEWAY_IP_ADDRESS [-d DESCRIPTION] [-peer_id PEER_ID] [-admin_state ADMIN_STATE] [-dpd-action ACTION] [-gateway_ip IP_ADDRESS] [-i INITIATOR_STATE] [-dpd-timeout VALUE] [-dpd-interval VALUE] [-ike NAME] [-ipsec NAME]
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

*CONNECTION_NAME* (obrigatório): nome da conexão.

-g *GATEWAY_NAME* (obrigatório): nome do gateway.

-k *PRESHARED_KEY* (obrigatório): chave pré-compartilhada.

-subnets "*SUBNET*/*MASK*" (obrigatório): endereço de sub-rede remota no formato CIDR.

-cip *CUSTOMER_GATEWAY_IP_ADDRESS* (obrigatório): endereço IP do terminal remoto do túnel da VPN.

-d *DESCRIPTION* (opcional): descrição dos parâmetros especificados.

-peer_id *PEER_ID* (opcional): ID do peer remoto. Outro terminal do túnel da VPN.

-admin_state *ADMIN_STATE* (opcional): status da conexão VPN. Um valor válido é `UP` ou `DOWN`.

-dpd-action *ACTION* (opcional): ação a ser executada quando o peer for detectado como inativo. Um valor válido é `hold`, `clear`, `disabled`, `restart` ou `restart-by-peer`. O valor padrão é `hold`.

-gateway_ip *IP_ADDRESS* (opcional): endereço IP do terminal de túnel da VPN local.

-i *INITIATOR_STATE* (opcional): estado do iniciador. O valor padrão é `bi-directional`.

-dpd-timeout *VALUE* (opcional): o valor de tempo limite em segundos após o qual a sessão é finalizada. Intervalo: 6 a 86400 segundos. O valor padrão é `120` segundos.

-dpd-interval *VALUE* (opcional): intervalo keep-alive em segundos. Envie mensagens keep-alive no intervalo configurado para verificar se o peer está ativo. Intervalo: 5 a 86399 segundos. O valor padrão é `15` segundos.

-ike *NAME* (opcional): nome da política IKE.

-ipsec *NAME* (opcional): nome da política IPSec.

**Exemplos**:

Crie uma nova conexão vpn com o nome `my_connection`:
```
bluemix vpn connection-create my_connection -g my_gateway -k 123456 -subnets "192.168.10.0/24" -cip 162.135.1.1
```


## bluemix vpn ike-create
Cria uma política IKE.

```
bluemix vpn ike-create POLICY_NAME -g GATEWAY_NAME [-d DESCRIPTION] [-pfs GROUP] [-e ENCRYPTION_ALGORITHM] [-lv LIFETIME_VALUE]
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

*POLICY_NAME* (obrigatório): nome da política IKE.

-g *GATEWAY_NAME* (obrigatório): nome do gateway.

-d *DESCRIPTION* (opcional): descrição dos parâmetros especificados.

-pfs *GROUP* (opcional): identificador de grupo Diffie-Hellman (DH). Um valor válido é `Group2`, `Group5` ou `Group14`. O valor padrão é `Group2`.

-e *ENCRYPTION_ALGORITHM* (opcional): algoritmo de criptografia. Um valor válido é `aes-128`, `aes-192`, `aes-256` ou `3des`. O valor padrão é `aes-128`.

-lv *LIFETIME_VALUE* (opcional): valor de tempo de vida da associação de segurança IKE. Intervalo: 60 a 86400 segundos. O valor padrão é `86400` segundos.

**Exemplos**:

Crie uma nova política IKE com o nome `my_ike`:
```
bluemix vpn ike-create my_ike -g my_gateway
```


## bluemix vpn ipsec-create
Cria uma política IPSec.

```
bluemix vpn ipsec-create POLICY_NAME -g GATEWAY_NAME [-d DESCRIPTION] [-pfs GROUP] [-e ENCRYPTION_ALGORITHM] [-lv LIFETIME_VALUE]
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

*POLICY_NAME* (obrigatório): nome da política IPSec.

-g *GATEWAY_NAME* (obrigatório): nome do gateway.

-d *DESCRIPTION* (opcional): descrição dos parâmetros especificados.

-pfs *GROUP* (opcional): identificador de grupo Diffie-Hellman (DH). Um valor válido é `Group2`, `Group5` ou `Group14`. O valor padrão é `Group2`.

-e *ENCRYPTION_ALGORITHM* (opcional): algoritmo de criptografia. Um valor válido é `aes-128`, `aes-192`, `aes-256` ou `3des`. O valor padrão é `aes-128`.

-lv *LIFETIME_VALUE* (opcional): valor de tempo de vida da associação de segurança. Intervalo: 60 a 86400 segundos. O valor padrão é `3600` segundos.

**Exemplos**:

Criar uma política IPSec com o nome `my_policy`:
```
bluemix vpn ipsec-create my_policy -g my_gateway
```


## bluemix vpn gateway-create
Cria um gateway VPN.

```
bluemix vpn gateway-create GATEWAY_NAME -t TYPE [-gateway_ip IP_ADDRESS] [-subnets SUBNET_ADDRESS]
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

*GATEWAY_NAME* (obrigatório): nome do gateway.

-t *TYPE* (obrigatório): contêineres para os quais deseja ativar o serviço. Um valor válido é `allSingleContainers`, `allContainerGroups` ou `allContainers`. Nenhum valor padrão; deve-se especificar um tipo.

-gateway_ip *IP_ADDRESS* (opcional): endereço IP do gateway.

-subnets *SUBNET_ADDRESS* (opcional): endereço de sub-rede no formato CIDR.

**Exemplos**:

Crie um gateway com o nome `my_gateway` e digite `allContainerGroups`:
```
bluemix vpn gateway-create my_gateway -t allContainerGroups
```


## bluemix vpn connections
Exibe informações sobre todas as conexões atuais.

```
bluemix vpn connections
```

**Pré-requisitos**: Terminal, Login, Destino


## bluemix vpn ikes
Exibe informações sobre as conexões IKE atuais.

```
bluemix vpn ikes
```

**Pré-requisitos**: Terminal, Login, Destino


## bluemix vpn ipsecs
Exibe informações sobre as conexões IPSec atuais.

```
bluemix vpn ipsecs
```

**Pré-requisitos**: Terminal, Login, Destino


## bluemix vpn gateways
Exibe informações sobre os gateways atuais.

```
bluemix vpn gateways
```

**Pré-requisitos**: Terminal, Login, Destino


## bluemix vpn connection
Exibe todas as informações sobre uma determinada conexão.

```
bluemix vpn connection CONNECTION_NAME
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

*CONNECTION_NAME* (obrigatório): nome da conexão a ser exibida.


## bluemix vpn ike
Exibe informações sobre uma conexão IKE.

```
bluemix vpn ike POLICY_NAME
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

*POLICY_NAME* (obrigatório): nome da política IKE a ser exibida.


## bluemix vpn ipsec
Exibe informações sobre uma conexão IPSec.

```
bluemix vpn ipsec POLICY_NAME
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

*POLICY_NAME* (obrigatório): nome da política IPSec a ser exibida.


## bluemix vpn gateway
Exibe informações de conexão de um gateway.

```
bluemix vpn gateway GATEWAY_NAME
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

*GATEWAY_NAME* (obrigatório): nome do gateway a ser exibido.


## bluemix vpn connection-delete
Exclui uma conexão existente.

```
bluemix vpn connection-delete CONNECTION_NAME
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

*CONNECTION_NAME* (obrigatório): nome da conexão a ser excluída.


## bluemix vpn ike-delete
Exclui uma política IKE existente.

```
bluemix vpn ike-delete POLICY_NAME
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

*POLICY_NAME* (obrigatório): nome da política IKE a ser excluída.


## bluemix vpn ipsec-delete
Exclui uma política IPSec existente.

```
bluemix vpn ipsec-delete POLICY_NAME
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

*POLICY_NAME* (obrigatório): nome da política IPSec a ser excluída.


## bluemix vpn gateway-delete
Exclui um gateway existente.

```
bluemix vpn gateway-delete GATEWAY_NAME
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

*GATEWAY_NAME* (obrigatório): nome do gateway a ser excluído.


## bluemix vpn connection-update
Atualiza uma conexão VPN existente.

```
bluemix vpn connection-update CONNECTION_NAME [-g GATEWAY_NAME] [-k PRESHARED_KEY] [-subnets "SUBNET/MASK"] [-cip CUSTOMER_GATEWAY_IP_ADDRESS] [-d DESCRIPTION] [-peer_id PEER_ID] [-admin_state ADMIN_STATE] [-dpd-action ACTION] [-gateway_ip IP_ADDRESS] [-i INITIATOR_STATE] [-dpd-timeout VALUE] [-dpd-interval VALUE] [-ike NAME] [-ipsec NAME]
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

*CONNECTION_NAME* (obrigatório): nome da conexão.

-g *GATEWAY_NAME* (opcional): nome do gateway.

-k *PRESHARED_KEY* (opcional): chave pré-compartilhada.

-subnets "*SUBNET*/*MASK*" (opcional): endereço de sub-rede no formato CIDR.

-cip *CUSTOMER_GATEWAY_IP_ADDRESS* (opcional): endereço IP do terminal remoto do túnel da VPN.

-d *DESCRIPTION* (opcional): descrição dos parâmetros especificados.

-peer_id *PEER_ID* (opcional): ID do peer remoto. Outro terminal do túnel da VPN.

-admin_state *ADMIN_STATE* (opcional): status da conexão VPN. Um valor válido é `UP` ou `DOWN`.

-dpd-action *ACTION* (opcional): ação a ser executada quando o peer for detectado como inativo. Um valor válido é `hold`, `clear`, `disabled`, `restart` ou `restart-by-peer`.

-gateway_ip *IP_ADDRESS* (opcional): endereço IP do terminal de túnel da VPN local.

-i *INITIATOR_STATE* (opcional): estado do iniciador.

-dpd-timeout *VALUE* (opcional): o valor de tempo limite em segundos após o qual a sessão é finalizada. Intervalo: 6 a 86400 segundos.

-dpd-interval *VALUE* (opcional): intervalo keep-alive em segundos. Envie mensagens keep-alive no intervalo configurado para verificar se o peer está ativo. Intervalo: 5 a 86399 segundos.

-ike *NAME* (opcional): nome da política IKE.

-ipsec *NAME* (opcional): nome da política IPSec.


## bluemix vpn ike-update
Atualiza uma política IKE.

```
bluemix vpn ike-update POLICY_NAME [-g GATEWAY_NAME] [-d DESCRIPTION] [-pfs GROUP] [-e ENCRYPTION_ALGORITHM] [-lv LIFETIME_VALUE]
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

*POLICY_NAME* (obrigatório): nome da política IKE.

-g *GATEWAY_NAME* (opcional): nome do gateway.

-d *DESCRIPTION* (opcional): descrição dos parâmetros especificados.

-pfs *GROUP* (opcional): identificador de grupo Diffie-Hellman (DH). Um valor válido é `Group2`, `Group5` ou `Group14`.

-e *ENCRYPTION_ALGORITHM* (opcional): algoritmo de criptografia. Um valor válido é `aes-128`, `aes-192`, `aes-256` ou `3des`.

-lv *LIFETIME_VALUE* (opcional): valor de tempo de vida da associação de segurança IKE. Intervalo: 60 a 86400 segundos.


## bluemix vpn ipsec-update
Atualiza uma política IPSec.

```
bluemix vpn ipsec-update POLICY_NAME [-g GATEWAY_NAME] [-d DESCRIPTION] [-pfs GROUP] [-e ENCRYPTION_ALGORITHM] [-lv LIFETIME_VALUE]
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

*POLICY_NAME* (obrigatório): nome da política IPSec.

-g *GATEWAY_NAME* (opcional): nome do gateway.

-d *DESCRIPTION* (opcional): descrição dos parâmetros especificados.

-pfs *GROUP* (opcional): identificador de grupo Diffie-Hellman (DH). Um valor válido é `Group2`, `Group5` ou `Group14`.

-e *ENCRYPTION_ALGORITHM* (opcional): algoritmo de criptografia. Um valor válido é `aes-128`, `aes-192`, `aes-256` ou `3des`.

-lv *LIFETIME_VALUE* (opcional): valor de tempo de vida da associação de segurança. Intervalo: 60 a 86400 segundos.


## bluemix vpn gateway-update
Atualiza um gateway VPN existente.

```
bluemix vpn gateway-update GATEWAY_NAME [-t TYPE] [-gateway_ip IP_ADDRESS] [-subnets SUBNET_ADDRESS]
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

*GATEWAY_NAME* (obrigatório): nome do gateway.

-t *TYPE* (opcional): contêineres para os quais deseja ativar o serviço. Um valor válido é `allSingleContainers`, `allContainerGroups` ou `allContainers`.

-gateway_ip *IP_ADDRESS* (opcional): endereço IP do gateway.

-subnets *SUBNET_ADDRESS* (opcional): endereço de sub-rede no formato CIDR.
