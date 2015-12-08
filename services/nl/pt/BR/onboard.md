{:shortdesc: .shortdesc} 
{:new_window: target="_blank"}

# Integrando um serviço com o {{site.data.keyword.Bluemix_notm}}
{: #v2api}
Última atualização: 11 de novembro de 2015

Para construir serviços e para integrá-los ao {{site.data.keyword.Bluemix}}, deve-se implementar seus serviços, implementar os brokers de serviço para os serviços e, em seguida, registrar os brokers de serviços com o {{site.data.keyword.Bluemix_notm}}. 

Os brokers de serviço são serviços da web RESTful que estendem seus serviços e integram seus serviços ao {{site.data.keyword.Bluemix_notm}}. Os brokers de serviço no {{site.data.keyword.Bluemix_notm}} fornecem os recursos a seguir:
* Preencha o catálogo de serviços que é exibido na interface com o usuário do {{site.data.keyword.Bluemix_notm}} e na saída do comando **cf marketplace**.
* Disponibilize seus serviços para os aplicativos no {{site.data.keyword.Bluemix_notm}} respondendo a solicitações como fornecimento e ligação. Após uma instância do serviço ser provisionada e ligada a um aplicativo usando o broker de serviço, o aplicativo pode interagir com a instância de serviço diretamente sem o broker de serviço.

Os brokers de serviço suportam dois tipos de serviços a serem integrados com o {{site.data.keyword.Bluemix_notm}}: serviços regulares do {{site.data.keyword.Bluemix_notm}} que existem no {{site.data.keyword.Bluemix_notm}} e serviços fornecidos pelo usuário que são provisionados fora do {{site.data.keyword.Bluemix_notm}}.

Os brokers de serviço são implementados usando a API do broker de serviço Cloud Foundry. Para obter uma visão geral de como a API do broker de serviço funciona, veja a seção **Visão geral da API** da página [API do broker de serviço](http://docs.cloudfoundry.org/services/api.html) na documentação do Cloud Foundry.

**Nota:** Se você desejar ativar o serviço em um ambiente {{site.data.keyword.Bluemix_notm}} Dedicated, veja [Tornando os serviços acessíveis a partir de Dedicated](../MCCP/index.html) para obter detalhes.

## Visão geral de construção e integração de serviços

É possível construir seu próprio serviço e integrá-lo ao {{site.data.keyword.Bluemix_notm}}.

O processo para construir e integrar um serviço ao {{site.data.keyword.Bluemix_notm}} consiste nas tarefas a seguir:
1. Implemente seu serviço.
   Para construir um serviço e integrá-lo ao {{site.data.keyword.Bluemix_notm}}, deve-se implementar a funcionalidade de seu serviço primeiro. É possível criar e implementar seu serviço como um aplicativo no {{site.data.keyword.Bluemix_notm}}. Para obter informações sobre como criar um aplicativo no {{site.data.keyword.Bluemix_notm}}, veja [Criando aplicativos da Web](https://www.stage1.eu-gb.bluemix.net/docs/starters/index.html); para obter informações sobre a implementação de um aplicativo no {{site.data.keyword.Bluemix_notm}}, veja [Implementando aplicativos usando o comando cf](https://www.stage1.eu-gb.bluemix.net/docs/manageapps/deployingapps.html#dep_apps).
2. Implemente seu broker de serviço. 
   Para permitir que seu broker de serviço se comunique com o {{site.data.keyword.Bluemix_notm}} usando as chamadas API REST, deve-se implementar os terminais de API de Catálogo, Provisionar e Desprovisionar. Por meio desses terminais, você é solicitado a fornecer recursos para seu serviço, como documentação, imagens de ícone, um guia de Iniciação Rápida e a URL para o iframe de administração que fornece a interface com o usuário para instâncias de serviço. 
   
   Se o seu serviço puder ser ligado a aplicativos no {{site.data.keyword.Bluemix_notm}}, também deve-se implementar os terminais Ligar e Desvincular.
   
   Para obter mais informações, veja [Implementando um broker de serviço](./index.html#implementing-a-service-broker).
  
3. Registre seu broker de serviço no {{site.data.keyword.Bluemix_notm}}. 
   Use a interface de linha de comandos **cloud-cli** para registrar o broker de serviço. Para obter mais informações, veja [Registrando o broker de serviço](./index.html#registering-the-service-broker).
   
Depois que você tiver integrado seu serviço ao {{site.data.keyword.Bluemix_notm}}, é possível localizar o serviço na saída do comando **cf marketplace**. Também é possível localizar o serviço no catálogo de serviços da interface com o usuário do {{site.data.keyword.Bluemix_notm}}. O serviço está sob a categoria do serviço que você especificou no campo de tag do JSON de definição de serviço.


## Exemplo: Construindo e integrando um serviço

É possível tentar um serviço de amostra para ver como construir e integrar um serviço ao {{site.data.keyword.Bluemix_notm}}. A API do broker de serviço já está implementada no código dos serviços de amostra.

Para construir e integrar um serviço de amostra ao {{site.data.keyword.Bluemix_notm}}, conclua as etapas a seguir:
1. Faça download dos serviços de amostra que são listados em [Tutoriais e amostras](./index.html#tutorials-and-samples). 
2. Implemente o serviço de amostra no {{site.data.keyword.Bluemix_notm}}. Para obter mais informações sobre a implementação de um aplicativo no {{site.data.keyword.Bluemix_notm}}, veja [Implementando aplicativos usando o comando cf](https://www.stage1.eu-gb.bluemix.net/docs/manageapps/deployingapps.html#dep_apps).
3. Crie um JSON de definição de broker de serviço. Para obter mais informações, veja [Definição de broker de serviço](./index.html#service-broker-definition).
4. Registre a definição de broker de serviço no {{site.data.keyword.Bluemix_notm}} usando o comando **cloud-cli create-service-broker**. Para obter mais informações, veja [Registrando o broker de serviço](registering-the-service-broker).

Depois que você tiver integrado um serviço de amostra ao {{site.data.keyword.Bluemix_notm}}, é possível localizar o serviço de amostra na saída do comando **cf marketplace** e no catálogo de serviço da interface com o usuário do {{site.data.keyword.Bluemix_notm}}. 


## Implementando um Broker de Serviço
{: #v2impl}

Para implementar um broker de serviço no {{site.data.keyword.Bluemix_notm}}, deve-se implementar a API do broker de serviço Cloud Foundry. A API do broker de serviço é um conjunto de terminais REST que são consumidos pelo {{site.data.keyword.Bluemix_notm}}.
1. Forneça autenticação para solicitações de HTTP que o {{site.data.keyword.Bluemix_notm}} envia para seu broker de serviço.
   O {{site.data.keyword.Bluemix_notm}} se autentica com seu broker de serviço usando a autenticação básica HTTP, portanto, deve-se fornecer um método de autenticação ao implementar seu broker de serviço. E deve-se verificar o nome do usuário e a senha no cabeçalho de autenticação de solicitações de HTTP que o {{site.data.keyword.Bluemix_notm}} envia a você. Se o nome do usuário e a senha forem inválidos, deve-se retornar uma mensagem 401 Desautorizado.
   
   **Nota:** Ao registrar o broker de serviço, deve-se fornecer o nome do usuário e a senha usados para autenticação no JSON de definição de seu broker de serviço. Para obter mais informações sobre o JSON de definição, veja [Definição de broker de serviço](./index.html#service-broker-definition).

2. Implemente os terminais de API para o broker de serviço. 
   Em seu código, deve-se processar solicitações de HTTP e fornecer respostas relacionados para os terminais de API Catálogo, Provisionar e Desprovisionar, de acordo com a especificação da API para brokers de serviço no {{site.data.keyword.Bluemix_notm}}. Para obter informações sobre os terminais de API, veja [Referência da API REST](./index.html#rest-api-reference). 
   
   Para serviços de amostra que implementam os terminais de API para Java&trade, Node.js e Ruby, veja [Tutoriais e amostras} (./index.html#tutorials-and-samples). 
   
3. Forneça mensagens de erro para o broker de serviço que são exibidas na interface com o usuário do {{site.data.keyword.Bluemix_notm}} quando ocorrem erros.
   Para fornecer mensagens de erro para os terminais do broker de serviço, deve-se retornar um objeto JSON com uma entrada de descrição. Por exemplo: 
   ```
   {
  "description" : "O serviço falhou devido à autorização inválida"
   }
   ```

   
## Registrando o broker de serviço
{: #v2reg}

Após a implementação do broker de serviço, deve-se registrá-lo no {{site.data.keyword.Bluemix_notm}}.

Para registrar um broker de serviço no {{site.data.keyword.Bluemix_notm}}, deve-se concluir as tarefas a seguir: 
1. Crie a definição de broker de serviço em um arquivo JSON. Para obter mais informações, veja [Definição de broker de serviço](./index.html#service-broker-definition).
2. Certifique-se de fornecer metadados de serviço, um guia de Iniciação Rápida, as imagens de ícone de serviço e a documentação para concluir o resultado do Catálogo (GET) para o serviço. Para obter mais informações, veja [Referência da API REST](./index.html#rest-api-reference).
3. Prepare a interface com o usuário do serviço usando um iframe para integrar à interface com o usuário do {{site.data.keyword.Bluemix_notm}}. Para obter mais informações, veja [Suporte de iframe de administração](./index.html#administration-iframe-support).
4. Use a interface de linha de comandos **cloud-cli** para registro.
   1. Especifique o host e a porta em que o {{site.data.keyword.Bluemix_notm}} está em execução, inserindo o comando de destino a seguir:
      ```
	  cloud-cli target https://console.{{site.data.keyword.domainname}}
	  ```
   2. Efetue login no {{site.data.keyword.Bluemix_notm}} usando um nome de usuário registrado e uma senha:
      ```
	  cloud-cli login -userID example@bluemix.net -pw password
	  ```
   3. Insira o comando **cloud-cli create-service-broker** para registrar o broker de serviço no {{site.data.keyword.Bluemix_notm}}:
      ```
	  cloud-cli create-service-broker sample_broker.json
	  ```
   4. Insira o comando **cf marketplace** para verificar se a oferta de serviço existe:
      ```
      cf marketplace
          service       version   provider  plans    description 
          mongodb       2.2       core      100      MongoDB NoSQL database 
          mysql         5.5       core      100      MySQL database      
                        
          Sample        0.1       ace       100      Um serviço hello world de amostra. Somente uso instrutivo, não para uso na produção.
          postgresql    9.1       core      100      Banco de dados PostgreSQL (vFabric)                
          rabbitmq      2.8       core      100      Fila de mensagens RabbitMQ	  
      ```		
      **Nota:** Também é possível especificar o destino e as credenciais do {{site.data.keyword.Bluemix_notm}} toda vez que você inserir um comando **cloud-cli**; entretanto, se você especificar o destino e as informações de login do {{site.data.keyword.Bluemix_notm}} antes de executar outros comandos **cloud-cli**, o destino e as informações de login poderão ser salvos para que não seja necessário especificar as informações na próxima vez que você inserir um comando **cloud-cli**.
	  
	  A oferta de serviços agora está disponível no {{site.data.keyword.Bluemix_notm}} e os aplicativos podem provisionar e se ligar a ela.
	  
	  O uso dos comandos **cloud-cli** podem ser acessados por meio da opção de ajuda:
	  ```
	  cloud-cli help
	  ```
	  A interface de linha de comandos cloud-cli também fornece mais ajuda para cada comando, especificando o comando a seguir:
	  ```
	  cloud-cli help `commandName`
	  ```
	  
**Nota:**

O registro de serviço é restrito. Embora qualquer um esteja livre para registrar um novo serviço, há restrições sobre quem tem permissão para ver o serviço. Os novos serviços não devem usar curingas como um asterisco (*) na propriedade **acls.wildcards** quando os serviços estão sendo registrados. Em vez disso, os novos serviços são restritos a listar explicitamente seus usuários com base em seus endereços de e-mail. Se você deseja que seu serviço esteja mais amplamente disponível, envie um e-mail para a lista de distribuição `cloudoe-admin@us.ibm.com` para solicitar que as listas ACL de seu serviço sejam modificadas.

Se você tentar registrar um serviço com curingas, ele será rejeitado com uma mensagem de erro **Desautorizado**.

Os serviços que podem estar amplamente disponíveis **devem** atender aos critérios a seguir:
* Incluir um ícone que possa ser exibido na interface com o usuário do {{site.data.keyword.Bluemix_notm}}.
* Incluir um texto de descrição que possa ser exibido na interface com o usuário do {{site.data.keyword.Bluemix_notm}}.
* Incluir uma documentação que seja referenciada pela propriedade **docURL**.
* Incluir informações de contato como parte da documentação no caso de as pessoas terem perguntas ou problemas com seu serviço.


## Atualizando o broker de serviço com a interface de linha de comandos cloud-cli
{: #v2update}

Depois de definir o broker de serviço e registrá-lo no {{site.data.keyword.Bluemix_notm}}, é possível atualizar o broker de serviço usando a interface de linha de comandos **cloud-cli**. Por exemplo, é possível atualizar os campos no arquivo JSON de definição do broker de serviço e também atualizar os campos na resposta JSON de GET /v2/catalog.

Use o comando a seguir para atualizar o broker de serviço:
```
cloud-cli update-service-broker serviceBrokerJsonFile
```

Nesse comando, serviceBrokerJsonFile é o arquivo JSON para o broker de serviço.

Caso deseje renomear o broker de serviço, use a opção originalName e especifique o nome original do broker de serviço com essa opção. Para obter mais informações sobre os comandos **cloud-cli**, veja [Comandos cloud-cli](https://www.stage1.eu-gb.bluemix.net/docs/cli/cloudcli.html).


## Criando uma extensão
{: #create_extension}

É possível declarar um serviço V2 como uma extensão, incluindo um bloco de extensão na seção de metadados da definição JSON desse serviço.

A interface com o usuário do {{site.data.keyword.Bluemix}} suporta extensões do {{site.data.keyword.Bluemix_notm}}. Uma extensão é modelada como um serviço, em vez de um bloco de construção no código de aplicativos, para oferecer suporte aos aplicativos em um espaço. Exemplos de extensões do {{site.data.keyword.Bluemix_notm}} incluem Agile Planning, Auto-scaling, APM, MQA e assim por diante.

**Nota:** O {{site.data.keyword.Bluemix_notm}} não suporta a criação de uma extensão do broker de serviço V1.
```
{ "services" :
      [{
          // "bindable" aplica-se a todos os serviços, mas as extensões em particular são mais prováveis de configurar "bindable" como false
         "bindable" : true,
         "description" : "Descrição da extensão",
         "id" : "a_unique_id1",
         "name" : "Meu nome de extensão",
         // A inclusão de "bluemix_extensions" em "tags" é recomendada
         "tags" : ["bluemix_extensions"],
         "metadata" : { 
              // A presença do bloco "extension" instrui a interface com o usuário do Bluemix que o serviço deve ser tratado como uma extensão na UI
              "extension" : {
              },
                ...
          },
        ...
       }
     ]}
```

Os serviços que são declarados como extensões são tratados de forma diferente dos serviços normais. Apenas uma instância da extensão pode ser criada dentro de um espaço. (Isso é impingido pela interface com o usuário do {{site.data.keyword.Bluemix_notm}}, não pela linha de comandos cf.) Se você ligar uma extensão a um aplicativo e uma instância da extensão já tiver sido criada no espaço do aplicativo, a instância existente da extensão será reutilizada.


## Fornecendo metadados convertidos
{: #translation}

O texto traduzível que é exibido na interface com o usuário do {{site.data.keyword.Bluemix_notm}} inclui sequências de texto para serviços, iniciadores, planos de suporte e planos de tempo de execução. Após a tradução das sequências de texto nos metadados de seu serviço ou iniciador, é possível fornecer as sequências de texto traduzidas para a interface com o usuário do {{site.data.keyword.Bluemix_notm}} usando o campo metadata.i18n.

As sequências de texto que são exibidas na interface com o usuário do {{site.data.keyword.Bluemix_notm}} podem ser traduzidas para os idiomas que estão listados na tabela a seguir. Quando a tradução é fornecido, o código do idioma para o idioma específico deve ser especificado nos metadados.

*Tabela 1. Idiomas suportados*

Linguagem | Código de idioma
----- | -----
Chinês (simplificado) | zh-Hans
Chinês (tradicional) | zh-Hant
Francês | fr
Alemão | de
Italiano | it
Japonês | ja
Coreano | ko
Português (Brasil) | pt-BR
Espanhol | es

Para fornecer sequências de texto traduzidas para o {{site.data.keyword.Bluemix_notm}}, deve-se usar o campo i18n que contém os campos de metadados relacionados à tradução na definição de seu serviço ou iniciador. 

Consulte as orientações a seguir quando incluir sequências de texto traduzidas no campo metadata.i18n:

* O campo metadata.i18n deve conter os códigos de idioma como chaves no hash de objeto.
* A estrutura dos metadados para cada código de idioma deve ser a mesma que a estrutura do metadados de nível superior. Isso permite que as sequências traduzidas sobrescrevam as sequências do idioma inglês que estão nos metadados de nível superior. As sequências traduzidas podem então ser exibidas na interface com o usuário do {{site.data.keyword.Bluemix_notm}}.
* As sequências traduzidas devem incluir o ID de cada plano. Isso permite que o plano convertido sobrescreva a versão do idioma inglês do plano que está especificada no nível superior.

Use as etapas a seguir ao fornecer as sequências de texto traduzidas na interface com o usuário do {{site.data.keyword.Bluemix_notm}}.

* Se você for um provedor de serviços, é possível fornecer sequências de texto traduzidas nos metadados do serviço. 
  As sequências traduzidas devem ser retornadas no campo metadata.i18n do resultado GET /v2/catalog para a definição de serviço.
  
  Veja a sequência JSON a seguir como um exemplo de uma definição de serviço que contém o campo metadata.i18n:
  ```
  {
    "services": [
        {
            "id": "766fa866-a950-4b12-adff-c11fa4cf8fdc",
            "name": "cloudamqp",
            "description": "Servidores HA RabbitMQ gerenciados na nuvem",
            "metadata": {
                "displayName": "CloudAMQP",
                "longDescription": "Cluster RabbitMQ gerenciados, altamente disponíveis, na nuvem",
                "providerDisplayName": "84codes AB",
                "instructionsUrl": "/path/to/instructions.md",
                "i18n": {
                    "fr": {
                        "description": ...,
                        "metadata": {
                            "displayName": ...,
                            "longDescription": ...,
                            "providerDisplayName": ...
                            "instructionsUrl": "/path/to/fr/instructions.md"
                        },
                        "plans": [
                            "id": "024f3452-67f8-40bc-a724-a20c4ea24b1c",
                            "description": ...,
                            "metadata": {
                                "bullets": [
                                    "20 GB de mensagens des",
                                    "..."
                                ],
                                "costs": [
                                     {
                                       "unitId": "INSTANCES_PER_MONTH",
                                       "unit": "MONTHLY",
                                       "partNumber": "D15UTLL"
                                      }
                                  ],             
                                "displayName": ...
                            }
                        ],
                        
                    },
                    "de": {
                        ...
                    },
                    ...
                }
            },
            "plans": [
                {
                    "id": "024f3452-67f8-40bc-a724-a20c4ea24b1c",
                    "name": "bunny",
                    "description": "Um plano médio",
                    "metadata": {
                        "bullets": [
                            "20 GB de mensagens",
                            "20 conexões"
                        ],
                        "costs": [
                            {
                              "unitId": "INSTANCES_PER_MONTH",
                              "unit": "MONTHLY",
                              "partNumber": "D15UTLL"
                            }
                        ],
                        "displayName": "Big Bunny"
                    }
                }
            ],
            
        }
    ]
  }
  ```
  Além de sequências de texto nos metadados, também é possível fornecer versões traduzidas do guia de Iniciação Rápida, que está no formato de Redução. A URL da versão do idioma inglês da guia de Iniciação Rápida é especificada no campo metadata.instructionsUrl. Deve-se especificar a URL de um Guia de Iniciação Rápida traduzido no campo metadata.instructionsUrl dos metadados de cada código de idioma para o qual o guia for traduzido. A URL do Guia de Iniciação Rápida traduzido substitui o campo metadata.instructionsUrl que está nos metadados de nível superior. O Guia de Iniciação Rápida traduzido é exibido na interface com o usuário do {{site.data.keyword.Bluemix_notm}}. 
  
* Se você for um provedor iniciador, é possível fornecer sequências de texto traduzidas nos metadados do iniciador.
  Os dados traduzidos são retornados no campo extra no arquivo metadata.json do iniciador.
   
  Veja a sequência JSON a seguir como um exemplo de uma definição de iniciador que contém o campo extra.i18n:
  ```
  {
    "name": "Java DB Web Starter",
    "description": "Esse aplicativo de amostra demonstra como usar o Java JPA para se conectar a um banco de dados SQL.",
    "instructions": "app/instructions.md",
    "extra": {
        "i18n": {
            "fr": {
                "name": ...,
                "description": ...,
                "instructions": "app/fr/instructions.md"
            }
        }
    }
  }
  ```
  
* A equipe do Business Support System (BSS) é responsável pela tradução de planos de suporte e planos de tempo de execução. Os metadados JSON para planos de suporte e planos de tempo de execução são retornados pelos servidores BSS. Esses metadados são estruturados da mesma maneira que os metadados do plano de serviço.  
  
  Para os planos de suporte e planos de tempo de execução que são exibidos na interface com o usuário do {{site.data.keyword.Bluemix_notm}}, veja [Folha de precificação]({{site.data.keyword.pricing_list}}). 
  
  

## Referências do Broker de Serviço
{: #service_broker_references}

### Definição de broker de serviço

Para registrar um broker de serviço, deve-se fornecer um arquivo JSON que defina o broker de serviço. O formato do arquivo JSON é conforme a seguir.

**name**

O nome do broker de serviço. Esse nome deve ser exclusivo no {{site.data.keyword.Bluemix_notm}}. O valor inserido para o nome também é usado para identificar o serviço ao gerar métricas e analíticas. O conjunto de ferramentas de analítica se refere a esse valor como o rótulo do serviço.

**broker_url**

A URL da implementação do broker de serviço. 

**auth_username**

Um nome de usuário que é incluído nas solicitações de autenticação básica de HTTP para o broker de serviço. 

**auth_password**

Uma senha que é incluída nas solicitações de autenticação básica de HTTP para o broker de serviço. 

**owningOrganization**

O nome de uma organização cujos gerenciadores têm permissão para atualizar ou excluir o broker de serviço.

**serviceKeysSupported**

Um valor booleano que indica se a API de chaves de serviço é suportada. A API de chaves de serviço é usada para permitir que um serviço seja usado fora do Bluemix. O valor padrão é false.

**visibilities**

Informações sobre as organizações que têm visibilidade dos serviços que são fornecidos pelo broker de serviço. 
* **visibilities.organization_name**
    
	O nome de uma organização que tem visibilidade dos serviços. 
* **visibilities.plan_id**
	   
	O plano que é visível às organizações. Se o plano não for especificado, a organização pode ver todos os serviços e planos que são fornecidos pelo broker de serviço.

**use_bss_proxy**

(Opcional) Um valor booleano que indica se o broker de serviço pode ser acessado de outras regiões. Um valor de **true** significa que o broker de serviço pode ser acessada a partir de outras regiões. O valor padrão é **false**. 	   


**region_broker_urls**

(Opcional) Uma matriz de sequências que contêm os nomes e as URLs do broker de serviço para regiões dedicadas específicas. Especifique esse campo somente se os serviços puderem ser usados como serviços dedicados.

**partner**

(Opcional) Um valor booleano que indica se os serviços podem ser acessados a partir de todas as regiões públicas. Esse campo é usado por brokers de serviço a partir de provedores de serviços de terceiros e o valor padrão é false.

O código a seguir é um exemplo de uma definição de broker de serviço:
```
{
    "name" : "MyServiceBroker",
    "broker_url" : "http://serviceBrokerImpl.stage1.eu-gb.mybluemix.net",
    "auth_username": "ServiceBrokerUser",
    "auth_password": "ServiceBrokerPassword",
    "visibilities" : [
        {"organization_name" : "myOrganization"}
    ],
    "use_bss_proxy": true,
    "region_broker_urls": [ 
        {"name": "citi:production:us-south", "region_broker_url": "https://serviceBrokerImpl.citi-ng.bluemix.net"}
    ]
}
```


### Referência da API REST
{: #v2build}

O Bluemix suporta a API de broker de serviço Cloud Foundry V2. O Bluemix também fornece a API de extensão que contém os terminais Ativar e Estado. 

Entre os terminais de API a seguir que o Bluemix suporta, deve-se implementar os terminais Catálogo, Provisionar e Desprover. Se o parâmetro bindable for configurado como true ao implementar o terminal Catálogo, também deve-se implementar os terminais Ligar e Desvincular. 

[**Catálogo (GET)**](./index.html/catalog-get-)

Obtém informações sobre os brokers de serviço que preenchem o catálogo de serviços. Ao implementar esse terminal, deve-se fornecer as informações de serviço que você deseja exibir na interface com o usuário do Bluemix e na interface de linha de comandos cf.

[**Provisionar (PUT)**](./index.html/provision-put-)

Cria uma instância de serviço.

[**Desprover (DELETE)**]()

Exclui uma instância de serviço.

[**Ligar (PUT)**]()

Conecta uma instância de serviço a um aplicativo criando credenciais que são necessárias para o aplicativo acessar a instância.

[**Desvincular (DELETE)**]()

Desconecta uma instância de serviço de um aplicativo.

[**Ativar (PUT)**]()

Ativa uma instância de serviço.

[**Estado (GET)**]()

Obtém o estado de uma instância de serviço.



#### Catálogo (GET)
Catálogo é o primeiro terminal que deve-se implementar para o broker de serviço. O Bluemix chama esse terminal quando você emite `cloud-cli create-service-broker` ou `cloud-cli update-service-broker`.

**URL de catálogo (GET)**

O caminho da URL para o método GET que é chamado dentro da implementação do broker de serviço é `/v2/catalog`.

**Resposta do catálogo (GET)**

Na resposta JSON de GET /v2/catalog, deve-se fornecer as definições para seus serviços e planos de serviço, incluindo as informações de serviço que você deseja exibir na interface com o usuário do Bluemix.

Um código de status de 200 é o valor bem-sucedido esperado que é manipulado pelo Bluemix.

A resposta JSON de GET /v2/catalog consiste em uma matriz de definições de serviço e definições de plano de serviço no campo de serviços. Para uma amostra de JSON que inclui todos os campos obrigatórios, veja a amostra de JSON da resposta do Catálogo (GET).

Para obter detalhes de todos os campos de JSON em uma definição de serviço, veja a lista a seguir:

* **name**
	
	O nome do serviço que é exibido na interface de linha de comandos cf. Esse nome deve ser exclusivo no Bluemix e deve usar letras minúsculas e não deve conter espaços. Não é possível mudar o nome do serviço depois de registrar o serviço no Bluemix.

* **id **
    
	O ID do serviço. Esse ID deve ser exclusivo no Bluemix e deve ser um GUID (Identificador Exclusivo Global). Não é possível mudar o ID do serviço depois de registrar o serviço no Bluemix.

* **bindable**
    
	Um valor booleano que indica se as instâncias de serviço podem ser ligadas a aplicativos.

* **description**
    
	A descrição do serviço que é exibida ao usar o comando **cf marketplace** ou ao passar o mouse sobre o ícone do serviço no catálogo da interface com o usuário do Bluemix. É possível incluir uma única sentença ou frase para a descrição.	
 
* **metadados
**
    
	Os metadados de serviço que são exibidos na página de detalhes do serviço na interface com o usuário do Bluemix. Um JSON válido é necessário. 
    
	É possível especificar os campos a seguir que estão contidos no campo de metadados:
	
	* **displayName**
	     
		 O nome que é exibido na interface com o usuário do Bluemix para um serviço. Dezenove caracteres, incluindo espaços, podem ser exibidos antes de o nome ser truncado.
  
    * **providerDisplayName**
	    
		O nome do provedor de serviços.
		
	* **longDescription**
	
	    A descrição detalhada para o serviço. Considere usar pelo menos duas sentenças para uma descrição longa.
		
	* **type**
	   
	    O tipo do serviço. É possível usar os valores a seguir para esse campo:
		
		* **referral**
		   
		    A ser detalhado...
			
		* **dedicated**
		
		    Um serviço que está disponível em um ambiente dedicado. Para obter informações adicionais sobre um ambiente dedicado, veja [Bluemix Dedicated](https://www.stage1.eu-gb.bluemix.net/docs/overview/overview.html#ov_arch).
		
		* **local
**
		
		    Um serviço que está disponível em um ambiente local. Para obter mais informações sobre um ambiente local, veja [Bluemix Local](https://www.stage1.eu-gb.bluemix.net/docs/overview/overview.html#ov_arch).
  
        * **partner**
		    
			Um serviço de terceiro fornecido por uma empresa que não seja a IBM.
			
    * **bullets**
	
	    Uma matriz de sequências que são exibidas para um serviço. É possível usar marcadores para fornecer informações além da descrição longa. O campo de marcadores deve conter, pelo menos, dois elementos de marcador. Cada elemento de marcador contém os campos a seguir:
		
		* **title**
		
		    O título do marcador.
			
		* **description**
		
		    A descrição do marcador.
			
	* **imageUrl**
	    
		A URL de uma imagem grande (50 x 50 pixels). Para obter informações adicionais sobre imagens que são usadas na interface com o usuário do Bluemix para serviços, veja [Imagens do ícone de serviço](./index.html#service-icon-images).
  
    * **smallImageUrl**
	
	    A URL de uma imagem pequena (24 x 24 pixels).
		
    * **mediumImageUrl**
	
	    A URL de uma imagem média (32 x 32 pixels).
		
    * **featuredImageUrl**
	    
		A URL de uma imagem apresentada (64 x 64 pixels).
		
	* **documentationUrl**
	
	    A URL da documentação sobre o serviço. 
		
	* **instructionsUrl**
	
	    A URL de um arquivo markdown que contém instruções para usuários sobre como usar o serviço. Para obter mais informações sobre como incluir as instruções na interface com o usuário do Bluemix para serviços, veja [Guia de Iniciação Rápida}(./index.html#quick-start-guide).
  
    * **termsUrl**
  
        A URL para arquivos PDF que contêm termos de acordo.
		
    * **locationDisplayName**
	
	    Uma sequência que especifica a localização geográfica onde o serviço está hospedado. Para serviços que estão hospedados em uma das regiões do Bluemix, especifique o nome de exibição do Bluemix para essa região; por exemplo, **Sul dos EUA** e **Reino Unido**.
    
	* **media**
	   
	    (Opcional) Uma matriz de elementos para exibir os vídeos e as capturas de tela que introduzem o serviço na interface com o usuário do Bluemix. Um elemento de mídia pode conter os campos a seguir:
		
		* **type**
		    
			O tipo do elemento de mídia. As opções a seguir podem ser especificadas como o tipo de mídia, em que a opção `image` é usada para capturas de tela e as opções youtube e vídeo são usadas para vídeos.
         
		    * **image**
			    
				Uma captura de tela. Se a interface com o usuário do seu serviço estiver dentro de um iframe, não inclua a interface com o usuário do Bluemix circundante em suas capturas de tela.
				
				**Nota:** Se você usar a imagem como o tipo de mídia e fornecer capturas de tela para seu serviço, deve-se seguir estas diretrizes:
				* Forneça 1 - 5 capturas de tela para cada serviço.
				* Inclua uma imagem em tamanho normal e uma imagem em miniatura para cada captura de tela. O tamanho da imagem em miniatura para uma captura de tela é menor do que a imagem em tamanho normal.
				* Certifique-se de que as imagens em tamanho normal tenham uma largura mínima de 640 pixels.
				* Certifique-se de que as imagens em tamanho normal tenham um tamanho máximo de 800 KB.
				* Certifique-se de que as dimensões mínimas em pixels das imagens em miniatura sejam 500x300 e que a taxa de proporção das imagens em miniatura seja 5:3.
				* Certifique-se de que o tamanho máximo de imagens em miniatura seja 300	KB.
				* Use arquivos PNG para ambas as imagens, em tamanho normal e em miniatura.
  
            * **youtube**
			
			    Um vídeo que é integrado pelo YouTube. Nesse campo, especifique a URL que está na guia **Integração** do vídeo do YouTube. 
				
				Vídeos fornecem uma visão geral, em vez de um tutorial, do seu serviço. Os vídeos do YouTube são reutilizáveis e podem ajustar a qualidade de acordo com a conexão da Internet. Para um vídeo do YouTube de amostra, consulte [Explorando o IBM	Watson](http://www.youtube.com/watch?v=6aKg_0t_zms).
				
			* **vídeo**
			
			    Um vídeo que é hospedado em um site de terceiro que não seja o YouTube. Nesse campo, forneça ambos os arquivos, MP4 e	OGG para o vídeo. 
			
            **Nota:** Se você usar youtube ou vídeo como o tipo de mídia e fornecer vídeos para seu serviço, deve-se seguir estas diretrizes:	
                * Certifique-se de que a resolução de vídeo mínima seja 720p.
				* Certifique-se de que a taxa de proporção de vídeos seja 16:9.
				* Certifique-se de que as dimensões mínimas em pixels de vídeos sejam 640x360.
				* Certifique-se de que a duração de vídeos seja 1 - 3 minutos.
				* Forneça imagens em miniatura para vídeos. O tamanho máximo de imagens em miniatura é 300k; as dimensões mínimas em	pixels de imagens em miniatura são 500x300; a taxa de proporção de imagens em miniatura é 5:3.
				* Certifique-se de que a qualidade de áudio mínima para vídeos seja 160	kbps.
				
	* **thumbnailUrl**
        
        A URL da imagem de visualização para o elemento de mídia.

    * **url**
    
        A URL da captura de tela ou o vídeo do YouTube.

    * **source**

        As origens de vídeos que não estão hospedadas no YouTube. Cada elemento de origem na matriz contém os campos a seguir:

        * **type**

            O tipo do vídeo. Ele deve ser um formato de vídeo suportado por HTML5; por exemplo, **video/mp4** ou **video/ogg**. 	

        * **url**
        
            A URL do vídeo.

    * **caption**

        A legenda para o elemento de mídia. As legendas ajudam na acessibilidade para pessoas com deficiência para entender seus elementos de mídia.
 
        Assegure-se de descrever o conteúdo de seu elemento de mídia na legenda. Por exemplo, "Este vídeo demonstra o que é o serviço de Push e como usar notificações push para enviar conteúdo relevante para as pessoas certas no tempo e local certos."

        O comprimento máximo da legenda é de 350 caracteres.

    * **serviceKeysSupported**
  
        Um valor booleano que indica se a API de chaves de serviço é suportada. A API de chaves de serviço é usada para permitir que um serviço seja usado fora do Bluemix. O valor padrão é false.

    * **plan_updateable**

        Um valor booleano que indica se o serviço suporta mudanças de plano. O valor padrão é false.

    * **embeddableDashboard**

        (Opcional) Um campo que indica como o painel de serviço é exibido na interface com o usuário do Bluemix. Se você não especificar esse campo, o painel será integrado, mas estará restrito a uma largura mínima de 960px e o painel terá preenchimento horizontal adicional ao redor do iframe. 

        É possível usar os valores a seguir para esse campo:

        * **true**
   
            Indica que o painel de serviço está integrado na interface com o usuário do Bluemix usando um iframe responsivo sem uma largura mínima. Se você configurar o valor como	true, o campo embeddableDashboardFullWidth poderá ser especificado.

        * **false**
  
            Indica que o painel de serviço não está integrado na interface com o usuário do Bluemix. Em vez disso, é possível abrir o painel em uma guia do navegador separada clicando no botão na interface com o usuário da instância de serviço.

        * **drilldown**
  
            Indica que o painel de serviço se abre na mesma guia do navegador ao clicar no ladrilho da instância de serviço a partir da página de visão geral do aplicativo ou ao clicar na instância de serviço a partir da árvore de navegação no painel do Bluemix. 

        * **ativar**

            Indica que o painel de serviço se abre em uma nova guia do navegador ao clicar no ladrilho da instância de serviço a partir da página de visão geral do aplicativo ou ao clicar na instância de serviço a partir da árvore de navegação no painel do Bluemix.

            **Dica:** Para fornecer um botão **Voltar** na nova guia do navegador, especifique a URL de redirecionamento usando redirect no parâmetro `ace_config` para seu painel de serviço. Para obter mais informações sobre o parâmetro `ace_config`, veja [Suporte de iframe de administração](./index.html#administration-iframe-support). 		
				
    * **embeddableDashboardFullWidth**

        (Opcional) Um valor booleano que indica se o painel de serviço preenche a largura total do navegador. Se você não especificar esse campo, o valor será configurado para false. Um valor de false significa que o painel de serviço não preenche a largura do navegador. Esse valor não afeta a página de detalhes do serviço no catálogo.  
  
        **Importante:** Para que o valor do campo embeddableDashboardFullWidth especificado entre em vigor, deve-se configurar o valor do campo embeddableDashboard como **true**.
  
    * **notCreatable**
   
        (Opcional) Um valor booleano que indica se as instâncias para o serviço podem ser criadas a partir da interface com o usuário do Bluemix e a partir da interface de linha de comandos cf. Um valor true significa que as instâncias de serviço não podem ser criadas a partir da interface com o usuário do Bluemix ou a partir da interface de linha de comandos cf. O valor padrão é false.

    * **notCreatableMessage**	

        (Opcional) Uma mensagem que é exibida na interface com o usuário do Bluemix se as instâncias de serviço não puderem ser criadas. Se você não especificar esse campo, a mensagem padrão a seguir será exibida: `Para ser notificado quando ele estiver disponível, confirme o seu endereço de e-mail ou insira um endereço de e-mail diferente`.
  
    * **notCreatableRobotMessage**

        (Opcional) Uma mensagem que é exibida na bolha de fala da página de detalhes do serviço na interface com o usuário do Bluemix. A mensagem é usada para indicar se um serviço pode ter um problema ou outro motivo que esteja causando sua indisponibilidade. É possível especificar uma mensagem para explicar o motivo. Se você não especificar esse campo, a mensagem padrão a seguir será exibida: `Este serviço está indisponível atualmente`.

    * **apiReferenceUrl**

        (Opcional) A URL do iframe na área **Referência da API** na página de detalhes do serviço no **Catálogo**. 
  
    * **sdkDownloadUrl **

        (Opcional) A URL da página da web que é aberta quando o botão **Download SDK** é clicado. O botão **Download SDK** está no ladrilho do serviço da página de visão geral do aplicativo no	**Painel**. A página da web é aberta em uma nova guia do navegador.  
 
    * **userDefinedService**

        Metadados para serviços definidos pelo usuário. 
        * **parameters**
	
	        Uma matriz de pares de chave-valor que são definidos pelo serviço quando a instância do serviço é criada. 
		
		    * **parameters.name**
		    
			    A chave para o parâmetro.

            * **parameters.type**
		   
		        O tipo de campo de entrada que é exibido pela interface com o usuário do Bluemix. O valor pode ser texto ou senha.
			
		    * **parameters.value**
		
		        O valor padrão do parâmetro.
			
		    * **parameters.displayname**
		
		        O nome do parâmetro que é exibido.
			
		    * **parameters.invalidmessage**
		
		        A mensagem que aparece quando o conteúdo da caixa de texto é inválido.
			
		    * **parameters.description**
		
		        A descrição do parâmetro que é exibido para ajudar os usuários com o valor do parâmetro.
			
		    * **parameters.required**
		
		        Um valor booleano que indica se o parâmetro deve ser inserido na interface com o usuário do Bluemix.

            * **parameters.pattern**
		
		        Especifica uma expressão regular em relação à qual o valor é verificado. 
			
		    * **parameters.placeholder**
		
		        Especifica uma sugestão curta que descreve o valor esperado.
			
		    * **parameters.readonly**
		
		        Um valor booleano que indica se o valor do parâmetro é exibido somente e não pode ser alterado por usuários. O valor padrão é false.
			
		    * **parameters.hidden**
		
		        Um valor booleano que indica se o par chave-valor é oculto dos usuários. O valor padrão é false.
			
	    Para metadados de amostra que incluem os parâmetros definidos pelo usuário para um serviço definido pelo usuário, veja a sequência JSON a seguir:
		
	    ```
        {
           ...
           "metadata": {
             "featuredDescription": "A user-provided service. Instructional use only, not for use in production.",
             "isFeatured": false,
             "docURL": "http://www.yourserver.com:7080/doc/Sample/RESTApi.html",
             "userDefinedService": {
                 "dashboard_url": "https://example.com/dashboard/",
                 "parametersDescription": "Uma descrição contextual dos parâmetros, o exemplo seria: Deve-se <a href=\"http://ibm.com\" target=\"_blank\">registrar</a> antes de usar o serviço.",
                 "parameters": [
                     {
                        "name": "host",
                        "type": "text",
                        "value": "example.com",
                        "readonly": true,
                        "hidden": true
                     },
                     {
                        "name": "userid",
                        "displayname": "User id",
                        "type": "text",
                        "description": " ID do usuário que é usado para acessar o serviço.",
                        "invalidmessage": "Não é um endereço de e-mail válido",
                        "pattern": "^[_A-Za-z0-9-\\+]+(\\.[_A-Za-z0-9-]+)*@[A-Za-z0-9-]+(\\.[A-Za-z0-9]+)*(\\.[A-Za-z]{2,})$",
                        "placeholder": "email@example.com"
                     },
                     {
                        "name": "password",
                        "type": "password"
                     },
                     {
                        "name": "description",
                        "required": false
                     }
                 ]
             }
           }
        }
        ```

* **tag**

    Matrizes de sequências que indicam as categorias, os provedores e a prontidão de liberação dos serviços. 
	
	* As tags a seguir determinam as categorias às quais os serviços pertencem. 
	  
	   Como um serviço pode pertencer a somente uma categoria, é possível selecionar somente uma das tags de categoria a seguir para cada serviço. No entanto, é possível ligar a tag de categoria de um serviço com tags que especificam o provedor e a prontidão de liberação do serviço, como **ibm_created** e **ibm_beta**. 
	   
	   Se um serviço não tiver nenhuma das tags de categoria a seguir, ele será exibido na categoria **web_and_app**. 
	   
	    * **mobile**
	       
		   Serviços móveis.
		   
		* **web_and_app**
		
		   Serviços de aplicativos da web.
		   
		* **dev_ops**
		
		   DevOps Services.
		   
		* **integração
**
		
		   Serviços de integração.
		   
		* **data_management**
		
		    Serviços de gerenciamento de dados.
			
	    * **big_data**
		
		    Serviços de Big Data.
			
		* **security**
		
		    Serviços de segurança.
			
	    * **business_analytics**
		
		    Serviços de analítica.
			
		* **watson**
		
		    Serviços para construir aplicativos cognitivos.
			
	    * **internet_of_things**
		
		    Serviços para Internet of Things.
			
	    * **
pagamentos**
		
		    Serviços para coletar e rastrear pagamentos.
			
		* **privade**
		
		    Serviços privados.
			
	* (Opcional) As tags a seguir indicam os provedores de serviços. O valor padrão é **ibm_community**.
	
	    * **ibm_created**
		
		    O serviço é fornecido pela IBM. Se um serviço já especificou esse valor, o valor será preservado. 
			
		* **ibm_third_party**
		
		    O serviço é fornecido por parceiros de terceiros. Esse valor pode ser configurado somente por um administrador. Se um serviço já especificou esse valor, o valor será preservado. 
			
		* **ibm_community**
		
		    O serviço é fornecido por comunidades de software livre. Esse valor pode ser configurado somente por um administrador. Se um serviço já especificou esse valor, o valor será preservado. 
			
		* **ibm_private**
		
		    O serviço é um serviço privado que é visível somente a alguns usuários ou organizações.
			
	* (Opcional) As tags a seguir indicam a prontidão de liberação de serviços. O valor padrão é **ibm_release**.
	
	    * **ibm_experimental**
		
		    O serviço é experimental e não está pronto para produção. O provedor de serviços deseja que os usuários tentem o serviço, obtenham feedback e, então, decidam se continuarão a trabalhar no serviço. O provedor de serviços não fornece suporte ou garantia para o serviço experimental. O provedor de serviços pode remover o serviço do catálogo a qualquer momento.
			
			Os serviços que têm a tag ibm_experimental são rotulados com **Experimental** no Bluemix Labs Catalog. 
			
			A tag ibm_experimental tem precedência sobre outras tags. Por exemplo, se um serviço tiver a tag ibm_created e a tag ibm_experimental ao mesmo tempo, o serviço será rotulado com **Experimental** e exibido no Bluemix Labs Catalog.
			
			**Nota:** Também é possível usar somente uma das tags que são usadas para indicar a prontidão de liberação (ibm_experimental, ibm_beta e ibm_release) por vez.
			
		* **ibm_beta**
		
		    O serviço é um liberação beta. As versões beta de serviços devem incluir essa tag.
			
		* **ibm_release**
		
		    O serviço está liberado. O valor padrão se ibm_beta não for especificado. 
			
* **plans**

    Uma matriz de definições de plano de serviço. Cada entrada da matriz do campo de planos consiste nos campos a seguir: 
    
	* **name**

        O nome do plano de serviço que é usado na interface de linha de comandos cf. Por exemplo, o nome do plano é exibido na saída do comando **cf marketplace**. O nome do plano deve estar em letras minúsculas e não deve conter espaços e deve ser exclusivo dentro do serviço.	
		
	* **description**
	
	    A descrição do plano de serviço. A descrição é exibida depois que você selecionr um plano na página de detalhes do serviço no catálogo do Bluemix.
		
	* **libertar**
	
	    Um valor booleano que indica se o plano de serviço é grátis. O valor padrão é verdadeiro. 
		
	* **id **
	
	    O ID do plano de serviço. O ID deve ser exclusivo dentro do Bluemix e deve ser um GUID. 
		
	* **metadados
**
	 
	    Os metadados do plano de serviço que são exibidos no catálogo do Bluemix e na folha de precificação. O campo de metadados é um campo opcional. É possível especificar os campos a seguir no campo de metadados:
		
		* **displayName**
		
		    O nome do plano que é exibido na interface com o usuário do Bluemix. Esse nome é exibido na página de detalhes do serviço no catálogo e na folha de precificação.
			
			**Notas:**
			
			* Altere para letras maiúsculas somente a primeira letra do nome do plano; por exemplo, **Pequeno** ou **Mês**.
            * Não use **Default** como o nome do plano padrão. Use **Padrão** no lugar.			
	   
	    * **type**
		
		    O tipo do plano. É possível usar os valores a seguir para esse campo:
			
			* **subscrição**
			
			    Um plano de assinatura.
				
	    * **bullets**
		
		    Uma descrição dos recursos que podem ser usados com o plano. A descrição é exibida na coluna **Recursos** na página de detalhes do serviço do catálogo e na folha de precificação. O exemplo a seguir mostra informações que você pode especificar no campo de marcadores:
			
			```
			"bullets": ["1 app grátis com 3 dispositivos grátis por conta do Bluemix."],
			```
			**Notas:**
			
			* Para um plano de serviço grátis, no campo de marcadores, deve-se especificar a quantidade de recursos fornecidos sem encargos e se o uso dos recursos grátis é aplicado ao nível de conta do Bluemix ou ao nível de instância de serviço.
			* Use letras maiúsculas e minúsculas no estilo de sentença para o texto em cada marcador. Altere para letras maiúsculas somente a letra inicial da primeira palavra no texto e outras palavras que requerem letras maiúsculas e minúsculas, como nomes próprios (por exemplo, o nome do serviço). Sempre altere para letras maiúsculas a primeira palavra e não todas as palavras.
			* Os fragmentos de sentença (frases) são aceitáveis. Evite as construções como "Este é um plano grátis para..." quando "Plano grátis para..." for conveniente.
			* Insira um ponto no final de cada frase ou sentença no texto. 
			* Não especifique detalhes de preço no campo de marcadores, como **Os primeiros $5,00 de uso são grátis**.
			* Não use a palavra "via". Em vez disso, use um dos sinônimos a seguir: "em"," "junto", "por", "de", "no" ou "por meio de". 
			* Não abrevie "máximo" como "máx".
			* Se você usar parênteses para conter uma sentença separada completa, insira um ponto dentro dos parênteses. Se o texto entre parênteses não for uma sentença completa, não insira um ponto dentro dos parênteses.

        * **costs**
		
		    As informações de custo sobre o serviço que são exibidas na coluna Preço na página de detalhes do serviço do catálogo e na folha de precificação. Cada entrada da matriz contém os campos a seguir:
			
			* **unitId**
			    
				O ID da unidade. Use a forma plural e altere para letras maiúsculas todas as letras. Para planos grátis, esse campo é opcional.
				
				O valor desse campo é o mesmo que o nome de agregação especificado na definição de uso do recurso de serviço. Para obter mais informações sobre a definição de uso do recurso para seus serviços, veja [Configurando a medição do Bluemix](https://www.stage1.eu-gb.bluemix.net/docs/services/reporting_resource_usage.html#metering).
				
				**Nota:** Para planos grátis, se seu serviço não envia informações de uso, não é necessário especificar o campo unitId para esse plano grátis.

            * **unidade**
			
			    A métrica que é usada para calcular os encargos do serviço. O valor desse campo é usado na interface com o usuário do Bluemix para representar a métrica de encargo. Por exemplo, **$50,00 / GB**, em que GB é a unidade. Para planos grátis, esse campo é opcional.

				**Notas:**
     
	            * Altere para letras maiúsculas somente a primeira letra da unidade. Altere para letras maiúsculas todas as letras da unidade somente para abreviações, como GB, API e assim por diante.
				* Para planos grátis, se seu serviço não envia informações de uso, não é necessário especificar o campo de unidade para esse plano grátis.
				
			* **partNumber**
 
                O identificador part_number que é usado pelo sistema de faturamento IBM Distributed Software (DSW). Verifique com seu PLM sobre o valor desse campo. Para planos grátis, esse campo é opcional.
            
		* **paidOnly**

            (Opcional) Um valor booleano que indica se esse plano de serviço está disponível somente para contas de pagamento do Bluemix. Um valor de **true** significa que o plano de serviço é somente para contas de pagamento e não pode ser incluído em contas para teste. Um valor de **false** significa que o plano de serviço pode ser incluído nas contas de pagamento e contas para teste. O valor padrão é **false**.	
        
        O exemplo a seguir mostra como o código JSON no campo de planos é mapeado para as informações que são exibidas na página de detalhes do catálogo e na folha de precificação: 
         
        ![Planos de serviço de amostra](images/plan_metadata.png)		 

		
		
**Amostra de JSON da resposta do Catálogo (GET)**

```
{
    "services": [
        {
            "bindable": true,
            "description": "Cool Service é um solução de data warehousing e analítica.",
            "id": "cool-service-id",
            "name": "coolservice",
            "tags": [
                "business_analytics",
                "ibm_created"
            ],
            "metadata": {
                "displayName": "Cool Service",
                "providerDisplayName": "IBM",
                "longDescription": "Cool Service é um solução de data warehousing e analítica. É possível mover rapidamente seus dados para um banco de dados colunar contido na memória de próxima geração e começar a executar consultas analíticas complexas.",
                "bullets": [
                    {
                        "title": "Rápido e simples",
                        "description": "O Cool Service usa terminologia colunar dinâmica contida na memória e inovações, como processamento de vetor paralelo e compactação acionável para varrer e retornar rapidamente os dados relevantes."
                    },
                    {
                        "title": "Conectividade",
                        "description": "O Cool Service é construído para permitir que você se conecte facilmente a todos os seus serviços e aplicativos. É possível começar a analisar seus dados imediatamente com ferramentas familiares."
                    }
                ],
                "featuredImageUrl": "http://path/to/icon_64x64.png",
                "imageUrl": "http://path/to/icon_50x50.png",
                "mediumImageUrl": "http://path/to/icon_32x32.png",
                "smallImageUrl": "http://path/to/icon_24x24.png",
                "documentationUrl": "http://path/to/documentation.html",
                "instructionsUrl": "http://path/to/servicesample.md",
                "termsUrl": "http://path/to/terms_of_agreement.pdf",
                "media": [{
			"type": "youtube",
			"thumbnailUrl": "http://path/to/thumbnail.png",
			"url": "http://path/to/youtube/video",
			"caption": "Usando o Cool Service em 60 segundos"
		},
		{
			"type": "image",
			"thumbnailUrl": "http://path/to/thumbnail.png",
			"url": "http://path/to/image_file.png",
			"caption": "O Cool Service conecta aplicativos"
		},
		{
			"type": "video",
			"thumbnailUrl": "http://path/to/thumb.png",
			"caption": "O Cool Service trabalha com tabelas",
			"source": [{
				"type": "video/mp4",
				"url": "http://path/to/video_file.mp4"
			},
			{
				"type": "video/ogg",
				"url": "http://path/to/video_file.ogg"
			}],
			
		},
		]
            },
            "plans": [
                {
                    "name": "smallplan",
                    "description": "Esquema e espaço de tabela dedicados por instância de serviço em um servidor compartilhado. 1 GB e 10 GB de armazenamento do banco de dados compactado pode conter até 5 GB e 50 GB de dados descompactados, respectivamente, com base nas proporções de compactação típica.",
                    "free": false,
                    "id": "cool-service-plan-id",
                    "metadata": {
                        "bullets": [
                            "1 GB no mín. por instância. 10 GB no máximo por instância."
                        ],
                        "costs": [
                            {
                                "unitId": "INSTANCES_PER_MONTH",
                                "unit": "MONTHLY",
                                "partNumber": "D15UTLL"
                            }
                        ],
                        "displayName": "Pequeno"
                    }
                }
            ]
        }
    ]
}
```


O exemplo a seguir mostra como a resposta JSON de GET /v2/catalog é mapeada para a página de detalhes do serviço no catálogo do Bluemix:

![Página de detalhes do serviço de amostra](images/metadata.png)


**Teste para Catálogo (GET)**

É possível testar seu terminal Catálogo usando o comando a seguir:

```
curl -X GET -H "Accept:application/json" -H
"X-Broker-Api-Version:2.3" -H
"X-VCAP-Request-ID:e6dfc74d60e346c399bcfe04b1c2e760::a7a1bb74-5b5f-4356-ba70-eef0e36cf230"
-u "TestServiceBrokerUser:TestServiceBrokerPassword"
http://localhost:3000/v2/catalog
```


#### Provisionar (PUT)

É possível usar o terminal de API REST Provisionar para criar instâncias de serviço.

**URL de Provisionar (PUT)**

  O caminho da URL para o método PUT que é chamado dentro da implementação do broker de serviço é `/v2/service_instances/:instance_id`, em que `:instance_id` é o ID gerado pelo Controlador de Nuvem para a instância de serviço.

**Solicitação de Provisionar (PUT)**

  Os campos que são passados para PUT `/v2/service_instances/:instance_id` no corpo do JSON são os seguintes:

   * **organization_guid**
        
       O GUID da organização para **cf create-service**. 		

   * **plan_id**
   
       O ID do plano de serviço escolhido como parte de **cf create-service**. Este é um dos IDs de planos de serviços do catálogo Obter. 

   * **service_id**
   
       O ID da oferta de serviços como parte de **cf create-service**. Esse é um dos IDs de serviço do catálogo Obter. 

   * **space_guid**
   
       O GUID do espaço para **cf create-service**. 

**JSON de amostra da solicitação de Provisionar (PUT)**

```
{
  "organization_guid" : "a595cc4e-017a-437d-8a6f-7feb2fa0c88b",
  "plan_id"           : "ID do plano do broker de serviço V2 de teste",
  "service_id"        : "ID do broker de serviço V2 de teste",
  "space_guid"        : "af766c42-2f3f-41cf-8e4b-0c0761ef9d5c",
}
```

**Resposta de Provisionar (PUT)**

  Um código de status de 200 ou 201 é o valor bem-sucedido esperado que é manipulado pelo código do Controlador de Nuvem. Um código de status de 409 significa que o fornecimento já foi feito para essa URL.
  
  Os campos que são retornados de PUT /v2/service_instances/:instance_id no resultado do JSON são os seguintes:
  
   * **dashboard_url**
   
       A URL para um painel ou uma interface com o usuário para essa instância de serviço. Para obter informações sobre o suporte de iframe para esse painel ou interface com o usuário, veja [Suporte de iframe de administração](./index.html#administration-iframe-support).
	   
**JSON de amostra da resposta de Provisionar (PUT)**

```
{
  "dashboard_url" : "http://www.ibm.com"
}
```

**Teste para Provisionar (PUT)**

É possível testar seu terminal Provisionar usando o comando a seguir:
```
curl -X PUT -H "Accept:application/json" -H
"Content-Type:application/json" -H "X-Broker-Api-Version:2.3" -H
"X-VCAP-Request-ID:e81d9e214b9b4a13a843b1da12caa0f4::598af59e-b2b8-4ecd-bdea-b9cf20114509"
-u "TestServiceBrokerUser:TestServiceBrokerPassword" -d
"{\"organization_guid\":\"e6274fbc-e7d9-448f-a025-b2dbbe654edb\",
\"plan_id\":\"9a4194b0-4314-4188-a862-eaa60355beae\",
\"service_id\":\"8c1e1e8-76a4-4137-a02e-fed2fc04ba64\",
\"space_guid\":\"b0e72e12-205e-4984-8835-991d51ba804a\"}"
http://localhost:3000/v2/service_instances/3d06cbfa-e3d3-438c-b894-60f0e8f242ff
```

#### Ligar (PUT)
  
É possível o terminal de API REST Ligar para criar credenciais para acessar a instância de serviço por um aplicativo.

**URL de Ligar (PUT)**

O caminho da URL para o PUT que é chamado dentro da implementação do broker de serviço é `/v2/service_instances/:instance_id/service_bindings/:binding_id`, em que `:instance_id` é o ID gerado pelo Controlador de Nuvem para a instância de serviço e `:binding_id` é o ID gerado pelo Controlador de Nuvem para a ligação de serviço.	   
	   
**Solicitação de Ligar (PUT)**

Os campos que são passados para PUT /v2/service_instances/:instance_id/service_bindings/:binding_id no corpo do JSON são os seguintes:

   * **app_guid**

       O GUID do aplicativo ligado. 
    
   * **plan_id**

        O ID do plano que é escolhido como parte de **cf create-service**. Este é um dos IDs de planos de serviços do catálogo Obter. 

   * **service_id**		
   
       O ID da oferta de serviços como parte de **cf create-service**. Este é um dos IDs de serviço do catálogo Obter. 
	   
**JSON de amostra da solicitação de Ligar (PUT)**

```
{
  "app_guid" : "80e0caaa-4145-4f2a-9bf8-1ab00fff1766",
  "plan_id"           : "ID do plano do broker de serviço V2 de teste",
  "service_id"        : "ID do broker de serviço V2 de teste"
}
```

**Resposta de Ligar (PUT)**

Um código de status de 200 ou 201 é o valor bem-sucedido esperado que é manipulado pelo código do Controlador de Nuvem. Um código de status de 409 significa que a ligação já foi feita para essa URL.

Os campos que são retornados de PUT /v2/service_instances/:instance_id/service_bindings/:binding_id no resultado do JSON são os seguintes:

  * **credenciais**
  
      O valor do hash de credenciais.
	  
**JSON de amostra da resposta de Ligar (PUT)**

```
{
  "credentials"   :
  {
    "url"      : "http://10.0.1.2:12345"
    "userid"   : "8401a824-1da7-4114-8664-2460db21661a",
    "password" : "b98e9690-c5e7-405f-9ef6-d6fa36afbaba"
  }
}
```

**Teste para Ligar (PUT)**

É possível testar seu terminal Ligar usando o comando a seguir:
```
curl -X PUT -H "Accept:application/json" -H
"Content-Type:application/json" -H "X-Broker-Api-Version:2.3" -H
"X-VCAP-Request-ID:9449b70048434b3aa7106377cfb463e4::e9710444-5968-4895-9cf4-ae78d69bc168"
-u "TestServiceBrokerUser:TestServiceBrokerPassword" -d
"{\"app_guid\":\"d3f16a48-8bd1-4aab-a7de-e2a22ad38292\",
\"plan_id\":\"9a4194b0-4314-4188-a862-eaa60355beae\",
\"service_id\":\"8c14e1e8-76a4-4137-a02e-fed2fc04ba64\"}"
http://localhost:3000/v2/service_instances/3d06cbfa-e3d3-438c-b894-60f0e8f242ff/service_bindings/1eef45f2-6151-4394-a958-590a9be09210
```

#### Desvincular (DELETE)

**URL de Desvincular (DELETE)**

O caminho da URL para o DELETE que é chamado dentro da implementação do broker de serviço é `/v2/service_instances/:instance_id/service_bindings/:binding_id`, em que `:instance_id` é o ID gerado pelo Controlador de Nuvem para a instância de serviço e `:binding_id` é o ID gerado pelo Controlador de Nuvem para a ligação de serviço.

**Solicitação de Desvincular (DELETE)**

Os campos que são passados para `DELETE /v2/service_instances/:instance_id/service_bindings/:binding_id` como parâmetros de consulta são os seguintes:

   * **plan_id**
   
       O ID do plano que é escolhido como parte de **cf create-service**. Esse é um dos IDs do plano de serviço do catálogo Obter. 

    * **service_id**
    
        O ID da oferta de serviços como parte de **cf create-service**. Esse é um dos IDs de serviço do catálogo Obter.	
		
		
**Resposta de Desvincular (DELETE)**

Um código de status de 200 é o valor bem-sucedido esperado que é manipulado pelo código do Controlador de Nuvem. Um código de status de 410 significa que o recurso já foi excluído.

Atualmente nenhum campo é retornado de DELETE /v2/service_instances/:instance_id/service_bindings/:binding_id, mas um hash vazio é sugerido para expansão futura no caso de 200 ou 410.

**JSON de amostra da resposta de Desvincular (DELETE)**

```
{
}
```

**Teste para Desvincular (DELETE)**

É possível testar seu terminal Desvincular usando o comando a seguir:

```
curl -X DELETE -H "Accept:application/json" -H
"X-Broker-Api-Version:2.3" -H
"X-VCAP-Request-ID:33021f6327374feb9b21fd66e1475aa7::fa04ffe3-0ee4-459c-8715-6c1779318955"
-u "TestServiceBrokerUser:TestServiceBrokerPassword"
"http://localhost:3000/v2/service_instances/3d06cbfa-e3d3-438c-b894-60f0e8f242ff/service_bindings/1eef45f2-6151-4394-a958-590a9be09210?plan_id=9a4194b0-4314-4188-a862-eaa60355beae&service_id=8c14e1e8-76a4-4137-a02e-fed2fc04ba64"
```

#### Desprover (DELETE)

**URL de Desprover (DELETE)**

O caminho da URL para o DELETE chamado dentro da implementação do broker de serviço é `/v2/service_instances/:instance_id`, em que `:instance_id` é o ID gerado pelo Controlador de Nuvem para a instância de serviço.

**Solicitação de Desprover (DELETE)**

Os campos que são passados para DELETE /v2/service_instances/:instance_id como parâmetros de consulta são os seguintes:

   * **plan_id**
	
	    O ID do plano que é escolhido como parte de **cf create-service**. Esse é um dos IDs de planos de serviço do catálogo Obter. 
		
   * **service_id**
	
	    O ID da oferta de serviços como parte de **cf create-service**. Esse é um dos IDs de serviço do catálogo Obter.
		
**Resposta de Desprover (DELETE)**

Um código de status de 200 é o valor bem-sucedido esperado que é manipulado pelo código do Controlador de Nuvem. Um código de status de 410 significa que o recurso já foi excluído.

Atualmente nenhum campo é retornado de DELETE /v2/service_instances/:instance_id, mas um hash vazio é sugerido para expansão futura no caso de 200 ou o 410.

**JSON de amostra da resposta de Desprover (DELETE)**

```
{
}
```

**Teste para Desprover (DELETE)**

É possível testar seu terminal Desvincular usando o comando a seguir:

```
curl -X DELETE -H "Accept:application/json" -H
"X-Broker-Api-Version:2.3" -H
"X-VCAP-Request-ID:eb8d14f15efc4832beb65220b2cb48a8::3e3e2108-d7e4-498a-9180-68588153208f"
-u "TestServiceBrokerUser:TestServiceBrokerPassword"
"http://localhost:3000/v2/service_instances/3d06cbfa-e3d3-438c-b8960f0e8f242ff?plan_id=9a4194b0-4314-4188-a862-eaa60355beae&service_id=8c14e1e8-76a4-4137-a02e-fed2fc04ba64"
```
	

#### Ativar (PUT)

Este é um terminal da API de extensão que é fornecida pelo Bluemix. Esse terminal suporta a ativação ou desativação de uma instância de serviço.

**URL de Ativar (PUT)**

O caminho da URL para o método PUT para a implementação do broker de serviço é `/bluemix_v1/service_instances/:instance_id`, em que `:instance_id` é o ID gerado pelo Controlador de Nuvem para a instância de serviço.
	
**Solicitação de Ativar (PUT)**

Os campos que são passados para PUT /bluemix_v1/service_instances/:instance_id no corpo do JSON são os seguintes:

   * **ativado**
       
       Um valor booleano que indica se a instância de serviço precisa ser ativada.

**JSON de amostra da solicitação de Ativar (PUT)**

```
{
  "enabled" : true
}
```

**Resposta de Ativar (PUT)**

Um código de status de 204 é o valor bem-sucedido esperado.

**Teste para Ativar (PUT)**

É possível testar seu terminal Ativar usando o comando a seguir:

```
curl -X PUT -H "Content-Type:application/json" -u
"TestServiceBrokerUser:TestServiceBrokerPassword" -d
"{\"enabled\":true}"
http://localhost:3000/bluemix_v1/service_instances/3d06cbfa-e3d3-438c-b894-60f0e8f242ff
```


#### Estado (GET)

Este é um terminal da API de extensão que é fornecido pelo Bluemix. Esse terminal suporta a recuperação do estado atual de uma instância de serviço.

**URL de Estado (GET)**

O caminho da URL para o método GET para a implementação do broker de serviço é `/bluemix_v1/service_instances/:instance_id`, em que `:instance_id` é o ID gerado pelo Controlador de Nuvem para a instância de serviço.	   

**Resposta de Estado (GET)**

Um código de status de 200 é o valor bem-sucedido esperado. Os campos que são retornados de GET /bluemix_v1/service_instances/:instance_id no resultado do JSON são os seguintes:

   * **ativado**
       
	   Indica se a instância de serviço está ativada ou não.
	  
   * **estado**
   
       O valor é STARTING, STARTED, STOPPING ou STOPPED.
	   
   * **mensagem**
   
       A sequência para detalhes.
	   
**JSON de amostra da resposta de Estado (GET)**

```
{
  "enabled" : true,
  "state" : "STARTED",
  "message" : "A instância de serviço está ativada e iniciada"
}
```

**Teste para Estado (GET)**

É possível testar seu terminal Estado usando o comando a seguir:

```
curl -X GET -H "Accept:application/json" -u
"TestServiceBrokerUser:TestServiceBrokerPassword"
http://localhost:3000/bluemix_v1/service_instances/3d06cbfa-e3d3-438c-b894-60f0e8f242ff
```

### Guia de Iniciação Rápida
{: #v2next}

Os provedores de serviços podem exibir o guia de Iniciação Rápida na interface com o usuário do Bluemix para fornecer instruções sobre como usar o serviço para os usuários. O guia de Iniciação Rápida pode ser especificado durante o registro do serviço e será exibido na área **Visualizar Iniciação Rápida** na guia **Visão geral** da página de detalhes do aplicativo quando uma instância de serviço for criada.

O conteúdo da área de guia é exibido nos dois formatos a seguir:

* **Reduzidas**

    Exibe conteúdo limitado do guia e pode conter os recursos a seguir: 
	
	* Título de 40 caracteres
	* Visualização de 45 caracteres da descrição

* **Expandidas**

    Exibe o conteúdo completo do guia e pode conter os recursos a seguir: 
	
	* Título de 40 caracteres
	* Descrição
	* Marcadores: Cada marcador pode ter no máximo 90 caracteres
	* Código de amostra ou linha de comandos
	
O conteúdo do
guia é composto no formato de Redução de preço. Além do formato de Redução, a interface com o usuário do Bluemix suporta variáveis dinâmicas para gerar partes do conteúdo que é baseado dinamicamente na instância. As variáveis a seguir são substituídas dinamicamente quando
especificadas no formato de `${variable_name}`:

* **api-url**

    URL de terminal de API. É possível usar essa variável para exemplos de chamada de destino da linha de comandos cf.
	
* **username**

    Usuário que está com login efetuado.
	
* **service **

    Nome da oferta de serviços.
	
* **service-guid**

    GUID da oferta de serviços.
	
* **service-version**

    GUID da oferta de serviços.
	
* **service-plan**

    Nome do plano de serviço.
	
* **service-instance**

    Nome da instância de serviço.
	
* **doc-url**

    URL base para a documentação para essa instância do Bluemix.
	
* **ace-url** 

    URL base da interface com o usuário do Bluemix; por exemplo, `https://console.stage1.eu-gb.bluemix.net`.

Para assegurar consistência, a Redução deve usar o padrão de Redução geral a seguir:
```
Guia de introdução (40 caracteres no máximo)
----------------------------------------------

O texto de descrição exibe até 45 caracteres na visualização, mas o texto
integral é exibido quando a guia é expandida.

1. Máximo de 90 caracteres (2 linhas com 45 caracteres cada)
2. Hiperlinks também podem ser especificados [http://www.ibm.com](ibm.com)
3. O código de amostra também pode ser especificado e exibido em uma janela
de altura máxima de 250 px

    cf target ${api_url}
    cf login ${username}
    cf push ${app}
```

### Imagens do ícone de serviço
{: #v2image}

Como um provedor de serviços, deve-se fornecer as imagens que são usadas para exibir seu serviço na interface com o usuário do Bluemix. É possível fornecer ativos de imagem ao implementar o broker de serviço.

Deve-se fornecer imagens nos quatro tamanhos de imagem a seguir. Diferentes tamanhos de imagem são usados em diferentes partes da interface com o usuário do Bluemix. Todos os arquivos de imagem devem estar no formato PNG em planos de fundo de bitmap transparente.

**Pequeno 24 x 24**

Uma imagem de 24 x 24 pixels é exibida nos locais a seguir na guia Painel da interface com o usuário do Bluemix:

   * Na parte superior da interface com o usuário do serviço após esse serviço ser provisionado.
   * Nos ladrilhos dos aplicativos aos quais o serviço está ligado.
   
**Médio 32 x 32**

Uma imagem de 32 x 32 pixels é exibida no ladrilho do serviço, na guia Painel da interface com o usuário do Bluemix.

**Grande 50 x 50**

Uma imagem de 50 x 50 pixels é exibida nos locais a seguir da interface com o usuário do Bluemix:

   * Na página **Visão geral** da guia **Painel** de um aplicativo ao qual o serviço está ligado.
   * No catálogo de serviços na guia **Catálogo** 
   * Na página de detalhes do serviço que é aberta depois que você clicar em um serviço na guia **Catálogo**

**Destacado 64 x 64**

Uma imagem de 64 x 64 pixels é usada para exibir o serviço quando ele é um serviço destacado na página **SOLUÇÕES** do Bluemix. Esse tamanho da imagem permite fornecer texto que descreve o serviço.

**Notas:**

   * Se um conjunto de imagens não for fornecido por um serviço, o Bluemix fornecerá um conjunto de imagens padrão.
   * Deve-se armazenar em cache as informações para os ativos de imagem para evitar que as imagens sejam recarregadas desnecessariamente. É possível armazenar em cache as informações de imagem, incluindo um parâmetro de versão exclusivo para a URL da imagem e configurando os cabeçalhos de expirações de cache para valores grandes. Quando a imagem muda, o número da versão é atualizado. Por
exemplo:
   
   ```
   "imageUrl" : "http://serviceBrokerImpl.stage1.eu-gb.mybluemix.net/icons/serviceIcon?version=1" ,
   ```
   
**Dica:** Para obter aprovação da equipe de design do Bluemix para seus ícones, acesse [Lista de ícones principais](https://releaseblueprints.ibm.com/display/CLOUDOE/Master+Icon+List).


### Suporte de iframe de administração
{: #iframe}

A interface com o usuário de administração de um serviço é exibida na guia **Painel** da interface com o usuário do Bluemix dentro de um iframe. As informações a seguir mostram como o iframe é inicializado e como o código do iframe interage com o Bluemix. 

**Inicialização do iframe de administração**

Quando o iframe de administração é inicializado, um parâmetro chamado ace_config é passado na URL. Ele contém as seguintes informações:

```
{
  // ID representando o serviço atual; deve ser passado de volta para a interface com o usuário do Bluemix em todas as mensagens
  id: "12345-12345",

  // se chamado a partir do painel na interface com o usuário do Bluemix:
  orgGuid: "12345-12345",
  spaceGuid: "12345-12345",

  // se chamado a partir de um app:
  appGuid: "12345-12345",
  orgGuid: "12345-12345",
  spaceGuid: "12345-12345",

  // altura de pixel para o tamanho de iframe 'ideal', no qual ele se ajusta completamente na
  // porta de visualização sem barras de rolagem (largura é manipulada pela interface com o usuário do Bluemix)
  idealHeight: 300
  //Fornece uma URL integral para voltar para um local na UI do Bluemix. Isso é particularmente útil para os serviços que especificam a ativação para embeddableDashboard e desejam fornecer um botão "Voltar".
  redirect: "https://console.stage1.eu-gb.bluemix.net",
} 
```

Para recuperar esse objeto, deve-se tomar a ação a seguir: 

```
// os conteúdos da sequência do parâmetro URL `ace_config` são armazenados em `aceConfigString`
var aceConfig = JSON.parse(decodeURIComponent(aceConfigString)); 
```

**IU Responsiva**

Todo código de administração de serviço ou extensão deve ser responsivo -- ou seja, ele deve ser exibido corretamente em uma ampla variedade de larguras, tornando a fluir os componentes da UI conforme necessário para ajustar dentro da largura determinada. 

Para ativar sua UI responsiva no iframe, deve-se configurar o valor do campo embeddableDashboard nos metadados de serviço como **true**. Para obter mais informações sobre os metadados de serviço, veja v2metadata.html#v2metadata. 

Por padrão, a interface com o usuário do Bluemix define a altura do iframe para 1024 pixels. Se a UI de administração requer mais ou menos área para minimizar o espaço em branco ou ter barras de rolagem verticais, o código de administração pode enviar uma mensagem para a interface com o usuário do Bluemix usando a API window.postMessage. Por
exemplo: 

```
function sendFrameSizeMessage() {
    var targetOrigin = '*';
    var payload = {
        type: '/ace/service/framesize',
        data: {
            id: '12345-12345',   // ace_config.id
            height: 300
        }
    };
    window.top.postMessage(payload, targetOrigin);
}
```
Para obter mais informações sobre a API window.postMessage, veja [Window.postMessage](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage).

O exemplo a seguir mostra como ativar uma UI de administração para redimensionar quando o iframe for carregado pela primeira vez e para redimensionar dinamicamente quando a janela do navegador for redimensionada. 

```
(function() {

    function addEventListener(el, type, listener, useCapture) {
        if (el.addEventListener) {
            el.addEventListener(type, listener, useCapture);
        } else if (el.attachEvent) {
            el.attachEvent('on' + type, listener);
        }
    }

    var savedBodyHeight = 0;

    function sendResizeMessage() {
        var height = document.body.offsetHeight;

        if (height !== savedBodyHeight) {
            savedBodyHeight = height;

            var targetOrigin = '*';
            var payload = {
                type: '/ace/service/framesize',
                data: {
                    id: '12345-12345',   // ace_config.id
                    height: height
                }
            };
            window.top.postMessage(payload, targetOrigin);
        }
    }

    addEventListener(window, 'load', sendResizeMessage);
    addEventListener(window, 'resize', sendResizeMessage);

})();
```

**Altura ideal**

Quando o iframe de administração é inicializado, a interface com o usuário do Bluemix também calculará a altura ideal para o iframe, dado o tamanho da porta de visualização atual. Essa é a altura em que o iframe pode ser exibido na página sem mostrar barras de rolagem verticais na página. Ela é fornecida como parte do parâmetro URL ace_config.

Se a UI de administração de serviço ou extensão puder ser dimensionada dinamicamente, ela poderá ser configurada para ser exibida nessa altura ideal. O código do iframe deve, então, enviar a mensagem `/ace/service/framesize` para a interface com o usuário do Bluemix com essa altura. 


**Configurando o estado sujo**

Se a UI de administração de serviço ou extensão permite entrada do usuário, o código pode configurar o estado sujo da página para evitar que o usuário feche ou navegue para fora da página acidentalmente. Isso pode ser feito enviando a mensagem `/ace/service/dirty` para a interface com o usuário do Bluemix, com a propriedade Sujo configurada como true. Configure o valor como false para desativar o estado sujo. Por exemplo: 
```
function sendDirtyMessage() {
  var targetOrigin = '*';
  var payload = {
        type: '/ace/service/dirty',
        data: {
            id: '12345-12345',   // ace_config.id
            dirty: true          // ou false
        }
    };
    window.top.postMessage(payload, targetOrigin);
}
```

## Relatando o uso do recurso 
{: #reporting_resource_usage}

Para calcular o uso de recursos de serviço e relatar o uso ao Bluemix™, deve-se usar o Bluemix Metering Service. 

### Configurando a medição do Bluemix
{: #metering}

Os usuários do Bluemix são cobrados com base na quantia de recursos que eles usam. Por exemplo, os usuários do Bluemix que usam os serviços de banco de dados podem ser cobrados com base na quantia de armazenamento que seus aplicativos usam.

Depois de registrar sua definição de recurso com o serviço de medição do Bluemix, é possível usar a API que o serviço de medição do Bluemix fornece para relatar dados de uso de recursos de serviço que são consumidos por usuários do Bluemix.

Para usar o serviço de medição do Bluemix para reportar dados de uso, conclua as etapas a seguir:

1. Crie uma definição de recurso no formato JSON para listar recursos de serviço que você deseja medir. Também deve-se especificar métricas e modelos de agregação para esses recursos, que são usados para medição e também mostrados aos usuários do Bluemix na interface com o usuário do Bluemix. Para obter detalhes sobre o formato e o conteúdo para a definição de recurso, veja [Definição de recurso](.index.html#resource-definition).

   Assegure-se de que a definição de recurso siga as diretrizes de ID e nomenclatura detalhadas em [Diretrizes de envio de uso](./index.html#usage-submission-guidelines).

2. Registre a definição de recurso com o serviço de medição do Bluemix enviando um e-mail para o [Administrador de medição do Bluemix](mailto:Bluemix-MeteringService).

3. Implemente a API do serviço de medição do Bluemix para relatar os dados de uso de seu serviço. Veja [API do serviço de medição do Bluemix para detalhes](./index.html#bluemix-metering-service-api) para obter detalhes.

   Assegure-se de seguir as diretrizes de envio detalhadas em [Diretrizes de envio de uso](./index.html#usage-submission-guidelines).


### Definição de recurso

A definição de recurso é usada para listar os recursos de serviço que você deseja medir e para especificar métricas e modelos de agregação desses recursos.

A definição de recurso deve estar no formato JSON e deve conter todos os campos obrigatórios. Deve-se seguir todas as diretrizes de envio de uso ao especificar valores para esses campos. Para obter detalhes, veja [Diretrizes de envio de uso](./index.html#usage-submission-guidelines).

* **id **
    
	O ID do serviço. Esse ID deve ser exclusivo no Bluemix e deve ser um GUID. 
	
* **
recursos** 

    Os nomes e unidades do recursos do serviço.
	
	* **resources.name**
	
	    O nome do recurso de serviço. 
		
	* **resources.unit**
	
	    O nome da unidade e tipo de quantidade para o uso do recurso de serviço.
		
		* **resources.unit.name**
		
		    O nome da unidade para o recurso de serviço. Por exemplo, é possível especificar **GIGABYTES** ou **API_CALL** para esse campo.
			
		* **resources.unit.quantityType**
		
		    O tipo de quantidade para o recurso de serviço. Por exemplo, é possível especificar **CURRENT** ou **DELTA** para esse campo.

* **agregações**
	
    Uma matriz de sequências que representam os modelos de agregação para os recursos do serviço. 

    * **aggregations.id**

        O identificador do modelo de agregação para o uso do recurso de serviço. Assegure-se de que o valor do campo aggregations.id seja o mesmo que o valor do campo cost.unitId. O campo cost.unitId está contido no campo de planos da definição de serviço no resultado de Obter catálogo. Para obter mais informações sobre o campo de planos, veja Planos.

    * **aggregations.unit**

        O nome da unidade do modelo de agregação. 

    * **aggregations.aggregationGroup**

        O nome do grupo de agregação ao qual o modelo de agregação pertence.

    * **aggregations.formula**
  
        A fórmula do modelo de agregação. Deve-se incluir uma função e uma unidade de recurso na fórmula. As funções que podem ser usadas incluem **AVG**, **SUM** e **MAX**. As unidades de recurso devem ser as unidades que estão definidas no campo de recursos. 

Veja a definição a seguir de um uso de recurso como um exemplo:

```
{
    "id": "MyService-8e9f8a35-dc03-4192-8bba-a77ae60222eb",
    "resources": [
        {
            "name": "Armazenamento",
            "units": [
                {
                    "name": "GIGABYTE",
                    "quantityType": "CURRENT"
                }
            ]
        },
        {
            "name": "ApiCalls",
            "units": [
                {
                    "name": "API_CALL",
                    "quantityType": "DELTA"
                }
            ]
        }
    ],
    "aggregations": [
        {
            "id": "GB_PER_MONTH",
            "unit": "GIGABYTE",
            "aggregationGroup": {
                "name": "mensal"
            },
            "formula": "AVG({GIGABYTE})"
        },
        {
            "id": "API_CALLS_PER_MONTH",
            "unit": "API_CALL",
            "aggregationGroup": {
                "name": "mensal"
            },
            "formula": "SUM({API_CALL})"
        }
    ]
}
```

### Diretrizes de envio de uso
{: #metering_guidelines}

Deve-se seguir as diretrizes específicas ao usar o serviço de medição do Bluemix.

**Diretrizes de envio**

  Consulte as diretrizes a seguir ao enviar dados de uso de recurso usando o serviço de medição do Bluemix:
  
   * Envie os dados de uso de recurso para o serviço de medição uma vez a cada 2 a 24 horas. A frequência com que você envia seus dados de uso depende da frequência com que suas métricas de uso mudam.
   * Envie os dados de uso de recurso de um dia até o final do dia seguinte em Hora Universal Coordenada (UTC).
   * Um envio bem-sucedido retorna um código de resposta de 201. Se qualquer outro código de resposta for retornado, atualize e reenvie os dados até que você receba o código 201.
   * Para o ambiente de Estágio 1 amarelo, acesse o serviço de medição usando a URL a seguir: 
     ```
     https://MeteringInterface-Provider.stage1.ng.bluemix.net
     ```
   * Para o ambiente de Produção Amarelo, acesse o serviço de medição usando a URL a seguir: 
     ```
     https://meteringinterface-provider.ng.bluemix.net
     ```

**Diretrizes do ID de serviço**

  Deve-se seguir estas diretrizes ao especificar o ID de serviço usando o campo de ID na definição de recurso:
  * Inicie o ID com um caractere alfanumérico.
  * Use os caracteres A - Z, a - z e 0 - 9. Os únicos caracteres especiais que podem ser usados são hifens (-) e sublinhados (_).
  * Siga a convenção Camel Case se o ID contiver mais de uma palavra.
  * Assegure-se de que o comprimento máximo do ID seja 50 caracteres.
  
**Diretrizes de nome do recurso**

  Deve-se seguir estas diretrizes ao especificar o nome do recurso usando o campo resources.name na definição de recurso:
  
  * Use somente palavras que descrevam seus recursos. Por exemplo, **Storage** ou **ApiCalls**. 
  * Siga a convenção Camel Case se o nome contiver mais de uma palavra.
  * Altere para letras maiúsculas o primeiro caractere do nome.

**Diretrizes de nome da unidade de recurso**

  Deve-se seguir estas diretrizes ao especificar o nome da unidade de recurso usando o campo resources.unit.name na definição do recurso:

  * Use uma palavra para o nome da unidade e use um sublinhado (_), em vez de um espaço, para separar as palavras. Por exemplo, especifique **API_CALL** em vez de **API CALL**.  
  * Altere para letras maiúsculas todas as letras do nome.
  
**Diretrizes de qualidade da unidade de recurso**

  Deve-se seguir estas diretrizes ao especificar o tipo de quantidade de recursos usando o campo resources.unit.quantityType na definição de recurso:
  
  * Use uma palavra para o tipo de quantidade.
  * Altere para letras maiúsculas todas as letras do tipo de quantidade.
  
**Diretrizes do ID de agregação**

  Deve-se seguir estas diretrizes ao especificar o ID de agregação usando o campo aggregations.id na definição de recurso:

  * Altere para letras maiúsculas todas as letras do tipo de quantidade.
  * Use um sublinhado (_), em vez de um espaço, para separar as palavras.
  * Assegure-se de que esse ID inicie com ou corresponda ao valor de aggregations.unit. Por exemplo, é possível especificar **API_CALLS_PER_MONTH** para aggregations.id e especificar **API_CALLS** para aggregations.unit.

**Diretrizes de unidade de agregação**

  Deve-se seguir estas diretrizes ao especificar a unidade de agregação usando o campo aggregations.unit na definição de recurso:
   
  * Use formulário singular para o nome da unidade.
  * Altere para letras maiúsculas todas as letras do nome da unidade.
  * Assegure-se de que o nome da unidade especificado no campo aggregations.unit seja uma agregação do nome da unidade especificado no campo resources.unit.name.
  
**Diretrizes de grupo de agregação**

  Deve-se usar letras minúsculas para o campo aggregations.aggregationGroup na definição de recurso.
  
**Diretrizes de fórmula de agregação**

  Para o campo aggregations.formula na definição de recurso, se você desejar usar operações aritméticas na fórmula, deve-se usar a unidade de recurso como um operando e usar uma expressão aritmética infix na função da fórmula. Por exemplo, é possível usar a fórmula a seguir para converter Bytes em Megabytes:
  ```
  SUM({BYTE}/1048576)
  ```
  
### API do serviço de medição do Bluemix
{: #metering_api}

É possível usar os terminais de API do serviço de medição do Bluemix para relatar ou recuperar os dados de uso do serviço fornecendo um ID de serviço ou um ID de instância de serviço nas solicitações de HTTP.

No cabeçalho de resposta para cada envio de uso, a propriedade Local contém a URL para recuperar o registro de envio de uso. É possível salvar essa URL para referência futura.

**Request**

 * **Rota**
 
   ```
   POST /v1/metering/services/:service_id/usage?region=us-south
   ```
   **Nota:** Postar dados de uso usando essa API reduz o número de chamadas HTTP.
   
 * **Parâmetros de consulta**
    
     * **região ** 
		
		  O ID da região de dados de uso. É possível usar eu-gb para Londres, us-south para Dallas e au-syd para Sydney.
		  
 * **Parâmetros**
    
	 * **service_id**
	   
	     O ID do serviço. Esse ID deve ser exclusivo e deve ser um GUID.
		 
 * **Cabeçalho**
 
     * **Autorização**
	 
	     Credenciais de autenticação básica. Os campos de nome do usuário e senha são os mesmos que na definição do broker de serviço. Para obter mais informações sobre o formato do esquema de autenticação básica, veja [RFC1945](http://tools.ietf.org/html/rfc1945#section-11.1).
		 
 * **Corpo**
    
     * **service_instances**

         Uma matriz de sequências que contêm dados de uso de instâncias de serviço que você deseja postar. Essas instâncias de serviço usam a mesma região que o parâmetro de consulta.

         * **usage**

             Uma matriz de dados de uso que você deseja postar. Esses dados de uso têm a mesma região que o parâmetro de consulta.
    
             Dentro dos dados de uso, o plan_id é o ID do plano de serviço que é especificado como um parâmetro de cf create-service. O ID deve ser exclusivo dentro do Bluemix e deve ser um GUID. O valor desse campo plan_id é o mesmo que o campo plan_id que está na solicitação de Provisionar (PUT) quando a instância de serviço é criada. Para obter mais informações sobre o campo plan_id no terminal Provisionar (PUT), veja [Provisionar (PUT)].	
		 
         Veja a sequência JSON a seguir como um exemplo:
		```
         {
             "service_instances": [
                {
                     "service_instance_id": "myServiceInstance-guid",
                     "usage": [
                         {
                             "plan_id": "",
                             "start": 1396421450000,
                             "end": 1396421451000,
                             "organization_guid": "myOrganization-guid",
                             "space_guid": "mySpace-guid",
                             "consumer": {
                                 "type": "cloud-foundry-application",
                                 "value": "myApplication-guid"
                             },
                             "resources": [
                                 {
                                     "unit": "GIGABYTE",
                                     "quantity": 10
                                 },
                                 {
                                     "unit": "API_CALL",
                                     "quantity": 10
                                 }
                             ]
                         }
                     ]
                 }
             ]
         }	

        ```	 
		
**Resposta**

  * **Cabeçalho**
 
      * **Location**
    
          A URL para obter o registro de uso usando o método HTTP GET.


**Solicitação**

  * **Rota**
      
    ```
    GET /v1/metering/services/:service_id/usage/:usage_id?region=us-south
    ```
 * **Parâmetros de consulta**
   
     * **região **
	 
	     O ID da região de dados de uso. É possível usar **eu-gb** para Londres e **us-south** para Dallas.
		 
 * **Parâmetros**

     * **service_id**

         O ID do serviço. Esse ID deve ser exclusivo e deve ser um GUID.

     * **usage_id**

         O ID do registro de uso que você deseja recuperar.

 * **Cabeçalho**
    
     * **Autorização**

         Credenciais de autenticação básica. Os campos de nome do usuário e senha são os mesmos que na definição do broker de serviço. Para obter mais informações sobre o formato do esquema de autenticação básica, veja [RFC1945](http://tools.ietf.org/html/rfc1945#section-11.1).

**Response**

  * **Corpo**

      * **usage**

          Uma matriz de sequências que contêm os registros de uso que são retornados a partir desse ID de uso.


**Request**

  * **Rota**

    ```
    GET /v1/metering/service_instances/:instance_id/usage/:usage_id?region=us-south
    ```	  

  * **Parâmetros de consulta**

      * **região **

          O ID da região de dados de uso. É possível usar **eu-gb** para Londres e **us-south** para Dallas.	  
	
  * **Parâmetros**

      * **instance_id**
   
          O ID da instância de serviço.
  
      * **usage_id**

          O ID do registro de uso que você deseja recuperar.

  * **Cabeçalho**
 
      * **Autorização**
   
          Credenciais de autenticação básica. Os campos de nome do usuário e senha são os mesmos que na definição do broker de serviço. Para obter mais informações sobre o formato do esquema de autenticação básica, veja [RFC1945](http://tools.ietf.org/html/rfc1945#section-11.1).   
	  
**Resposta**

  * **Corpo**
  
      * **usage**
	    
		  Uma matriz de sequências que contêm os registros de uso que são retornados a partir desse ID de uso.
		

		
## LINKS RELACIONADOS		
		
### TUTORIAIS E AMOSTRAS

[Um serviço de amostra para Java](https://github.rtp.raleigh.ibm.com/bluemix/sample-services/tree/master/v2/java-v2)

[Um serviço de amostra para Node.js](https://github.rtp.raleigh.ibm.com/bluemix/sample-services/tree/master/v2/node-v2)

[Um serviço de amostra para Ruby](https://github.rtp.raleigh.ibm.com/bluemix/sample-services/tree/master/v2/ruby-v2)

### GENERAL

[API do broker de serviço de Cloud Foundry](http://docs.cloudfoundry.org/services/api.html)

[Metadados do catálogo de Cloud Foundry](http://docs.cloudfoundry.org/services/catalog-metadata.html)

[Gerenciamento de catálogo de Pivotal](http://docs.run.pivotal.io/services/api.html#catalog-mgmt)

[Interface com o usuário do Bluemix](https://ace.stage1.ng.bluemix.net)

[Implementando seu app com a interface da linha de comandos Cloud Foundry](https://www.stage1.eu-gb.bluemix.net/docs/starters/install_cli.html)

[Comandos cloud-cli](https://www.stage1.eu-gb.bluemix.net/docs/cli/cloudcli.html)

[Demarcação](http://daringfireball.net/projects/markdown/)

[API de fornecimento V2 no Cloud Foundry](http://docs.cloudfoundry.org/services/api.html#provisioning)

[Extensões de ativação da API do broker de serviço](http://rchgsa.ibm.com/~anhkhoa/public/projects/coe/docs/)


















