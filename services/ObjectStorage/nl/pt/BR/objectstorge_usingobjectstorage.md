{:new_window: target="_blank"}

# Iniciar o uso do {{site.data.keyword.objectstorageshort}}  {: #using-object-storage} 

*Última atualização: 24 de junho de 2016*
{: .last-updated}


## Usando a interface com o usuário do {{site.data.keyword.objectstorageshort}} {: #using-object-storage-ui}

### Elementos de UI e navegação
Quando seu {{site.data.keyword.objectstorageshort}} estiver provisionado, será possível ver informações sobre a instância no painel de instância do serviço {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}}. No painel, selecione sua instância do {{site.data.keyword.objectstorageshort}} para visualizar o painel com informações mais detalhadas.  
#### Dados de uso
Na página inicial do aplicativo, você verá as informações de uso de armazenamento de sua instância. Ele mostra também o número atual de **Contêineres de armazenamento** e o número total de **Objetos** em todos os seus contêineres. Ele lista seu uso de memória em megabytes. **Armazenamento consumido** refere-se à quantia atual de espaço usado. 
#### Ações
Para recuperar os dados de uso mais recentes, clique no botão **Atualizar**.   
####Navegador de objetos 
Use o navegador de objeto para gerenciar os contêineres e objetos do armazenamento de objetos. É possível criar contêineres, fazer upload de arquivos, excluir contêineres e excluir arquivos entre outras ações.


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


## Usando a CLI do Swift para acessar o {{site.data.keyword.objectstorageshort}} {: #using-swift-cli}

É possível acessar o serviço {{site.data.keyword.objectstorageshort}} na Internet e a partir de aplicativos e servidores virtuais no IBM {{site.data.keyword.Bluemix_notm}}. Os casos de uso comuns para o serviço {{site.data.keyword.objectstorageshort}} são como a seguir:

* Fazendo backup dos dados de volume de suas instâncias
* Usando como um local intermediário ao transferir grandes quantias de dados
* Transferindo dados entre os ambientes que não estão diretamente conectados
* Agindo como um armazenador central

O serviço {{site.data.keyword.objectstorageshort}} baseia-se no OpenStack Swift e pode ser acessado usando qualquer aplicativo cliente compatível. Esta seção descreve como usar o cliente Python Swift, que é a interface de linha de comandos (CLI) para a API do {{site.data.keyword.objectstorageshort}} e suas extensões, para trabalhar com contêineres e arquivos.

### Instalando o cliente Swift {: #install-swift-client}

Instale o software obrigatório a seguir, se ainda não estiver instalado. Para obter mais informações, consulte a [Documentação do OpenStack](http://docs.openstack.org/user-guide/common/cli_install_openstack_command_line_clients.html#install-the-prerequisite-software){: new_window}. 
* Python 2.7 ou mais recente
* Pacote setuptools
* Pacote pip

Instale o cliente Python Swift usando o Python pip:

	sudo pip install python-swiftclient

### Configurando o Cliente {: #setup-swift-client}

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

**Nota:** certifique-se de incluir um ```/v3``` para os ```auth_url``` a partir das credenciais na interface com o usuário do {{site.data.keyword.objectstorageshort}} quando configurar as variáveis de ambiente ```OS_AUTH_URL``` para o cliente Swift.


### Trabalhando com contêineres {: #work-with-containers}

Listando contêineres:

	swift list
	
Criando um contêiner:

	swift post <container_name>
	
Listando o conteúdo de um contêiner:

	swift list <container_name>

### Trabalhando com Objetos {: #work-with-objects}

#### Incluindo um arquivo em um contêiner

	swift upload <container_name> <file_name>

#### Incluindo arquivos maiores que 5 GB em um contêiner

Se você estiver fazendo upload de um arquivo maior que 5 GB, deverá dividi-lo em chunks menores. É possível instruir o cliente Swift para manipular esse upload fornecendo o parâmetro ```-segment-size```:

	swift upload <container_name> <file_name> --segment-size <size_in_bytes>
	
Cada segmento é transferido por upload em paralelo para um contêiner separado chamado ```<container_name>_segments```. Depois que todos os segmentos são transferidos por upload, o Swift cria um arquivo manifest para que os segmentos possam ser transferidos por download em um único arquivo do contêiner original ```<container_name>``` com o nome do arquivo original ```<file_name>```.

Por exemplo, o comando a seguir faz upload de um arquivo chamado ```large_file``` de um contêiner chamado ```test_container``` com o tamanho de segmento ```1073741824```.

	swift upload test_container -S 1073741824 large_file

É possível executar o comando a seguir para fazer download do arquivo:

	swift download test_container large_file

#### Transferindo um Arquivo por Download

	swift download <container_name> <file_name>
	
#### Incluindo um diretório em um contêiner

Swift não possui uma estrutura de diretórios verdadeira, mas usa a nomenclatura para representar um layout de diretório. Para incluir um diretório em um contêiner, execute o comando a seguir:

	swift upload <container_name> <directory_name>
	
Esse comando fará upload da estrutura de diretório completa como um caminho relativo. Por exemplo, se especificar ```/mnt/volume1```, a estrutura de diretório mnt/volume1 será anexada a todos os nomes de arquivos para indicar a estrutura de diretório.

	
#### Fazendo download de um diretório

Para fazer download de uma estrutura de diretório, use o parâmetro ```-prefix``` para indicar o diretório ou a estrutura de diretório da qual você deseja fazer download.

	swift download <container_name> --prefix <directory>
	
#### Excluindo um Arquivo

	swift delete <container_name> <file_name>

### Trabalhando com versão de objetos {: #work-with-object-versioning}

É possível configurar versões de cada objeto em seu contêiner usando a sinalização ```X-Versions-Location```. Para isso, crie um contêiner adicional para manter as versões mais antigas de seus objetos como a seguir. 

Se você estiver usando o cliente swift, poderá configurá-lo dessa forma:

	swift post container_one -H "X-Versions-Location:container_two"

Se estiver usando curl, poderá configurá-lo como este:

	curl -i -X PUT -H "X-Auth-Token: <token>" -H "X-Versions-Location:container_two" https://<object-storage_url>/container_one

No exemplo, ```container_two``` foi configurado para conter as versões mais antigas de seus objetos armazenados no ```container_one```. Portanto, ```container_one``` terá a versão mais atual de seus objetos e ```container_two``` terá as versões mais antigas de seus objetos. Certifique-se de que ```container_two``` exista na ordem para que a versão funcione.

Com a versão configurada, quando você fizer upload de um objeto para o ```container_one```, se houver uma versão existente do objeto, ela será movida para o ```container_two``` pois a nova versão está criada no ```container_one```. Se você excluir um objeto do ```container_one```, a versão anterior do objeto será movida do ```container_two``` de volta para o ```container_one```.

Os objetos no ```container_two``` serão nomeados automaticamente com o formato a seguir: ```<Length><Object_name>/<Timestamp>```

```Comprimento``` refere-se ao comprimento do nome de seu objeto; é um número hexadecimal de 3 caracteres preenchido com zero. ```Object_name``` é o nome de seu objeto. ```Timestamp``` é o registro de data e hora de quando essa versão específica do objeto foi originalmente transferida por upload.

Para desativar a versão, use a sinalização ```X-Remove-Versions-Location```:

	swift post container_one -H "X-Remove-Versions-Location:"

ou

	curl -i -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Versions-Location: anyvalue" https://<object-storage_url>/container_one

Aqui está um exemplo completo do uso de versão:

1. Crie um contêiner:

		$ swift post container_one
		$

2. Configure a versão para container_one:

		$ swift post container_one -H "X-Versions-Location:container_two"
		$

3. Crie o container_two:

		$ swift post container_two
		$

4. Faça upload de um objeto pela primeira vez no container_one:

		$ swift upload container_one object
		object
		$

5. Liste objetos no container_one:

		$ swift list container_one
		object
		$

6. Liste objetos no container_two:

		$ swift list container_two
		$

7. Faça upload de uma nova versão do objeto no container_one:

		$ swift upload container_one object
		object
		$

8. Liste objetos no container_one:

		$ swift list container_one
		object
		$

9. Liste objetos no container_two:

		$ swift list container_two
		006object/1457456909.27383
		$

10. Exclua um objeto no container_one:

		$ swift delete container_one object
		object
		$

11. Liste ambos os contêineres:

		$ swift list container_one
		object
		$ swift list container_two
		$

### Planejando a exclusão de objeto {: #schedule-object-deletion}

É possível configurar seus objetos para expirar em período de tempo especificado. Ou seja, é possível planejar a exclusão de seus objetos. Isso pode ser feito usando um dos dois cabeçalhos ```X-Delete-At``` ou ```X-Delete-After```. O cabeçalho ```X-Delete-At``` usa um número inteiro que representa o período no qual excluir o objeto. O cabeçalho ```X-Delete_After``` usa um número inteiro que representa o número de segundos após os quais o objeto será excluído.

Se você estiver usando o cliente swift para fazer um post no objeto em seu contêiner, consulte os exemplos a seguir.

* Para configurar o objeto a ser excluído em "01/04/2016 8h", use o comando a seguir:

		swift post -H "X-Delete-At:1459515600" container object

* Para configurar o objeto a ser excluído em uma hora, use o comando a seguir:

		swift post -H "X-Delete-After:3600" container object

  Depois de fazer isso, o comando ```swift stat container object``` mostrará o cabeçalho ```X-Delete-At``` com a expiração apropriada no período.

* Para remover o prazo de expiração do objeto, use o comando a seguir:

		swift post -H "X-Remove-Delete-After:" container object

Se estiver usando curl, os comandos serão como a seguir. 

* Para configurar o objeto a ser excluído em "01/04/2016 8h", use o comando a seguir:

		curl -X POST -H "X-Auth-Token: <token>" -H "X-Delete-At:1459515600" https://<object-storage_url>/container/object

* Para configurar o objeto a ser excluído em uma hora, use o comando a seguir:

		curl -X POST -H "X-Auth-Token: <token>" -H "X-Delete-After:3600" https://<object-storage_url>/container/object

* Para verificar se o objeto tem o cabeçalho, use o comando a seguir:

		curl -I -H "X-Auth-Token: <token>" https://<object-storage_url>/container/object

* Para remover o prazo de expiração, use o comando a seguir:

		curl -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Delete-At:" https://<object-storage_url>/container/object

**Nota:** a exclusão real de um objeto pode não acontecer no horário exato indicado. No entanto, o objeto irá expirar, de fato, no horário especificado, ou seja, ele não será mais acessível. A exclusão real ocorrerá na próxima vez que o daemon swift-object-expirer configurado no cluster swift for executado.





### Criando uma URL provisória {: #create-temporary-url}

Uma URL provisória é uma URL longa, difícil de adivinhar que pode ser usada por um período especificado para fazer download de objetos sem requerer autenticação adicional. Gere uma URL provisória com as etapas a seguir:

1. Identifique sua conta de autenticação.
2. Configure uma chave secreta.
3. Crie a URL provisória.

#### Identificando sua conta de autenticação

O comando Swift ```stat``` imprime informações sobre sua conta:

	swift stat

Localize o campo Conta e anote a sequência completa atrás de *Conta*:, incluindo ```AUTH_```.

#### Configurando uma chave secreta

Essa chave pode ser qualquer coisa que você selecionar, mas a melhor prática é selecionar uma sequência longa, aleatória e difícil de adivinhar.

	swift post -m "Temp-URL-Key:<key>"
	
Execute o comando Swift ```stat``` para verificar se o ```Temp-URL-Key``` foi configurado com sucesso.

	swift stat


#### Criando a URL provisória

O comando Swift ```tempurl``` usa estes argumentos posicionais:

* [method] GET para permitir download. PUT para permitir upload.
* [seconds] Tempo em segundos que a URL provisória estará disponível.
* [path] O caminho completo do objeto expresso como ```/v1/<auth_account>/<container_name>/<object_name>```. Para obter mais informações, consulte a [URL do {{site.data.keyword.objectstorageshort}}](#access-points). 
* [key] A chave configurada na etapa 2.

```
swift tempurl GET <seconds> <path> <key>
```

Esse comando retornará uma URL que pode ser anexada ao nome do cluster para obter uma URL completa. Use a URL completa para fazer download do objeto com qualquer cliente HTTP compatível, como curl, wget ou Firefox.

## Usando a API REST do Swift para acessar o {{site.data.keyword.objectstorageshort}} {: #using-swift-restapi}

É possível usar a API REST do Swift com uma interface do cliente da linha de comandos, como cURL, ou chamar a API a partir do aplicativo.  

### URL do {{site.data.keyword.objectstorageshort}} {: #access-points}

Para interagir com a API do {{site.data.keyword.objectstorageshort}}, construa a URL do {{site.data.keyword.objectstorageshort}} como a seguir:

	https://<access point>/<API version>/AUTH_<project ID>/<container namespace>/<object namespace>



A URL consiste em cinco partes. A ```<API version>``` é v1. É possível localizar o ```<project ID>```, ```<container namespace>```,
e ```<object namespace>``` do {{site.data.keyword.objectstorageshort}} a partir da interface com o usuário do {{site.data.keyword.objectstorageshort}}. Para o ```<access point>```, consulte a tabela a seguir: 


| **Região**  |   **Ponto de acesso público**                     |
|-------------|-----------------------------------------------|
| Dallas      | https://dal.objectstorage.open.softlayer.com/ | 
| Londres      | https://lon.objectstorage.open.softlayer.com/ |


*Tabela 1. Ponto de acesso do {{site.data.keyword.objectstorageshort}}*


### API do {{site.data.keyword.objectstorageshort}}

Consulte a [Referência completa da API do OpenStack Swift](http://developer.openstack.org/api-ref-objectstorage-v1.html){: new_window} para obter uma lista abrangente das opções e exemplos de API REST do {{site.data.keyword.objectstorageshort}}.

## Usando o {{site.data.keyword.objectstorageshort}} em várias regiões {: #multi-regions}  

O serviço IBM {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}} suporta as regiões de armazenamento Dallas e Londres. Essas regiões de armazenamento são independentes da região do {{site.data.keyword.Bluemix_notm}}, como sul do EUA e Reino Unido, na qual a instância de serviço {{site.data.keyword.objectstorageshort}} foi criada.  Por exemplo, se você criar uma instância do {{site.data.keyword.objectstorageshort}} na região sul dos EUA do {{site.data.keyword.Bluemix_notm}}, poderá ler e gravar dados na região de armazenamento Dallas ou Londres.  

Para a região sul dos EUA do {{site.data.keyword.Bluemix_notm}}, a região de armazenamento Dallas é a padrão. Para a região Reino Unido do {{site.data.keyword.Bluemix_notm}}, a região de armazenamento Londres é a padrão.  A interface com o usuário do {{site.data.keyword.objectstorageshort}} sempre ativa a região de armazenamento padrão da região do {{site.data.keyword.Bluemix_notm}}. Para alternar regiões, clique na lista suspensa da Região do {{site.data.keyword.objectstorageshort}} e escolha outra região.

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

Use o valor do campo ```X-Subject-Token``` a partir do cabeçalho de resposta como o campo ```X-Auth-Token``` quando fizer solicitações para o serviço {{site.data.keyword.objectstorageshort}}.

A seguir está uma resposta de exemplo. A resposta foi cortada para mostrar somente as informações relevantes do {{site.data.keyword.objectstorageshort}}.

	HTTP/1.1 201 Created
	Date: Mon, 29 Feb 2016 21:03:41 GMT
	Server: Apache/2.4.6 (CentOS) OpenSSL/1.0.1e-fips mod_wsgi/3.4 Python/2.7.5
	X-Subject-Token: gAAAAABW1LIubUgqKl-eInzhZUHWEnXijp7t6_5inl4DTRLxDhNbJ25ly2X7bASNvH7ocxinaJu_kdhSfnHNRwPAeYY77Ii2Cwp02-bvxUA1S9lV_knT6EyCOW2mSBl_HuuDD2cEgdiKmyZTVt-RvDxhPKYD-rHkJz-dHO4Folg8TVXotilb1uw
	Vary: X-Auth-Token
	x-openstack-request-id: req-01e096c8-5393-4f98-8ff6-029c55e42524
	Content-Length: 12051
	Content-Type: application/json

	{
	  "token" : {
	    "roles" : [
	      {
	        "id" : "f61f06a84f6443e880210fa986bd8691",
	        "name" : "ObjectStorageOperator"
	      }
	    ],
	    "catalog" : [
	      {
	        "endpoints": [
			{
	            "id" : "20cbfa6ff22b4a67a1484d30235bfc80",
	            "region" : "london",
	            "region_id" : "london",
	            "url" : "https:\/\/lon.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "admin"
	          },
	          {
	            "id" : "38b8c081b11a452bb951698c334a406d",
	            "region" : "london",
	            "region_id" : "london",
	            "url" : "https:\/\/lon.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "internal"
	          },
	          {
	            "id" : "4207049680fa4effbecd044c7448a8cb",
	            "region" : "dallas",
	            "region_id" : "dallas",
	            "url" : "https:\/\/dal.objectstorage.open.softlayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "public"
	          },
	          {
	            "id" : "8a65a0cf38ac4211ad6a3c9c0eb337ff",
	            "region" : "london",
	            "region_id" : "london",
	            "url" : "https:\/\/lon.objectstorage.open.softlayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "public"
	          },
	          {
	            "id" : "a60cf32be624491d89170ef8264de5e8",
	            "region" : "dallas",
	            "region_id" : "dallas",
	            "url" : "https:\/\/dal.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "admin"
	          },
	          {
	            "id" : "c769862200124a308d6748e418c971ba",
	            "region" : "dallas",
	            "region_id" : "dallas",
	            "url" : "https:\/\/dal.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "internal"
	          }
	        ],
	        "id" : "896e4064cbe742afbf9a543c15f27ac0",
	        "type" : "object-store",
	        "name" : "swift"
	      },
	    ],
	    "extras" : {

	    },
	    "user" : {
	      "id" : "0b8aebd924ef4cc7aa9232f07e47e874",
	      "name" : "user_87c094ce47a9feae3a137ffcbbfa098a888c12a8",
	      "domain" : {
	        "id" : "8753ff40ac1a4f4a9f162ad8026b6ce0",
	        "name" : "757955"
	      }
	    },
	    "expires_at" : "2016-02-29T22:03:42.061343Z",
	    "audit_ids" : [
	      "cbA-iL2dSheyB72PHd7q8Q"
	    ],
	    "issued_at" : "2016-02-29T21:03:42.000000Z",
	    "project" : {
	      "id" : "3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	      "name" : "object_storage_c1d8b3a1",
	      "domain" : {
	        "id" : "8753ff40ac1a4f4a9f162ad8026b6ce0",
	        "name" : "757955"
	      }
	    },
	    "methods" : [
	      "password"
	    ]
	  }
	}


A URL do {{site.data.keyword.objectstorageshort}} está localizada no Catálogo de serviços. O Catálogo de serviços está contido no corpo de resposta da solicitação de token. A resposta é um catálogo completo de serviços do OpenStack que estão disponíveis. Selecione o terminal no Catálogo de serviços com o tipo de ```object-store``` e a região que corresponde ao campo de região nas credenciais.

**Nota:** use a interface pública (`publicURL`). A interface interna (`internalURL`) não é acessível a partir do {{site.data.keyword.Bluemix_notm}}.


## Desvinculando e desprovendo o {{site.data.keyword.objectstorageshort}} {: #deprovisioning-object-storage}

### Como desprover o serviço do {{site.data.keyword.objectstorageshort}}
1.	Selecione o serviço no painel do {{site.data.keyword.Bluemix_notm}}.  
2.	Clique no ícone de engrenagem e selecione **Excluir serviço**.
	
**Aviso:** se você desprover uma instância de serviço do IBM {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}}, o projeto em nuvem e a conta Swift serão excluídos. Todos os contêineres e objetos na instância desprovida serão excluídos do Swift e não poderão ser restaurados.

### Desvinculando um aplicativo ou excluindo uma chave de serviço

Se você desvincular um aplicativo da instância do {{site.data.keyword.objectstorageshort}} ou excluir a chave de serviço, as credenciais serão excluídas. A conta do {{site.data.keyword.objectstorageshort}} não será excluída até que a instância do {{site.data.keyword.objectstorageshort}} seja desprovida. É possível gerar novas credenciais de nuvem [religando ou criando uma nova chave de serviço](#bind-object-storage-to-application).

