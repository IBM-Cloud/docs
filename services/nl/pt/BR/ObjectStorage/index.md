{:new_window: target="_blank"}

# Introdução ao {{site.data.keyword.objectstorageshort}} {: #getting-started-with-object-storage} 

O {{site.data.keyword.objectstoragefull}} fornece a você acesso a uma conta Swift do {{site.data.keyword.objectstorageshort}} totalmente provisionada para gerenciar seus dados. O swift fornece uma plataforma de armazenamento acessível por API totalmente distribuída. É possível usá-la diretamente em seus aplicativos ou para backups, tornando-a ideal para armazenamento de ampliação e custo efetivo.

O IBM {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}} usa o OpenStack Identity (Keystone) para autenticação e pode ser acessado diretamente usando chamadas API v1 do OpenStack Object Storage (Swift). O IBM {{site.data.keyword.objectstorageshort}} pode estar ligado a um aplicativo {{site.data.keyword.Bluemix_notm}} ou ser acessado de fora de um aplicativo {{site.data.keyword.Bluemix_notm}}. 

Mais informações e documentação sobre como usar o OpenStack Swift e o Keystone estão disponíveis no [site de documentação do OpenStack](http://docs.openstack.org){: new_window}.

O diagrama de arquitetura do {{site.data.keyword.objectstorageshort}} é o seguinte:

[![{{site.data.keyword.objectstorageshort}} Diagrama de arquitetura](images/object_storage_solution_archectiture_small.png)](http://www.ng.bluemix.net/docs/api/content/services/ObjectStorage/images/object_storage_solution_archectiture.png){: new_window}

*Figure 1. {{site.data.keyword.objectstorageshort}} Diagrama de arquitetura*

**Nota:** a criptografia do lado do provedor não é fornecida. É responsabilidade do aplicativo cliente criptografar dados antes de fazer upload.

**Nota:** o plano Beta do serviço {{site.data.keyword.objectstorageshort}} será removido do catálogo após a disponibilidade geral do serviço {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.objectstorageshort}}. Após um período de cortesia, as instâncias de serviço que usam o plano Beta serão removidas. [Atualize seu plano de precificação](#changeplan) para continuar usando o serviço {{site.data.keyword.objectstorageshort}}. 




## Criando uma instância do {{site.data.keyword.objectstorageshort}} no {{site.data.keyword.Bluemix_notm}} {: #creating-object-storage-instance} 

### Como criar uma instância do serviço {{site.data.keyword.objectstorageshort}}
1.	Acesse a guia **Catálogo** do {{site.data.keyword.Bluemix_notm}} e insira **{{site.data.keyword.objectstorageshort}}** na caixa de procura ou acesse **Serviços** e selecione **Armazenamento**. Clique no serviço **{{site.data.keyword.objectstorageshort}}**. 
2.	Selecione seu espaço, app, nome de serviço e plano e clique em **Criar**. 
**Nota:** se você escolher inicialmente a opção **Deixar desvinculado** para o campo **App**, ainda poderá ligar a instância de serviço ao aplicativo {{site.data.keyword.Bluemix_notm}} depois de concluir a configuração. Consulte as instruções a seguir.

## Usando o {{site.data.keyword.objectstorageshort}} a partir de um app {{site.data.keyword.Bluemix_notm}} {: #using-object-storage-from-bluemix-app} 

### Como ligar seu serviço {{site.data.keyword.objectstorageshort}} a um aplicativo após a criação {: #bind-object-storage-to-application} 
1.	No painel {{site.data.keyword.Bluemix_notm}}, selecione o app que deseja ligar.
2.	Na visão geral do app, clique em **Ligar um serviço ou uma API**.
3.	Selecione sua instância do {{site.data.keyword.objectstorageshort}} na lista de serviços e clique em **Incluir**.
4.	Clique em **Remontar** quando solicitado. Seu app deve ser remontado para usar o novo serviço.

### Contexto ligado

Para usar o {{site.data.keyword.objectstorageshort}} em um contexto ligado, as credenciais de nuvem são fornecidas indiretamente por meio do processo de ligação de aplicativos. Depois de ligar com êxito uma instância de serviço ao seu aplicativo, uma configuração semelhante à do exemplo a seguir é incluída na variável de ambiente `VCAP_SERVICES`.

    {
    "Object-Storage": [
    {
      "name": "Object-Storage - YP",
      "label": "Object-Storage",
      "plan": "Free",
      "credentials": {
         "auth_url": "https://identity.open.softlayer.com",
         "project": "object_storage_d049255b",
         "projectId": "0f47b41b06d047f9aae3b33f1db061ed",
         "region": "dallas",
         "userId": "ad78b2a3f843466988afd077731c61fc",
         "username": "user_202db1f8a7aa3f3ac51ec68f10dbe7dc29070bc7",
         "password": "K/jyIi2jR=1?D.TP",
         "domainId": "2df6373c549e49f8973fb6d22ab18c1a",
         "domainName": "639347"
        }
       }
      ]
    }

## Usando a interface com o usuário do {{site.data.keyword.objectstorageshort}} {: #using-object-storage-ui}

### Elementos de UI e navegação
Quando seu {{site.data.keyword.objectstorageshort}} estiver provisionado, será possível ver informações sobre a instância no painel de instância do serviço {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}}. No painel, selecione sua instância do {{site.data.keyword.objectstorageshort}} para visualizar o painel com informações mais detalhadas.  
#### Dados de uso
Na parte superior do painel, você verá as informações de uso de armazenamento para sua instância. Ele mostra também o número atual de **Contêineres de armazenamento** e o número total de **Objetos** em todos os seus contêineres. Ele lista seu uso de memória em megabytes. **Armazenamento consumido** refere-se à quantia atual de espaço usado. 
#### Ações
Para recuperar os dados de uso mais recentes, clique no botão **Atualizar**.   
####Navegador de objetos 
A seção da parte inferior do painel contém o navegador de objetos. Use o navegador de objeto para gerenciar os contêineres e objetos do armazenamento de objetos. É possível criar contêineres, fazer upload de arquivos, excluir contêineres e excluir arquivos entre outras ações.

## Usando a CLI do Swift para acessar o {{site.data.keyword.objectstorageshort}} {: #using-swift-cli}

É possível acessar o serviço {{site.data.keyword.objectstorageshort}} na Internet e a partir de aplicativos e máquinas virtuais no IBM {{site.data.keyword.Bluemix_notm}}. Os casos de uso comuns para o serviço {{site.data.keyword.objectstorageshort}} são como a seguir:

* Fazendo backup dos dados de volume de suas instâncias
* Usando como um local intermediário ao transferir grandes quantias de dados
* Transferindo dados entre os ambientes que não estão diretamente conectados
* Agindo como um armazenador central

O serviço {{site.data.keyword.objectstorageshort}} baseia-se no OpenStack Swift e pode ser acessado usando qualquer aplicativo cliente compatível. Esta seção descreve como usar o cliente Python Swift, que é a interface de linha de comandos (CLI) para a API do {{site.data.keyword.objectstorageshort}} e suas extensões, para trabalhar com contêineres e arquivos.

### Instalando o cliente Swift

Instale o software obrigatório a seguir, se ainda não estiver instalado. Para obter mais informações, consulte a [Documentação do OpenStack](http://docs.openstack.org/user-guide/common/cli_install_openstack_command_line_clients.html#install-the-prerequisite-software){: new_window}. 
* Python 2.7 ou mais recente
* Pacote setuptools
* Pacote pip

Instale o cliente Python Swift usando o Python pip:

	sudo pip install python-swiftclient

### Configurando o Cliente

O cliente Swift usa as informações sobre autenticação das variáveis de ambiente a seguir:
* ```OS_AUTH_URL``` é a URL de terminal
* ```OS_USER_ID``` é o nome do usuário
* ```OS_PASSWORD``` é a senha

Configure as informações sobre autenticação como a seguir. 

	export OS_USER_ID=24a20b8e4e724f5fa9e7bfdc79ca7e85
	export OS_PASSWORD=aaa55AAAaaaaa]?,
	export OS_PROJECT_ID=383ec90b22ff4ba4a78636f4e989d5b1
	export OS_AUTH_URL=https://identity.open.softlayer.com/v3
	export OS_REGION_NAME=dallas
	export OS_IDENTITY_API_VERSION=3
	export OS_AUTH_VERSION=3

É possível localizar os valores de credenciais para o serviço {{site.data.keyword.objectstorageshort}} na página **Credenciais de serviço** na interface com o usuário do {{site.data.keyword.objectstorageshort}}. 

**Nota:** certifique-se de incluir um ```/v3``` na ```auth_url`` das credenciais na interface com o usuário do {{site.data.keyword.objectstorageshort}} ao configurar as variáveis de ambiente ```OS_AUTH_URL`` para o cliente Swift.


![Credenciais de serviço do {{site.data.keyword.objectstorageshort}}](images/service_credentials.jpg)

*Figure 2. {{site.data.keyword.objectstorageshort}} Credenciais de serviço*

### Trabalhando com contêineres

Listando contêineres:

	swift list
	
Criando um contêiner:

	swift post <container_name>
	
Listando o conteúdo de um contêiner:

	swift list <container_name>

### Trabalhando com Objetos

#### Incluindo um arquivo em um contêiner

	swift upload <container_name> <file_name>

#### Incluindo arquivos maiores que 5 GB em um contêiner

Se você estiver fazendo upload de um arquivo maior que 5 GB, deverá dividi-lo em chunks menores. É possível instruir o cliente Swift para manipular esse upload fornecendo o parâmetro ```-segment-size```:

	swift upload <container_name> <file_name> --segment-size <size_in_bytes>
	
Cada segmento é transferido por upload em paralelo para um contêiner separado chamado ```<container_name>_segments```. Depois que todos os segmentos são transferidos por upload, o Swift cria um arquivo manifest para que os segmentos possam ser transferidos por download em um único arquivo do contêiner original ```<container_name>`` com o nome de arquivo original ```<file_name>``.

Por exemplo, o comando a seguir faz upload de um arquivo chamado ```large_file``` de um contêiner chamado ```test_container`` com o tamanho de segmento ```1073741824``.

	swift upload test_container -S 1073741824 large_file

É possível executar o comando a seguir para fazer download do arquivo:

	swift download test_container large_file

#### Transferindo um Arquivo por Download

	swift download <container_name> <file_name>
	
#### Incluindo um diretório em um contêiner

Swift não possui uma estrutura de diretórios verdadeira, mas usa a nomenclatura para representar um layout de diretório. Para incluir um diretório em um contêiner, execute o comando a seguir:

	swift upload <container_name> <directory_name>
	
Esse comando fará upload da estrutura de diretório completa como um caminho relativo. Por exemplo, se você especificar ```/mnt/volume1```, a estrutura de diretório mnt/volume1 será anexada a todos os nomes de arquivos para indicar a estrutura de diretório.

	
#### Fazendo download de um diretório

Para fazer download de uma estrutura de diretório, use o parâmetro ```-prefix``` para indicar o diretório ou a estrutura de diretório da qual você deseja fazer download.

	swift download <container_name> --prefix <directory>
	
#### Excluindo um Arquivo

	swift delete <container_name> <file_name>

### Criando uma URL provisória

Uma URL provisória é uma URL longa, difícil de adivinhar que pode ser usada por um período especificado para fazer download de objetos sem requerer autenticação adicional. Gere uma URL provisória com as etapas a seguir:

1. Identifique sua conta de autenticação.
2. Configure uma chave secreta.
3. Crie a URL provisória.

#### Identificando sua conta de autenticação

O comando Swift ```stat``` imprime informações sobre sua conta:

	swift stat

Localize o campo Conta e anote a sequência inteira atrás de *Conta*:, incluindo ```AUTH_```.

#### Configurando uma chave secreta

Essa chave pode ser qualquer coisa que você selecionar, mas a melhor prática é selecionar uma sequência longa, aleatória e difícil de adivinhar.

	swift post -m "Temp-URL-Key:<key>"

#### Criando a URL provisória

O comando Swift ```tempurl``` usa estes argumentos posicionais:

* [method] GET para permitir download, PUT para permitir upload
* [seconds]  Tempo em segundos que a URL provisória estará disponível
* [path] O caminho completo do objeto expresso como /v1/<auth_account>/<container_name>/<object_name>
* [key]  A chave configurada na etapa 2

```
swift tempurl GET <seconds> <path> <key>
```

Esse comando retornará uma URL que pode ser anexada ao nome do cluster para obter uma URL completa. Use a URL completa para fazer download do objeto com qualquer cliente HTTP compatível, como curl, wget ou Firefox.

## Usando a API REST do Swift para acessar o {{site.data.keyword.objectstorageshort}} {: #using-swift-restapi}

É possível usar a API REST do Swift com uma interface do cliente da linha de comandos, como cURL, ou chamar a API a partir do aplicativo.  

### URL do {{site.data.keyword.objectstorageshort}} {: #access-points}

Para interagir com a API do {{site.data.keyword.objectstorageshort}}, construa a URL do {{site.data.keyword.objectstorageshort}} como a seguir:

	https://<access point>/<API version>/AUTH_<project ID>/<container namespace>/<object namespace>

Exemplo:

![URL do {{site.data.keyword.objectstorageshort}}](images/Swift_URL.png)

*Figura 3. {{site.data.keyword.objectstorageshort}} URL*

A URL consiste em cinco partes. A ```<API version>``` é v1. É possível localizar o ```<project ID>``, ```<container namespace>`` e ```<object namespace>`` do {{site.data.keyword.objectstorageshort}} na interface com o usuário do {{site.data.keyword.objectstorageshort}}.  Para o ```<access point>``, consulte a tabela a seguir: 


| **Região**  |     **Ponto de acesso interno**                             |     **Ponto de acesso público**                   |
|-------------|-----------------------------------------------------------|-----------------------------------------------|
| Dallas      | https://dal.objectstorage.service.open.networklayer.com/  | https://dal.objectstorage.open.softlayer.com/ | 
| Londres      | https://lon.objectstorage.service.open.networklayer.com/  | https://lon.objectstorage.open.softlayer.com/ |


*Tabela 1. Ponto de acesso do {{site.data.keyword.objectstorageshort}}*

Use o ponto de acesso interno ao acessar o serviço {{site.data.keyword.objectstorageshort}} de dentro do {{site.data.keyword.Bluemix_notm}} ou o ponto de acesso público ao acessar o serviço {{site.data.keyword.objectstorageshort}} de fora do {{site.data.keyword.Bluemix_notm}}.

### API do {{site.data.keyword.objectstorageshort}}

Consulte a [Referência completa da API do OpenStack Swift](http://developer.openstack.org/api-ref-objectstorage-v1.html){: new_window} para obter uma lista abrangente das opções e exemplos de API REST do {{site.data.keyword.objectstorageshort}}.

## Usando o {{site.data.keyword.objectstorageshort}} em várias regiões {: #multi-regions}  

O serviço IBM {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}} suporta as regiões de armazenamento Dallas e Londres. Essas regiões de armazenamento são independentes da região do {{site.data.keyword.Bluemix_notm}}, como sul do EUA e Reino Unido, na qual a instância de serviço {{site.data.keyword.objectstorageshort}} foi criada.  Por exemplo, se você criar uma instância do {{site.data.keyword.objectstorageshort}} na região sul dos EUA do {{site.data.keyword.Bluemix_notm}}, poderá ler e gravar dados na região de armazenamento Dallas ou Londres.  

Para a região sul dos EUA do {{site.data.keyword.Bluemix_notm}}, a região de armazenamento Dallas é a padrão. Para a região Reino Unido do {{site.data.keyword.Bluemix_notm}}, a região de armazenamento Londres é a padrão.  A interface com o usuário do {{site.data.keyword.objectstorageshort}} sempre ativa a região de armazenamento padrão da região do {{site.data.keyword.Bluemix_notm}}. Para alternar regiões, clique na lista suspensa da Região do {{site.data.keyword.objectstorageshort}} e escolha outra região.

![Região de mudança do {{site.data.keyword.objectstorageshort}}](images/change_region.png)

*Figura 4. {{site.data.keyword.objectstorageshort}} Mudança de região*

**Nota:** o serviço {{site.data.keyword.objectstorageshort}} NÃO suporta replicação de região de armazenamento cruzada.

### Acesso multiregion

Para usar o serviço {{site.data.keyword.objectstorageshort}}, deve-se [autenticar no OpenStack Keystone](#keystone-authentication). Após a autenticação bem-sucedida, um ```X-Subject-Token``` e os terminais do {{site.data.keyword.objectstorageshort}} ficarão disponíveis na resposta.

Por exemplo, para criar um contêiner chamado ```my_container``` na região de armazenamento Dallas, especifique um ponto de acesso Dallas no comando curl como a seguir:

	# curl -i https://dal.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAAAAABWlw5mwttbb_6G3LnTiGusyoOSEHXMG7oTnDYWN1vBZB6XAxUEhz4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5N7lEZyyKQlsgmQWcrch8VOO_OiSKKToORYR7luI-2TrR_JIVZm-8AAS6hLhk9"

	HTTP/1.1 201 Created
	Content-Length: 0
	Content-Type: text/html; charset=UTF-8
	X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
	Date: Thu, 14 Jan 2016 03:16:13 GMT


Para criar um contêiner chamado ```my_container``` na região de armazenamento Londres, especifique um ponto de acesso Londres no comando curl como a seguir:

	# curl -i https://lon.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAAAAABWlw5mwttbb_6G3LnTiGusyoOSEHXMG7oTnDYWN1vBZB6XAxUEhz4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5N7lEZyyKQlsgmQWcrch8VOO_OiSKKToORYR7luI-2TrR_JIVZm-8AAS6hLhk9"

	HTTP/1.1 201 Created
	Content-Length: 0
	Content-Type: text/html; charset=UTF-8
	X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
	Date: Thu, 14 Jan 2016 03:16:13 GMT

**Nota:** o ```X-Subject-Token``` adquirido do Keystone funciona nas regiões de armazenamento. 

Para obter mais informações sobre os pontos de acesso para diferentes regiões, consulte a tabela [Ponto de acesso do Object Storage](#access-points).


## Entendendo autenticação e credenciais {: #understanding-authentication-credentials}

### Gerando credenciais do {{site.data.keyword.objectstorageshort}} sem ligar um aplicativo

Para gerar credenciais de nuvem do {{site.data.keyword.objectstorageshort}} para uso fora de um aplicativo {{site.data.keyword.Bluemix_notm}}, deve-se gerar uma chave de serviço para sua instância do {{site.data.keyword.objectstorageshort}}. É possível gerar a uma nova chave selecionando **Credenciais de serviço** na barra lateral da interface com o usuário ou usando o Cloud Foundry CLI (versão 6.11.3 ou mais recente). Depois de gerar e recuperar uma chave de serviço para sua instância do {{site.data.keyword.objectstorageshort}}, será possível usar as informações de integração de nuvem para solicitar um token Keystone usando um OpenStack SDK ou a API do OpenStack Identity e iniciar o uso da conta Swift para gerenciar objetos.
   
Para criar a chave usando o Cloud Foundry CLI, efetue login e execute o comando a seguir:
 
    cf create-service-key <object_storage_instance_name> <unique_name_for_this_key>

Para recuperar as credenciais de serviço do Cloud Foundry CLI, execute o comando a seguir:

	cf service-key <object_storage_instance_name> <unique_name_for_this_key>


### Projetos em nuvem e usuários
O provisionamento de uma nova instância do {{site.data.keyword.objectstorageshort}} cria um projeto Keystone isolado no IBM Public Cloud. Ao ligar um novo aplicativo à instância do {{site.data.keyword.objectstorageshort}}, é criado um novo usuário do Keystone com acesso ao projeto. Quando você desprovisiona a instância, o projeto e o usuário são excluídos.

### OpenStack Identity (Keystone) v3 {: #keystone-authentication}
A estrutura de credenciais contém um conjunto completo de atributos para permitir a escolha do método de solicitação de token do OpenStack ou o OpenStack SDK que melhor se ajusta ao seu aplicativo. 
 
A solicitação de token v3 recomendada é uma solicitação de POST para https://identity.open.softlayer.com/v3/auth/tokens conforme mostrado no comando curl a seguir:

	curl -i \
	  -H "Content-Type: application/json" \
	  -d '
	{
		"auth": {
			"identity": {
				"methods": [
					"password"
				],
				"password": {
					"user": {
						"id": "ad78b2a3f843466988afd077731c61fc",
						"password": "K/jyIi2jR=1?D.TP"
					}
				}
			},
			"scope": {
				"project": {
					"id": "0f47b41b06d047f9aae3b33f1db061ed"
				}
			}
		}
	}' \
	  https://identity.open.softlayer.com/v3/auth/tokens ; echo

Use o valor do campo ```X-Subject-Token``` do cabeçalho de resposta como o campo ```X-Auth-Token`` ao fazer solicitações para o serviço {{site.data.keyword.objectstorageshort}}.

Um exemplo de resposta é como a seguir:

	HTTP/1.1 201 Created
	X-Subject-Token: gAAAAABWlw5mwttbb_6G3LnTiGusyoOSEHXMG7oTnDYWN1vBZB6XAxUEhz4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5N7lEZyyKQlsgmQWcrch8VOO_OiSKKToORYR7luI-2TrR_JIVZm-8AAS6hLhk9
	Vary: X-Auth-Token
	Content-Type: application/json
	Content-Length: 960
	Date: Tue, 10 Jun 2014 20:40:14 GMT
	
	{"token": 
	{"audit_ids": ["ECwrVNWbSCqmEgPnu0YCRw"], "methods": ["password"],
	 "roles": [{"id": "c703057be878458588961ce9a0ce686b", "name": "admin"}],
	 "expires_at": "2014-06-10T21:40:14.360795Z", 
	 "project": {"domain": {"id": "default", "name": "Default"}, "id": "3d4c2c82bd5948f0bcab0cf3a7c9b48c", "name": "demo"}, 
	 "catalog": [
	 {
		"endpoints": [
			{
			"adminURL": "https://lon.objectstorage.service.open.networklayer.com/v1/AUTH_35a68d1d115b4a0f8c7975d4f96f256b",
			"id": "20cbfa6ff22b4a67a1484d30235bfc80",
			"internalURL": "https://lon.objectstorage.service.open.networklayer.com/v1/AUTH_35a68d1d115b4a0f8c7975d4f96f256b",
			"publicURL": "https://lon.objectstorage.open.softlayer.com/v1/AUTH_35a68d1d115b4a0f8c7975d4f96f256b",
			"region": "london"
			},
			{
			"adminURL": "https://dal.objectstorage.service.open.networklayer.com/v1/AUTH_35a68d1d115b4a0f8c7975d4f96f256b",
			"id": "4207049680fa4effbecd044c7448a8cb",
			"internalURL": "https://dal.objectstorage.service.open.networklayer.com/v1/AUTH_35a68d1d115b4a0f8c7975d4f96f256b",
			"publicURL": "https://dal.objectstorage.open.softlayer.com/v1/AUTH_35a68d1d115b4a0f8c7975d4f96f256b",
			"region": "dallas"
			}
			],
		"endpoints_links": [],
		"name": "swift",
		"type": "object-store"
		},
	 ], 
	 "extras": {},
	 "user": {"domain": {"id": "default", "name": "Default"}, "id": "3ec3164f750146be97f21559ee4d9c51", "name": "admin"},  "issued_at": "2014-06-10T20:40:14.360822Z"}}


A URL do {{site.data.keyword.objectstorageshort}} está localizada no Catálogo de serviços. O Catálogo de serviços está contido no corpo de resposta da solicitação de token. A resposta é um catálogo completo de serviços do OpenStack que estão disponíveis. Selecione o terminal no Catálogo de serviços com o tipo de ```object-store```, região que corresponde ao campo de região nas credenciais, e a interface interna (`internalURL`) ao acessar o serviço {{site.data.keyword.objectstorageshort}} de dentro do {{site.data.keyword.Bluemix_notm}} ou a interface pública (`publicURL`) ao acessar o serviço {{site.data.keyword.objectstorageshort}} de fora do {{site.data.keyword.Bluemix_notm}}.



## Desvinculando e desprovendo o {{site.data.keyword.objectstorageshort}} {: #deprovisioning-object-storage}

### Como desprover o serviço do {{site.data.keyword.objectstorageshort}}
1.	Selecione o serviço no painel do {{site.data.keyword.Bluemix_notm}}.  
2.	Clique no ícone de engrenagem no canto superior direito e selecione **Excluir serviço**.
	
**Aviso:** se você desprover uma instância de serviço do IBM {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}}, o projeto em nuvem e a conta Swift serão excluídos. Todos os contêineres e objetos na instância desprovida serão excluídos do Swift e não poderão ser restaurados.

### Desvinculando um aplicativo ou excluindo uma chave de serviço

Se você desvincular um aplicativo da instância do {{site.data.keyword.objectstorageshort}} ou excluir a chave de serviço, as credenciais serão excluídas. A conta do {{site.data.keyword.objectstorageshort}} não será excluída até que a instância do {{site.data.keyword.objectstorageshort}} seja desprovida. É possível gerar novas credenciais de nuvem [religando ou criando uma nova chave de serviço](#bind-object-storage-to-application).

## Perguntas frequentes {: #FAQ} 

### Como os preços variam dependendo do plano que eu escolher?
A precificação varia dependendo do plano escolhido. Para obter mais informações sobre precificação, consulte a [Folha de precificação do IBM Bluemix](https://console.ng.bluemix.net/pricing/){: new_window} ou use a [Calculadora](https://console.ng.bluemix.net/?direct=classic/#/pricing/cloudOEPaneId=pricing&paneId=pricingSheet){: new_window} para obter estimativas mais detalhadas.

### Como mudar meu plano de Beta para Padrão? {: #changeplan}  
O plano Beta do serviço {{site.data.keyword.objectstorageshort}} será removido do catálogo após a Disponibilidade geral do serviço {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.objectstorageshort}}. As instâncias de serviço dos clientes NÃO são migradas do plano Beta para Padrão automaticamente. Será necessário atualizar seu plano seguindo estas etapas:

1.	Clique em **Plano** na barra de navegação esquerda na interface com o usuário do {{site.data.keyword.objectstorageshort}}.
2.	Selecione **Padrão** como o novo plano e, em seguida, clique em **Salvar**.

![Mudança de plano de precificação do {{site.data.keyword.objectstorageshort}}](images/Change_plan.png)

*Figura 5. {{site.data.keyword.objectstorageshort}} Mudança de plano de precificação*

Suas instâncias de serviço e dados do cliente são movidos para o novo plano.

Também é possível mudar seu plano de pagamento usando a interface de linha de comandos. Para obter mais informações, consulte [Como mudar seu plano](../../pricing/index.html#changing)  

**Nota:** as instâncias de serviço do plano Beta não podem ser movidas para o plano Grátis. As instâncias de serviço não migradas serão desativadas e, depois de 60 dias, excluídas. 

### Quais contas e planos de pagamento posso usar para o {{site.data.keyword.objectstorageshort}}?
O serviço {{site.data.keyword.objectstorageshort}} é fornecido com várias opções de planos. A partir de nossa liberação de disponibilidade geral, dois planos são oferecidos no momento, Padrão e Grátis. O plano Padrão está disponível somente para Contas pagas do {{site.data.keyword.Bluemix_notm}}, seja Pagamento por uso ou Assinatura, e para usuários internos da IBM.

Contas para teste que ainda estejam ativas podem usar o plano Grátis, que permite a existência de somente uma instância em uma Organização do {{site.data.keyword.Bluemix_notm}}. Depois que o tempo na avaliação do {{site.data.keyword.Bluemix_notm}} expirar, a instância de serviço associada do {{site.data.keyword.objectstorageshort}} será desativada, ou seja, a conta de armazenamento não poderá ser acessada pela interface com o usuário ou pela linha de comandos do {{site.data.keyword.Bluemix_notm}}. Depois de um período de cortesia de 30 dias, sua conta do {{site.data.keyword.Bluemix_notm}} será limpa e todos os dados excluídos. Para evitar perda de dados, recomenda-se fazer upgrade para uma Conta paga do {{site.data.keyword.Bluemix_notm}} o mais rápido possível. Para fazer upgrade de sua conta, clique no menu de gerenciamento de usuários no canto superior direito e selecione **Conta**, que fornece instruções sobre o processo de upgrade.

É possível fazer upgrade de instâncias criadas no plano Grátis para o plano Padrão com as etapas descritas em [Como mudar meu plano de Beta para Padrão?](#changeplan). Para fazer upgrade para o plano Padrão, a organização associada deve ser uma Conta paga do {{site.data.keyword.Bluemix_notm}}. Não é possível fazer upgrade de contas para teste com instâncias do {{site.data.keyword.objectstorageshort}} para o plano Padrão, e fazer downgrade de instâncias no plano Padrão para outros planos.

### Como serei encarregado e cobrado pelo meu uso do {{site.data.keyword.objectstorageshort}}?

O serviço do {{site.data.keyword.objectstorageshort}} cobra somente pelo que você usa.  Não há taxa mínima, taxas de configuração ou compromissos para iniciar o uso do serviço. Não há cobrança por solicitação de API ou tráfego de rede por dados de entrada.

Seu uso do {{site.data.keyword.objectstorageshort}} é faturado com base no uso médio de armazenamento diário por meio do ciclo de faturamento. Isto inclui todos os dados de objeto nos contêiners que foram criados em sua conta da organização no {{site.data.keyword.Bluemix_notm}}. 

Os encargos de Transferência dos dados de saída se aplicam sempre quando dados são lidos a partir de quaisquer dos seus contêiners de objetos na rede pública. Isto é faturado com base na transferência média diária pública de dados de saída por meio do ciclo de faturamento.

Os componentes de métricas para a precificação do {{site.data.keyword.objectstorageshort}} são os seguintes:
* Uso de armazenamento  - $0.04 por GB por mês
* Transferência de dados de saída pública  - $0.09 por GB por mês 

Ao final do ciclo de faturamento, o {{site.data.keyword.Bluemix_notm}}  faturará o cliente automaticamente pelo uso no período de faturamento atual. É possível visualizar seus encargos para o período atual de faturamento via relatório do {{site.data.keyword.Bluemix_notm}}.

O plano de serviço padrão que é liberado para Londres e Dallas têm a mesma precificação.

### Como a replicação de dados é executada no {{site.data.keyword.objectstorageshort}}?
O serviço do {{site.data.keyword.objectstorageshort}} mantém três cópias de seus dados que são replicados entre múltiplos nós de armazenamento. Para obter infomações adicionais, consulte o documento [OpenStack Swift Replication](http://docs.openstack.org/developer/swift/overview_replication.html){: new_window}.

># Links relacionados {:class="linklist"}
>## Referência da API {:id="api"}
>* [API do OpenStack Object Storage (Swift) v1](http://developer.openstack.org/api-ref-objectstorage-v1.html){: new_window}
>* [API do OpenStack Identity (Keystone) v3.0](http://developer.openstack.org/api-ref-identity-v3.html){: new_window}
>
># Links relacionados {:class="linklist"}
>## SDK {:id="sdk"}
>* [Kits de desenvolvimento de software (SDK) do OpenStack ](https://wiki.openstack.org/wiki/SDKs){: new_window}
>
># Links relacionados {:class="linklist"}
>## Tutoriais e amostras {:id="samples"}
>* [Conectando-se ao IBM Object Storage for Bluemix com Java](https://developer.ibm.com/recipes/tutorials/connecting-to-ibm-object-storage-for-bluemix-with-java/){: new_window}
>* [Usar Python para acessar o Bluemix Object Storage](https://developer.ibm.com/recipes/tutorials/use-python-to-access-your-bluemix-object-storage/){: new_window}
>* [Bluemix Object Storage Community](https://www.ibm.com/developerworks/community/groups/service/html/communityoverview?communityUuid=1b48459f-4091-43cb-bca4-37863606d989){: new_window}
>
># Links relacionados {:class="linklist"}
>## Tempos de execução compatíveis {:id="buildpacks"}
>* [Liberty for Java](https://www.ng.bluemix.net/docs/starters/liberty/index.html){: new_window}
>* [SDK for Node.js](https://www.ng.bluemix.net/docs/starters/nodejs/index.html){: new_window}
>* [Ir para](https://www.ng.bluemix.net/docs/starters/go/index.html){: new_window}
>* [PHP](https://www.ng.bluemix.net/docs/starters/php/index.html){: new_window}
>* [Python](https://www.ng.bluemix.net/docs/starters/python/index.html){: new_window}
>* [Ruby](https://www.ng.bluemix.net/docs/starters/rails/index.html){: new_window}
>* [Buildpacks
de comunidade](https://www.ng.bluemix.net/docs/starters/byob.html){: new_window}
>
># Links relacionados {:class="linklist"}
>## Links relacionados {:id="general"}
>* [Folha de precificação do IBM Bluemix](https://www.ng.bluemix.net/#/pricing){: new_window}
>* [Pré-requisitos do IBM Bluemix](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
>
>{:elementKind="article" id="rellinks"}
