---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Introdução ao {{site.data.keyword.vpn_short}}
{: #vpn}  
*Última atualização: 09 de maio de 2016*

O serviço {{site.data.keyword.vpn_full}} para Bluemix&reg; está disponível para acesso com segurança somente aos Contêineres IBM (contêineres Docker) dentro do ambiente de nuvem do IBM Bluemix. É possível usar o ambiente de nuvem do IBM Bluemix como uma extensão de seu datacenter corporativo. Também é possível conectar a servidores SoftLayer usando o serviço IBM VPN.
{:shortdesc}

Antes de começar, assegure-se de que tenha um contêiner do IBM Docker pronto para uso. Veja [Contêineres IBM para Bluemix](https://www.ng.bluemix.net/docs/containers/container_index.html) para obter detalhes de como criar e gerenciar Contêineres IBM.  

Para começar, selecione o quadro da instância de serviço **Rede privada virtual** no painel Bluemix. Conclua as etapas a seguir:

1. Configure o gateway {{site.data.keyword.vpn_short}} selecionando **CRIAR GATEWAY**. Um gateway padrão é criado. Se necessário, edite a configuração de gateway conforme mostrado nas etapas a seguir.  
{: #gateway}  

  1. Selecione **EDITAR**.  
  2. Especifique o nome do gateway.  
  3. Selecione o contêiner e o grupo de contêiner com os quais você deseja usar o serviço da VPN.
	**Observação:** as sub-redes privadas do contêiner e do grupo de contêiner são pré-selecionadas de forma que você possa acessá-las por meio da conexão da VPN.
  4. Selecione **SALVAR**.  

 É possível usar as políticas IKE e IPSec padrão ou configurar políticas customizadas. Se desejar usar as políticas padrão, ignore a etapa 4.

2. Configure a política IKE selecionando a guia **Políticas IKE e IPSec**.
  1. Selecione **INCLUIR NOVA**.  
  2. Especifique os detalhes a seguir:
	* **Nome**: o nome da política IKE
	* **Algoritmo de autorização**: sha1; não pode ser mudado  
	* **Algoritmo de criptografia**: selecione no menu suspenso. Valores: aes-128 (padrão), aes-192, aes-256, 3des
	* **Tempo de vida chave**: valor de tempo de vida (em segundos) da associação de segurança IKE. Intervalo: de 60 a 86400. Valor padrão: 86400
	* **PFS**: identificador do grupo Diffie-Hellman (DH). Valores: Group2, Group5, Group14. Valor padrão: Group2
	* **Modo de negociação**: principal; não pode ser mudado
	* **Versão**: IKEV1; não pode ser mudada
  3. Selecione **SALVAR**.

3. Configure a polícia IPSec:
  1. Selecione **INCLUIR NOVA**.  
  2. Especifique os detalhes a seguir:
  	* **Nome**: o nome da política IPSec  
  	* **Algoritmo de autorização**: sha1; não pode ser mudado  
  	* **Algoritmo de criptografia**: selecione no menu suspenso. Valores: aes-128 (padrão), aes-192, aes-256, 3des
  	* **Tempo de vida chave**: valor de tempo de vida (em segundos) da associação de segurança. Intervalo: de 60 a 86400. Valor padrão: 3600
  	* **PFS**: identificador do grupo Diffie-Hellman (DH). Valores: Group2, Group5, Group14. Valor padrão: Group2
  	* **Protocolo de conversão**: ESP; não pode ser mudado
  	* **Modo de encapsulamento**: túnel; não pode ser mudado
  3. Selecione **SALVAR**.  

4. Forneça os detalhes para estabelecer uma conexão entre seu datacenter ou o gateway VPN (rede privada virtual) do servidor SoftLayer e o gateway VPN (rede privada virtual) da IBM.  
{: #site}  

  1. Selecione a guia **Dispositivo de gateway**.
  2. Selecione **Criar conexão** na seção **Conexões do site**.
  3. Especifique os detalhes de conexão do site a seguir:  
  	* **Nome**: o nome da conexão  
  	* **Descrição**: a descrição da conexão (opcional)  
  	* **Sequência de chave pré-compartilhada**: chave pré-compartilhada (segredo) a ser usada para autenticação
  	* **Estado do administrador**: status da conexão VPN (rede privada virtual). Selecione no menu suspenso: PARA CIMA ou PARA BAIXO. Valor padrão: Para cima  
  	* **IP do gateway do cliente**: endereço IP do terminal remoto do túnel VPN  
  	* **Sub-rede do cliente**: endereço de sub-rede remota em formato CIDR (Classless Inter-Domain Routing). Selecione o sinal de mais para incluir outra sub-rede.
  4. (Opcional) Configure os parâmetros das **Configurações avançadas** a seguir:  
  	* **Política IKE**: selecione a política IKE.  
  	* **Intervalo keep-alive**: o intervalo keep-alive em segundos. Envie mensagens keep-alive no intervalo configurado para verificar se o peer está ativo. Valor padrão: 15. Intervalo: de 5 a 86399
  	* **Ação no peer inativo**: ação a ser tomada quando o peer for detectado como inativo.  
    	Valores: 
  		* suspenso (valor padrão): a associação de segurança (SA) é colocada em suspensão 
  		* limpar: a SA é excluída
  		* desativada: a SA é desativada
  		* reiniciar: a SA é renegociada
  		* reiniciar por peer: todas as SAs com o peer inativo são renegociadas  
  	* **Política IPSec**: selecione a política IPSec.
  	* **Tempo limite de keep-alive**: valor do tempo limite em segundos após o qual a sessão é finalizada. Valor padrão: 120. Intervalo: de 6 a 86400. O valor de tempo limite de keep-alive deve ser maior que o valor do intervalo keep-alive.
  5. Selecione **SALVAR**.

  **Nota:** quando a conexão estiver sendo estabelecida, o status da conexão será exibido como ***criação pendente***. Quando você vir esse status, atualize a tela algumas vezes para ver o status ativo da conexão.

**Importante:** se estiver usando um aplicativo da web, deverá ligar o aplicativo da web ao contêiner do Docker que está sendo usado. Essa ligação é necessária para o tráfego passar pelo túnel VPN IPSec.

**Importante:** o serviço IBM VPN opera atualmente no modo respondente. Para iniciar a conexão VPN (rede privada virtual), um pacote de dados deve fluir do gateway IBM VPN (rede privada virtual) para seu datacenter no local ou o servidor SoftLayer. Depois que a conexão VPN (rede privada virtual) for estabelecida, o tráfego poderá fluir em direção entre os terminais da conexão VPN (rede privada virtual).

 
# rellinks
## amostras 
{: #samples}  
* [Exemplo de configuração de gateway strongSwan no local](vpn_onpremises.html#strongswan){: new_window}
* [Exemplo de configuração de gateway Vyatta no local](vpn_onpremises.html#vyatta){: new_window}
* [Exemplo de configuração do SoftLayer Gateway Appliance Service (GaaS) no local](vpn_onpremises.html#gaas){: new_window}
* [Exemplo de configuração do Cisco ASA no local](vpn_onpremises.html#cisco){: new_window}

## api  
{: #api}  
* [APIs IBM VPN RESTful](https://new-console.ng.bluemix.net/apidocs/101){: new_window}

## gerais  
{: #general}  
* [Interface da linha de comandos IBM VPN](../../cli/plugins/vpn/index.html){: new_window}
* [Perguntas mais frequentes do IBM VPN](vpn_faq.html#vpn_faq){: new_window}
* [Folha de precificação do IBM Bluemix](https://console.{DomainName}/pricing/){: new_window}
* [Pré-requisitos do IBM Bluemix](https://developer.ibm.com/bluemix/support/#prereqs)
