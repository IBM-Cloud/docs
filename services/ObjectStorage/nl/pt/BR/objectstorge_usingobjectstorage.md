---

copyright:
  years: 2014, 2016

---

{:new_window: target="_blank"}

# Iniciar o uso do {{site.data.keyword.objectstorageshort}}  {: #using-object-storage}

*Última atualização: 13 de agosto de 2016*
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

```
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
```

## Usando a CLI de Swift para acessar o {{site.data.keyword.objectstorageshort}} {: #using-swift-cli}

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

```
	sudo pip install python-swiftclient
```

Instale o cliente do Python Keystone executando o comando a seguir:

```
	sudo pip install python-keystoneclient
```

### Configurando o Cliente {: #setup-swift-client}

O cliente Swift usa as informações sobre autenticação das variáveis de ambiente a seguir:
* `OS_AUTH_URL` é a URL de terminal
* `OS_USER_ID` é o nome do usuário
* `OS_PASSWORD` é a senha

Configure as informações sobre autenticação como a seguir.

```
export OS_USER_ID=24a20b8e4e724f5fa9e7bfdc79ca7e85
export OS_PASSWORD=aaa55AAAaaaaa]?,
export OS_PROJECT_ID=383ec90b22ff4ba4a78636f4e989d5b1
export OS_AUTH_URL=https://identity.open.softlayer.com/v3
export OS_REGION_NAME=dallas
export OS_IDENTITY_API_VERSION=3
export OS_AUTH_VERSION=3
```

É possível localizar os valores de credenciais para o serviço {{site.data.keyword.objectstorageshort}} na página **Credenciais de serviço** na interface com o usuário do {{site.data.keyword.objectstorageshort}}.

**Nota:** Certifique-se de incluir um `/v3` na `auth_url` a partir das credenciais na interface com o usuário do
{{site.data.keyword.objectstorageshort}} ao configurar as variáveis de ambiente `OS_AUTH_URL` para o cliente Swift.


### Trabalhando com contêineres {: #work-with-containers}

Listando contêineres:
```
	swift list
```
Criando um contêiner:
```
	swift post <container_name>
```
Listando o conteúdo de um contêiner:
```
	swift list <container_name>
```
### Trabalhando com Objetos {: #work-with-objects}

#### Incluindo um arquivo em um contêiner
```
	swift upload <container_name> <file_name>
```
#### Incluindo arquivos maiores que 5 GB em um contêiner

Se você estiver fazendo upload de um arquivo maior que 5 GB, deverá dividi-lo em chunks menores. É possível instruir o cliente Swift para manipular esse upload fornecendo o parâmetro `-segment-size`:
```
	swift upload <container_name> <file_name> --segment-size <size_in_bytes>
```
Cada segmento é transferido por upload em paralelo em um contêiner separado denominado `<container_name>_segments`. Após todos os segmentos serem transferidos por upload, a Swift
cria um arquivo manifest de forma que os segmentos possam ser transferidos por download em um arquivo único a partir do contêiner original `<container_name>` com o nome do arquivo
original `<file_name>`.

Por exemplo, o comando a seguir faz upload de um arquivo denominado `large_file` a partir de um contêiner denominado `test_container` com o tamanho de segmento
`1073741824`.
```
	swift upload test_container -S 1073741824 large_file
```
É possível executar o comando a seguir para fazer download do arquivo:
```
	swift download test_container large_file
```
#### Transferindo um Arquivo por Download
```
	swift download <container_name> <file_name>
```
#### Incluindo um diretório em um contêiner

Swift não possui uma estrutura de diretórios verdadeira, mas usa a nomenclatura para representar um layout de diretório. Para incluir um diretório em um contêiner, execute o comando a seguir:
```
	swift upload <container_name> <directory_name>
```
Esse comando fará upload da estrutura de diretório completa como um caminho relativo. Por exemplo, se você especificar `/mnt/volume1`, a estrutura de diretório mnt/volume1 será anexada a
todos os nomes de arquivos para indicar a estrutura de diretório.


#### Fazendo download de um diretório

Para fazer download de uma estrutura de diretório, use o parâmetro `-prefix` para indicar o diretório ou a estrutura de diretório da qual você deseja fazer download.
```
	swift download <container_name> --prefix <directory>
```
#### Excluindo um Arquivo
```
	swift delete <container_name> <file_name>
```
### Trabalhando com versão de objetos {: #work-with-object-versioning}

É possível configurar versões de cada objeto em seu contêiner usando a sinalização `X-Versions-Location`. Para isso, crie um contêiner adicional para manter as versões mais antigas de seus objetos como a seguir.

Se você estiver usando o cliente swift, poderá configurá-lo dessa forma:
```
	swift post container_one -H "X-Versions-Location:container_two"
```
Se estiver usando curl, poderá configurá-lo como este:
```
	curl -i -X PUT -H "X-Auth-Token: <token>" -H "X-Versions-Location:container_two" https://<object-storage_url>/container_one
```
No exemplo, `container_two` foi configurado para conter as versões mais velhas de seus objetos armazenados em `container_one`. Portanto, `container_one`
terá a versão mais atual de seus objetos e `container_two` terá as versões mais velhas de seus objetos. Certifique-se de que `container_two` exista para que o versionamento
funcione.

Com o versionamento configurado, ao fazer upload de um objeto no `container_one`, se houver uma versão existente do objeto, a versão existente será movida para
`container_two` conforme a nova versão for criada em `container_one`. Se você excluir um objeto do `container_one`, a versão anterior do objeto será movida
do `container_two` de volta para o `container_one`.

Objetos no `container_two` serão automaticamente denominados com o formato a seguir: `<Length><Object_name>/<Timestamp>`.

`Length` refere-se ao comprimento do nome de seu objeto; esse é um número hexadecimal de 3 caracteres, com zeros à esquerda. `Object_name` é o nome de seu objeto. `Timestamp`
é o registro de data e hora de quando essa versão específica foi originalmente transferida por upload.

Para desativar a versão, use a sinalização `X-Remove-Versions-Location`:
```
	swift post container_one -H "X-Remove-Versions-Location:"
```
ou
```
	cURL -i -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Versions-Location: anyvalue" https://<object-storage_url>/container_one
```
Aqui está um exemplo completo do uso de versão:

1. Crie um contêiner:
```
		$ swift post container_one
		$
```
2. Configure a versão para container_one:
```
		$ swift post container_one -H "X-Versions-Location:container_two"
		$
```
3. Crie o container_two:
```
		$ swift post container_two
		$
```
4. Faça upload de um objeto pela primeira vez no container_one:
```
		$ swift upload container_one object
		object
		$
```
5. Liste objetos no container_one:
```
		$ swift list container_one
		object
		$
```
6. Liste objetos no container_two:
```
		$ swift list container_two
		$
```
7. Faça upload de uma nova versão do objeto no container_one:
```
		$ swift upload container_one object
		object
		$
```
8. Liste objetos no container_one:
```
		$ swift list container_one
		object
		$
```
9. Liste objetos no container_two:
```
		$ swift list container_two
		006object/1457456909.27383
		$
```
10. Exclua um objeto no container_one:
```
		$ swift delete container_one object
		object
		$
```
11. Liste ambos os contêineres:
```
		$ swift list container_one
		object
		$ swift list container_two
		$
```

### Planejando a exclusão de objeto {: #schedule-object-deletion}

É possível configurar seus objetos para expirar em período de tempo especificado. Ou seja, é possível planejar a exclusão de seus objetos. Isso pode ser feito usando um dos dois cabeçalhos `X-Delete-At` ou `X-Delete-After`. O cabeçalho `X-Delete-At` usa um número inteiro que representa o período no qual excluir o objeto. O cabeçalho `X-Delete_After` usa um número inteiro que representa o número de segundos após os quais o objeto será excluído.

Se você estiver usando o cliente swift para fazer um post no objeto em seu contêiner, consulte os exemplos a seguir.

* Para configurar o objeto a ser excluído em "01/04/2016 8h", use o comando a seguir:
```
		swift post -H "X-Delete-At:1459515600" container object
```
* Para configurar o objeto a ser excluído em uma hora, use o comando a seguir:
```
		swift post -H "X-Delete-After:3600" container object
```
  Depois de fazer isso, o comando `swift stat container object` mostrará o cabeçalho `X-Delete-At` com a expiração apropriada no período.

* Para remover o prazo de expiração do objeto, use o comando a seguir:
```
		swift post -H "X-Remove-Delete-After:" container object
```
Se você estiver usando cURL, os comandos serão como segue.

* Para configurar o objeto a ser excluído em "01/04/2016 8h", use o comando a seguir:
```
		cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-At:1459515600" https://<object-storage_url>/container/object
```
* Para configurar o objeto a ser excluído em uma hora, use o comando a seguir:
```
		cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-After:3600" https://<object-storage_url>/container/object
```
* Para verificar se o objeto tem o cabeçalho, use o comando a seguir:
```
		cURL -I -H "X-Auth-Token: <token>" https://<object-storage_url>/container/object
```
* Para remover o prazo de expiração, use o comando a seguir:
```
		cURL -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Delete-At:" https://<object-storage_url>/container/object
```
**Nota:** a exclusão real de um objeto pode não acontecer no horário exato indicado. No entanto, o objeto irá expirar, de fato, no horário especificado, ou seja, ele não será mais acessível. A exclusão real ocorrerá na próxima vez que o daemon swift-object-expirer configurado no cluster swift for executado.





### Criando uma URL provisória {: #create-temporary-url}

Uma URL provisória é uma URL longa, difícil de adivinhar que pode ser usada por um período especificado para fazer download de objetos sem requerer autenticação adicional. Gere uma URL provisória com as etapas a seguir:

1. Identifique sua conta de autenticação.
2. Configure uma chave secreta.
3. Crie a URL provisória.

#### Identificando sua conta de autenticação

O comando Swift `stat` imprime informações sobre sua conta:
```
	swift stat
```
Localize o campo Conta e anote a sequência completa por trás de *Conta*: incluindo `AUTH_`.

#### Configurando uma chave secreta

Essa chave pode ser qualquer coisa que você selecionar, mas a melhor prática é selecionar uma sequência longa, aleatória e difícil de adivinhar.
```
	swift post -m "Temp-URL-Key:<key>"
```
Execute o comando `stat` de Swift para verificar se a `Temp-URL-Key` está configurada com sucesso.
```
	swift stat
```

#### Criando a URL provisória

O comando Swift `tempurl` usa estes argumentos posicionais:

* [method] GET para permitir download. PUT para permitir upload.
* [seconds] Tempo em segundos que a URL provisória estará disponível.
* [path] O caminho completo do objeto expresso como `/v1/<auth_account>/<container_name>/<object_name>`. Para obter mais informações, consulte a [URL do {{site.data.keyword.objectstorageshort}}](#access-points).
* [key] A chave configurada na etapa 2.

```
swift tempurl GET <seconds> <path> <key>
```

Esse comando retornará uma URL que pode ser anexada ao nome do cluster para obter uma URL completa. Use a URL completa para fazer download do objeto com qualquer cliente HTTP compatível, como curl, wget ou Firefox.

## Usando a API REST do Swift para acessar o {{site.data.keyword.objectstorageshort}} {: #using-swift-restapi}

É possível usar a API REST do Swift com uma interface do cliente da linha de comandos, como cURL, ou chamar a API a partir do aplicativo.  

### URL do {{site.data.keyword.objectstorageshort}} {: #access-points}

Para interagir com a API do {{site.data.keyword.objectstorageshort}}, construa a URL do {{site.data.keyword.objectstorageshort}} como a seguir:
```
	https://<access point>/<API version>/AUTH_<project ID>/<container namespace>/<object namespace>
```


A URL consiste em cinco partes. A `<API version>` é v1. É possível localizar o `<project ID>`, o `<container
namespace>` e o
`<object namespace>` de seu {{site.data.keyword.objectstorageshort}} a partir da interface com o usuário do {{site.data.keyword.objectstorageshort}}.  Para o
`<access point>`, consulte a tabela a seguir:


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

Para usar o serviço {{site.data.keyword.objectstorageshort}}, deve-se [autenticar no OpenStack Keystone](#keystone-authentication). Após você ser autenticado com sucesso, um
`X-Subject-Token` e os terminais do {{site.data.keyword.objectstorageshort}} estarão disponíveis na resposta.

Por exemplo, para criar um contêiner denominado `my_container` na região de armazenamento de Dallas, especifique um ponto de acesso de Dallas no comando curl, como segue:
```
	# curl -i https://dal.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAAAAABWlw5mwttbb_6G3LnTiGusyoOSEHXMG7oTnDYWN1vBZB6XAxUEhz4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5N7lEZyyKQlsgmQWcrch8VOO_OiSKKToORYR7luI-2TrR_JIVZm-8AAS6hLhk9"

	HTTP/1.1 201 Created
	Content-Length: 0
	Content-Type: text/html; charset=UTF-8
	X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
	Date: Thu, 14 Jan 2016 03:16:13 GMT
```

Para criar um contêiner denominado `my_container` na região de armazenamento de Londres, especifique um ponto de acesso de Londres no comando curl, como segue:
```
	# curl -i https://lon.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAAAAABWlw5mwttbb_6G3LnTiGusyoOSEHXMG7oTnDYWN1vBZB6XAxUEhz4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5N7lEZyyKQlsgmQWcrch8VOO_OiSKKToORYR7luI-2TrR_JIVZm-8AAS6hLhk9"

	HTTP/1.1 201 Created
	Content-Length: 0
	Content-Type: text/html; charset=UTF-8
	X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
	Date: Thu, 14 Jan 2016 03:16:13 GMT
```
**Nota:** O `X-Subject-Token` que você adquiriu de Keystone funciona em todas as regiões de armazenamento.

Para obter mais informações sobre os pontos de acesso para diferentes regiões, consulte a tabela [Ponto de acesso do Object Storage](#access-points).


## Entendendo autenticação e credenciais {: #understanding-authentication-credentials}

### Gerando credenciais do {{site.data.keyword.objectstorageshort}} sem ligar um aplicativo

Para gerar credenciais de nuvem do {{site.data.keyword.objectstorageshort}} para uso fora de um aplicativo {{site.data.keyword.Bluemix_notm}}, deve-se gerar uma chave de serviço para sua instância do {{site.data.keyword.objectstorageshort}}. É possível gerar a uma nova chave selecionando **Credenciais de serviço** na barra lateral da interface com o usuário ou usando o Cloud Foundry CLI (versão 6.11.3 ou mais recente). Depois de gerar e recuperar uma chave de serviço para sua instância do {{site.data.keyword.objectstorageshort}}, será possível usar as informações de integração de nuvem para solicitar um token Keystone usando um OpenStack SDK ou a API do OpenStack Identity e iniciar o uso da conta Swift para gerenciar objetos.

Para criar a chave usando o Cloud Foundry CLI, efetue login e execute o comando a seguir:
 ```
    cf create-service-key <object_storage_instance_name> <unique_name_for_this_key>
```
Para recuperar as credenciais de serviço do Cloud Foundry CLI, execute o comando a seguir:
```
	cf service-key <object_storage_instance_name> <unique_name_for_this_key>
```

### Projetos em nuvem e usuários
O provisionamento de uma nova instância do {{site.data.keyword.objectstorageshort}} cria um projeto Keystone isolado no IBM Public Cloud. Ao ligar um novo aplicativo à instância do {{site.data.keyword.objectstorageshort}}, é criado um novo usuário do Keystone com acesso ao projeto. Quando você desprovisiona a instância, o projeto e o usuário são excluídos.

### OpenStack Identity (Keystone) v3 {: #keystone-authentication}
A estrutura de credenciais contém um conjunto completo de atributos para permitir a escolha do método de solicitação de token do OpenStack ou o OpenStack SDK que melhor se ajusta ao seu aplicativo.

A solicitação de token v3 recomendada é uma solicitação de POST para https://identity.open.softlayer.com/v3/auth/tokens conforme mostrado no comando curl a seguir:
```
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
```
Use o valor do campo `X-Subject-Token` a partir do cabeçalho de resposta como o campo `X-Auth-Token` quando fizer solicitações para o serviço {{site.data.keyword.objectstorageshort}}.

A seguir está uma resposta de exemplo. A resposta foi cortada para mostrar somente as informações relevantes do {{site.data.keyword.objectstorageshort}}.

	HTTP/1.1 201 Created
	Date: Mon, 29 Feb 2016 21:03:41 GMT
	Server: Apache/2.4.6 (CentOS) OpenSSL/1.0.1e-fips mod_wsgi/3.4 Python/2.7.5
	X-Subject-Token: gAAAAABW1LIubUgqKl-eInzhZUHWEnXijp7t6_5inl4DTRLxDhNbJ25ly2X7bASNvH7ocxinaJu_kdhSfnHNRwPAeYY77Ii2Cwp02-bvxUA1S9lV_knT6EyCOW2mSBl_HuuDD2cEgdiKmyZTVt-RvDxhPKYD-rHkJz-dHO4Folg8TVXotilb1uw
	Vary: X-Auth-Token
	x-openstack-request-id: req-01e096c8-5393-4f98-8ff6-029c55e42524
	Content-Length: 12051
	Content-Type: application/json
```
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
```

A URL do {{site.data.keyword.objectstorageshort}} está localizada no Catálogo de serviços. O Catálogo de serviços está contido no corpo de resposta da solicitação de token. A resposta é um catálogo completo de serviços do OpenStack que estão disponíveis. Selecione
o terminal a partir do Catálogo de serviços com o tipo `object-store` e a região que corresponde ao campo de região nas credenciais.

**Nota:** use a interface pública (`publicURL`). A interface interna (`internalURL`) não é acessível a partir do {{site.data.keyword.Bluemix_notm}}.



## Protegendo arquivos com controle de acesso de baixa granularidade {: #fine-grained-access-control}

Listas de controle de acesso de baixa granularidade ajudam a proteger arquivos quando você tiver múltiplos usuários que armazenem arquivos no mesmo contêiner.

Nota: Procedimentos que são esboçados nesse doc requerem a CLI de Swift. Para obter mais informações, consulte
[ usando o {{site.data.keyword.objectstorageshort}} com a CLI de Swift](https://console.ng.bluemix.net/docs/services/ObjectStorage/objectstorge_usingobjectstorage.html#using-swift-cli).


### Tipos de acesso {: #access-types}

O acesso ao serviço é controlado por funções de usuário e listas de controle de acesso de contêiner. Usuários do {{site.data.keyword.objectstorageshort}} podem ser administrativos ou não
administrativos. Listas de controle de acesso são ativadas por usuários administrativos no nível de contêiner e não estão disponíveis para a instância de serviço, conta de armazenamento ou no nível de projeto.

<table>
  <tr>
    <th> Usuários administrativos (administradores) </th>
    <th> Usuários não administrativos (membros) </th>
  </tr>
  <tr>
    <td> Gerenciar controle de acesso </td>
    <td> Por padrão, sem acesso ao serviço ou aos seus contêineres </td>
  </tr>
  <tr>
    <td> Podem criar e excluir contêineres </td>
    <td> Podem executar ações com base nas ACLs de leitura/gravação de contêineres </td>
  </tr>
  <tr>
    <td> Podem ler e gravar em contêineres </td>
    <td> Podem executar ações conforme determinado pelo administrador </td>
  </tr>
</table>

*Tabela 1: funções de usuário definidas*

É possível gerenciar usuários do {{site.data.keyword.objectstorageshort}} por meio da interface com o usuário do {{site.data.keyword.Bluemix_notm}}, da API do Cloud Foundry ou da CLI do
Cloud Foundry.



### Gerando credenciais de serviço do {{site.data.keyword.objectstorageshort}} {: #generating}

A partir do console do {{site.data.keyword.Bluemix_notm}}, é possível gerar novas credenciais de serviço para os usuários do {{site.data.keyword.objectstorageshort}}.  Para ver o novo
console, clique em **Tentar o novo {{site.data.keyword.Bluemix_notm}}**.

1.  Efetue login no {{site.data.keyword.Bluemix_notm}} como um usuário com função de desenvolvedor. Deve-se estar localizado dentro do espaço da instância de serviço que você deseja gerenciar.
2. Clique na guia **Credenciais de serviço**.
3. Clique em **Nova credencial**.
4. Forneça um nome para a credencial.
5. No campo de texto **Incluir parâmetros de configuração sequenciais**, insira as informações de credenciais para a função que você deseja criar. As informações devem ser
formatadas como uma carga útil de JSON.
  - Para criar um usuário administrativo: `{"role":"admin"}`
  - Para criar um usuário não administrativo: `{"role":"member"}`
5. Clique em ** Adicionar**.

Para gerar credenciais de serviço usando comandos cURL ou a CLI de Swift é possível usar as etapas a seguir.

1. Efetue login no {{site.data.keyword.Bluemix_notm}} como um usuário com função de desenvolvedor. Deve-se estar localizado dentro do espaço da instância de serviço que você deseja gerenciar.

  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```

2. Gere credenciais de serviço. `service-key-name` será o nome de sua credencial. É possível usar o comando do Cloud Foundry ou o comando cURL.

  Comando do Cloud Foundry:
  ```
  cf create-service-key "<object_storage_service_instance_name>" <service-key-name> -c '{"role":"<object_storage_role>"}'
  ```

  Exemplo:

  ```
  cf create-service-key "Object-Storage-AclTest" GeorgeKey -c '{"role":"member"}'

  ```
  Comando cURL:
  ```
  curl "https://api.ng.bluemix.net/v2/service_keys" -d '{   "service_instance_guid": "<service_instance_guid>",   "name": "<user_name>", "role": "member"}' -X POST -H "Authorization: <bearer_token>" -H "Content-Type: " -H "Cookie: "
  ```

3. Valide as credenciais para Chave de serviço que você criou.

  Comando do Cloud Foundry:
  ```
  cf service-key <service_key_name> <member_name>
  ```
  Exemplo:
  Criando uma chave de serviço para uma instância de serviço denominada Object-Storage-Acl-Test.
  ```
  {
    "auth_url": "https://identity.open.softlayer.com",
    "domainId": "8753ff40ac1a4f4a9f162ad8026b6ce0",
    "domainName": "757955",
    "password": "xxxxxxxx",
    "project": "object_storage_6046b6e2_ee53_4884_916f_89c65e4d408e",
    "projectId": "c727d7e248b448f6b268f31a1bd8691e",
    "region": "dallas",
    "role": "member",
    "userId": "3c5b516655e4479881d3d216895faedb",
    "username": "member_2afbeea1d58b1867f46c699553d1e4513e7df83a"
  }
  ```
  Comando cURL:
  ```
  curl "https://api.ng.bluemix.net/v2/service_instances/b9656309-d994-4dec-a71f-8eac6e2fc7dc/service_keys" -X GET  -H "Authorization: <bearer_token>" -H "Cookie: "
  ```



### Designando acesso {: #assigning-access}  

Apenas um usuário do {{site.data.keyword.objectstorageshort}} com uma função administrativa pode conceder acesso de leitura ou gravação a um contêiner para outro usuário.

Para conceder acesso de leitura na CLI use a opção `--read-acl` ou `-r`.

1. Autentique as suas credenciais usando as informações nas credenciais de serviço que você criou.  Você receberá a sua URL de Armazenamento de objeto e o token de autenticação como um resultado.

  Comando Swift:
  ```
  export OS_USER_ID=<user_id>
  export OS_PASSWORD=<password>
  export OS_TENANT_ID=<project_id>
  export OS_AUTH_URL=https://identity.open.softlayer.com/v3
  export OS_REGION_NAME=<region>
  export OS_IDENTITY_API_VERSION=3
  export OS_AUTH_VERSION=3

  swift auth
  ```
  Comando cURL:
  ```
  curl -i -H "X-Auth-User: <user_id>" -H "X-Auth-Key: <password>" <auth_url>
  ```
3. Conceda acesso de leitura executando o comando a seguir:

  Comando Swift:
  ```
  swift post <container_name> --read-acl "<user_id>:<project_id>"
  ```
  Comando cURL:
  ```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: <tenant_id>:<project_id>" -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```
4. Verifique o valor de ACL de leitura.

  Comando Swift:
  ```
  swift stat <container_name>
  ```
  Comando cURL:
  ```
  curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token:<OS_AUTH_TOKEN>"
  ```
  Exemplo de saída:
  ```
  HTTP/1.1 204 No Content
  Content-Length: 0
  X-Container-Object-Count: 1
  Accept-Ranges: bytes
  X-Storage-Policy: standard
  X-Container-Read: c727d7e248b448f6b268f31a1bd8691e:3c5b516655e4479881d3d216895faedb
  X-Container-Bytes-Used: 31512
  X-Timestamp: 1462818314.11220
  Content-Type: text/plain; charset=utf-8
  X-Trans-Id: txad7fe001da274b9ba39a6-005772e4d6
  Date: Tue, 28 Jun 2016 20:57:58 GMT
  ```

É possível manipular combinações de ACL de leitura.

<table>
  <tr>
    <th> Permissão </th>
    <th> Opções de ACL de leitura </th>
  </tr>
  <tr>
    <td> Ler para todas as referências, independentemente da conta de filiação </td>
    <td> `.r,*` </td>
  </tr>
  <tr>
    <td> Ler e listar para todas as referências e listagens </td>
    <td> `.r:*,.rlistings` </td>
  </tr>
  <tr>
    <td> Ler e listar para um usuário especificado em um projeto específico </td>
    <td> `< project_id>:< user_id>` </td>
  </tr>
  <tr>
    <td> Ler e listar para um usuário especificado em cada projeto </td>
    <td> `<*>:< user_id>` </td>
  </tr>
  <tr>
    <td> Ler e listar para cada usuário em um projeto específico </td>
    <td> `< project_id>:<*>` </td>
  </tr>
  <tr>
    <td> Ler e listar para cada usuário em cada projeto  </td>
    <td> `<*>:<*>` </td>
  </tr>
</table>

*Tabela 2: permissões de acesso de leitura por opção*

Nota: use uma vírgula (,) para separar listas de controle de acesso. Por exemplo, `-read-acl project id:user_id1, project_id2:user_id2`.


Para conceder acesso de gravação use a opção `--write-acl` ou `-w` por meio da CLI de Swift.

1. Autentique as suas credenciais usando as informações nas credenciais de serviço que você criou.  Você receberá a sua URL de Armazenamento de objeto e o token de autenticação como um resultado.

  Comando Swift:
  ```
  export OS_USER_ID="<user_id>"
  export OS_PASSWORD="<password>"
  export OS_TENANT_ID=<tenant_id>
  export OS_AUTH_URL=https://identity.open.softlayer.com/v3
  export OS_REGION_NAME=<region>
  export OS_IDENTITY_API_VERSION=3
  export OS_AUTH_VERSION=3

  swift auth
  ```
  Comando cURL:
  ```
  curl -i -H "X-Auth-User:< user_id>" -H "X-Auth-Key:< password>" https://identity.open.softlayer.com/v3
  ```
2. Conceda acesso de gravação executando o comando a seguir:

  Comando Swift:
  ```
  swift post <container_name> --write-acl "<user_id>:<project_id>"
  ```
  Comando cURL:
  ```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: <user_id>: <project_id>" -H "X-Auth-Token:<OS_AUTH_TOKEN>"

  ```
3. Verifique o valor de ACL de gravação.

  Comando Swift:
  ```
  swift stat <container_name>
  ```
  Comando cURL:
  ```
  curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token:<OS_AUTH_TOKEN>"
  ```


É possível manipular combinações de ACL de gravação.

<table>
  <tr>
    <th> Permissão </th>
    <th> Opções de ACL de gravação </th>
  </tr>
  <tr>
    <td> Gravar para um usuário especificado em um projeto específico </td>
    <td> `< project_id>:< user_id>` </td>
  </tr>
  <tr>
    <td> Gravar para um usuário especificado em cada projeto </td>  
    <td> `*:<user_id>` </td>
  </tr>
  <tr>
    <td> Gravar para cada usuário em um projeto específico </td>
    <td> `< project_id>:<*>` </td>
  </tr>
  <tr>
    <td> Gravar para cada usuário em cada projeto </td>
    <td> `<*>:<*>` </td>
  </tr>
</table>

*Tabela 3: permissões de acesso de gravação por opção*

Nota: use uma vírgula (,) para separar listas de controle de acesso. Por exemplo, `-write-acl project id:user_id1, project_id2:user_id2`.




### Removendo o acesso {: #removing-access}

Para remover ACLs de leitura de um contêiner:

  Comando Swift:
  ```
  swift post <container_name> --read-acl “”
  ```
  Comando cURL:
  ```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```

Para remover ACLs de gravação de um contêiner:

  Comando Swift:
  ```
  swift post <container_name> --write-acl “”
  ```
  Comando cURL:
  ```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```

Para verificar se você removeu uma ACL:

  Comando Swift:
  ```
  swift stat <container_name>
  ```

  Exemplo de saída:
  ```
         Account: AUTH_c727d7e248b448f6b268f31a1bd8691e
       Container: Test
         Objects: 1
           Bytes: 31512
        Read ACL:
       Write ACL:
         Sync To:
        Sync Key:
   Accept-Ranges: bytes
X-Storage-Policy: standard
     X-Timestamp: 1462818314.11220
      X-Trans-Id: txf04968bc9ef8431982b77-005772e34b
    Content-Type: text/plain; charset=utf-8

  ```
  Comando cURL:
  ```
  curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```




## Desvinculando e desprovendo o {{site.data.keyword.objectstorageshort}} {: #deprovisioning-object-storage}

### Como desprover o serviço do {{site.data.keyword.objectstorageshort}}
1.	Selecione o serviço no painel do {{site.data.keyword.Bluemix_notm}}.  
2.	Clique no ícone de engrenagem e selecione **Excluir serviço**.

**Atenção:** se você desprover uma instância de serviço do IBM {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}}, o projeto em nuvem e a
conta de Swift serão excluídos. Todos os contêineres e objetos na instância desprovida serão excluídos do Swift e não poderão ser restaurados.

### Desvinculando um aplicativo ou excluindo uma chave de serviço

Se você desvincular um aplicativo da instância do {{site.data.keyword.objectstorageshort}} ou excluir a chave de serviço, as credenciais serão excluídas. A conta do {{site.data.keyword.objectstorageshort}} não será excluída até que a instância do {{site.data.keyword.objectstorageshort}} seja desprovida. É possível gerar novas credenciais de nuvem [religando ou criando uma nova chave de serviço](#bind-object-storage-to-application).
