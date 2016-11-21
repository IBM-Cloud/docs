---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# IBM Secure Service Container
{: #etn_ssc}

Última atualização: 13 de outubro de 2016
{: .last-updated}

O IBM Blockchain High Security Business Network é implementado como um dispositivo no IBM Secure Service Container, que fornece a infraestrutura de base para
hospedar serviços de blockchain. O dispositivo combina sistemas operacionais, contêineres do Docker, middleware e componentes de software que trabalham de forma
autônoma e fornece serviços principais e infraestrutura com segurança otimizada.
{:shortdesc}

O IBM Secure Service Container traz a criptografia avançada, a segurança e a confiabilidade da plataforma z Systems LinuxONE para serviços de blockchain para
manipular dados sensíveis e regulares. O Blockchain é protegido por uma série de recursos do IBM Secure Service Container: sistema operacional encapsulado, discos
de dispositivo criptografados, proteção contra violação, memória protegida e forte isolamento de LPAR que podem ser configurados para correspondência de certificação de EAL5+.

O diagrama de arquitetura a seguir ilustra como o IBM Secure Service Container e os dispositivos de blockchain são organizados:

![Diagrama de arquitetura](images/Architecture_HSBN_SSC.png "IBM Secure Service Container e dispositivos de blockchain")
*Figura 1. Visão geral de IBM Secure Service Container e dispositivos de blockchain*
<br><br>
## Recursos de segurança de chave
O IBM Secure Service Container fornece as funções de segurança otimizada a seguir para serviços de blockchain:  

### Proteção a partir de Administradores de sistema
>O código do dispositivo não pode ser acessado até mesmo por Administradores de plataforma ou de sistema.  O acesso a dados é controlado pelo dispositivo; portanto, o acesso não autorizado é desativado.  Esta é
suportada por meio de uma combinação de assinar e criptografar todos os dados em andamento e inativos. Todo o acesso à memória também é removido. O firmware suporta isso com uma arquitetura de inicialização segura.

>Os administradores do sistema têm as limitações a seguir quando o blockchain está protegido pelo IBM Secure Service Container:
>* não é possível acessar nós
>* não é possível visualizar a rede de blockchain

### Proteção contra violação  
>O IBM Secure Service Container desativa todas as interfaces externas que fornecem acesso de memória de LPAR. Um carregador de inicialização de imagem é sinalizado para assegurar que ela não seja violada
ou trocada com uma diferente.

### Discos de dispositivo criptografados
>Todos os códigos e dados armazenados em disco são criptografados em todos os momentos usando a camada de criptografia do Linux:  
- Sistema operacional encapsulado
- IP protegido
- Monitoramento integrado e com capacidade de recuperação automática  
<br>

## Gerenciando dispositivos por meio de APIs REST
Dispositivos de software são pré-configurados para você usar na plataforma de z Systems confiável, segura e escalável. É possível gerenciar esses dispositivos por meio de APIs REST sem qualquer
configuração.

Para gerenciar ativos de blockchain por meio de APIs REST, é possível usar a UI do Swagger no painel do Blockchain em ferramentas de comando do Bluemix ou REST, como `curl` ou
`Postman`.

Por exemplo, para obter informações sobre todos os peers na rede, emita o comando a seguir usando `curl`:
```
curl -u <username>:<password> https://<peer_ip>:<port>/network/peers
```
Consulte o comando curl de amostra e os resultados retornados a seguir:
* Comando :
```
curl -u dashboarduser_type0_2ef27***:89317***https://ad3130e8-4a1a-4ce6-a084-689a345a3308_vp1-api.blockchain.ibm.com:443/network/peers
```
* Informações retornadas sobre todos os peers na rede:
```
{
	"peers": [{
		"ID" : {
			"name": "ad3130e8-4a1a-4ce6-a084-689a345a3308_vp2"
		},
		"address": "ad3130e8-4a1a-4ce6-a084-689a345a3308_vp2-discovery.blockchain.ibm.com:30303",
		"type": 1,
		"pkiID": "rC0uvv0cbSbiT8RUGKPQM3q/o09oyWlcBmRxogi2Cls="
	},
	{
		"ID" : {
			"name": "ad3130e8-4a1a-4ce6-a084-689a345a3308_vp1"
		},
		"address": "ad3130e8-4a1a-4ce6-a084-689a345a3308_vp1-discovery.blockchain.ibm.com:30303",
		"type": 1,
		"pkiID": "oeoI+Xa/lW8Xvrvv71A+Nvzit+JDa+oIkthpZHwfaTE="
	}]
}
```
Para saber mais sobre como interagir com blockchain por meio de APIs de REST, veja [Monitor de painel](https://new-console.ng.bluemix.net/docs/services/blockchain/ibmblockchainmonitor.html) e
[Amostras e tutoriais](https://new-console.ng.bluemix.net/docs/services/blockchain/ibmblockchain_tutorials.html).
