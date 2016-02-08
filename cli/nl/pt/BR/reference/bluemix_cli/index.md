{:shortdesc: .shortdesc}

# Comandos bx para interagir com o {{site.data.keyword.Bluemix_notm}}
{: #bluemix_cli}

*Última atualização:* 5 de janeiro de 2016

A interface de linha de comandos (CLI) do {{site.data.keyword.Bluemix}} fornece um conjunto de comandos que são agrupados por namespace para que os usuários interajam com o {{site.data.keyword.Bluemix_notm}}. Alguns comandos da CLI do {{site.data.keyword.Bluemix_notm}}, que são chamados de comandos bx, são wrappers de comandos cf existentes e outros são exclusivos para o {{site.data.keyword.Bluemix_notm}}. As informações a seguir listam todos os comandos que são suportados pela CLI do {{site.data.keyword.Bluemix_notm}} e inclui seus nomes, opções, uso, pré-requisitos, descrições e exemplos.
{:shortdesc}
 
**Nota:** *Pré-requisitos* listam quais ações são necessárias antes de usar o comando. Os comandos que não têm ações de pré-requisito listam **Nenhum**. Caso contrário, os pré-requisitos podem incluir uma ou mais das ações a seguir:
<dl>
<dt>Nó de Extremidade</dt>
<dd>Um terminal de API deve ser configurado por meio de <code>bluemix api</code> antes de usar o comando.</dd>
<dt>Login</dt>
<dd>É necessário efetuar login usando o comando <code>bluemix login</code> antes de usar esse comando.</dd>
<dt>Destino</dt>
<dd>O comando <code>bluemix target</code> deve ser usado para configurar uma organização e um espaço antes de usar esse comando.</dd>
</dl>

## bluemix help
Exiba a ajuda geral para comandos integrados de primeiro nível e namespaces suportados da CLI {{site.data.keyword.Bluemix_notm}} ou a ajuda para um comando ou namespace integrado específico.

```
bluemix help [COMMAND|NAMESPACE]
```

**Pré-requisitos**: Nenhum

**Opções de comando**:

*COMMAND*|*NAMESPACE* (opcional): O comando ou namespace para o qual a ajuda é exibida. Se não especificado, a ajuda geral para a CLI do {{site.data.keyword.Bluemix_notm}} será mostrada.

**Exemplos**:

Exiba a ajuda geral para a CLI do {{site.data.keyword.Bluemix_notm}}:

```
bluemix help
```

Exiba a ajuda para o namespace `catalog`:

```
bluemix help catalog
```

```
bluemix catalog help
```

Exiba a ajuda para o comando `info`:

```
bluemix help info
```

Exiba a ajuda para o comando `templates` sob o namespace `catalog`:

```
bluemix catalog help templates
```


## bluemix api
Configure ou visualize o terminal da API do {{site.data.keyword.Bluemix_notm}}. Esse comando agrupa o comando `cf api`.

```
bluemix api [API_ENDPOINT][--unset]
```

**Pré-requisitos**: Nenhum

**Opções de comando**:

*API_ENDPOINT* (opcional): O terminal de API que é o destino, por exemplo, https://api.ng.bluemix.net.  Se as opções *API_ENDPOINT* e `--unset` não forem ambas especificadas, o terminal de API atual será exibido.

`--unset` (opcional): Remova a configuração do terminal de API.

**Exemplos**:

Configure o terminal de API para api.ng.bluemix.net:

```
bluemix api api.ng.bluemix.net
```

Visualize o terminal de API atual:

```
bluemix api
```

Desconfigure o terminal de API:

```
bluemix api --unset
```


## bluemix login
Efetue login do usuário. Esse comando agrupa o comando `cf login`. As opções de comando são as mesmas que as opções de comando de `cf login`.

```
bluemix login [OPTIONS...]
```

**Pré-requisitos**: Terminal

**Opções de comando**:
Para obter informações sobre as opções suportadas pelo comando `login`, veja as informações de uso do comando `cf login` para comandos cf para gerenciar aplicativos.


## bluemix logout
Efetue logout do usuário. Esse comando agrupa o comando `cf logout`.

```
bluemix logout
```

**Pré-requisitos**: Nenhum


## bluemix target
Configure ou visualize a organização ou o espaço de destino. Esse comando agrupa o comando `cf target`.

```
bluemix target [-o ORG_NAME] [-s SPACE_NAME]
```

**Pré-requisitos**: Terminal, Login

**Opções de comando**:

-o *ORG_NAME* (opcional): O nome da organização que será o destino.

-s *SPACE_NAME* (opcional):  O nome do espaço que será o destino. 

Se -o *ORG_NAME* ou -s *SPACE_NAME* não forem especificados, a organização e o espaço atuais serão exibidos.

**Exemplos**:

Configure a organização atual como `MyOrg` e o espaço como `MySpace`:

```
bluemix target -o MyOrg -s MySpace
```

Visualize a organização e o espaço atuais:

```
bluemix target
```


## bluemix info
Visualize as informações básicas do {{site.data.keyword.Bluemix_notm}}, incluindo a região atual, a versão do controlador de nuvem e alguns terminais úteis, como terminais para login e a troca de token de acesso.

```
bluemix info
```

**Pré-requisitos**: Terminal





## bluemix regions
Visualize as informações para todas as regiões no {{site.data.keyword.Bluemix_notm}}.

```
bluemix regions
```

**Pré-requisitos**: Terminal


## bluemix region-set
Alterne para a região especificada. Esse comando redestina automaticamente para a mesma organização e o mesmo espaço na nova região, se possível. Caso contrário, o comando solicita que o usuário selecione uma nova organização e um novo espaço se o usuário já tiver efetuado login. O terminal de API é mudado apropriadamente.

```
bluemix region-set REGION_NAME
```

**Pré-requisitos**: Terminal

**Opções de comando**:

*REGION_NAME* (requerido): o nome da região para o qual você deseja alternar. É possível usar o comando `bluemix regions` para ver todos os nomes de região.

**Exemplos**:

Configure a região atual como `eu-gb`:

```
bluemix region-set eu-gb
```



## bluemix config
Grave os valores padrão no arquivo de configuração. 

```
bluemix config --http-timeout TIMEOUT_IN_SECONDS | --trace (true|false|path/to/file) | --color (true|false) | --locale (LOCALE|CLEAR)
```

**Pré-requisitos**: Nenhum

**Opções de comando**:

--http-timeout *TIMEOUT_IN_SECONDS*: o valor de tempo limite para solicitações de HTTP. O valor padrão é 60 segundos.

--trace true|false|*path/to/file*: rastreie solicitações de HTTP para o terminal ou o local especificado.

--color true|false: ative ou desative a saída de cor. A saída de cor é ativada por padrão.

--locale *LOCALE*: configure um código padrão de idioma. Se LOCALE for *CLEAR*, o código de idioma anterior será excluído.

Somente uma dessas opções pode ser especificada por vez. 

**Exemplos**:

Configure o tempo limite de solicitação de HTTP como 30 segundos:

```
bluemix config --http-timeout 30
```

Ative a saída de rastreio para solicitações de HTTP:

```
bluemix config --trace true
```

Rastreie solicitações de HTTP para um arquivo especificado */home/usera/my_trace*:

```
bluemix config --trace /home/usera/my_trace
```

Desative a saída de cor:

```
bluemix config --color false
```

Configure o código de idioma como zh_Hans:

```
bluemix config --locale zh_Hans
```

Limpe as configurações do código de idioma:

```
bluemix config --locale CLEAR
```










## bluemix list
Liste todos os aplicativos cf, contêineres, grupos de contêineres e grupos de VMs no espaço atual.

```
bluemix list [apps|containers|container-groups|vm-groups]
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

apps (opcional): Exiba somente as informações do aplicativo.

containers (opcional): Exiba somente as informações de contêineres.

container-groups (opcional): Exiba somente as informações sobre os grupos de contêineres.

vm-groups (opcional): Exiba somente as informações sobre os grupos de VMs.

Somente uma das opções `apps`, `containers`, `container-groups` ou `vm-groups` pode ser especificada por vez. Se nenhum deles for especificado, todos os apps cf, contêineres, grupos de contêineres e grupos de VMS serão listados.

**Exemplos**:

Liste todos os aplicativos cf:

```
bluemix list apps
```

Liste todas as instâncias de contêiner:

```
bluemix list containers
```

Liste todos os aplicativos, contêineres, grupos de contêineres e grupos de VMs:

```
bluemix list
```


## bluemix scale
Efetue scale in ou scale out do aplicativo cf ou grupo de contêineres para uma contagem de instâncias, cota do disco e tamanho de memória especificados. 

**Nota:** somente um número de instância pode ser especificado para ajuste de escala de um grupo de contêineres. Se nenhuma opção for especificada, esse comando listará a contagem de instâncias atual para o grupo de contêineres e também a cota do disco e o tamanho de memória para o aplicativo cf.

```
bluemix scale CF_APP_NAME|CONTAINER_GROUP_NAME [-i INSTANCE_COUNT][-k DISK_QUOTA] [-m MEMORY_SIZE]
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

*CF_APP_NAME*|*CONTAINER_GROUP_NAME* (requerido): o nome do aplicativo cf ou do grupo de contêineres a ser escalado.

-i *INSTANCE_COUNT* (opcional): o novo número de instância para o aplicativo cf ou o grupo de contêineres a ser escalado. Essa opção é a única opção válida para o grupo de contêineres a ser escalado.

-k *DISK_QUOTA* (opcional): a nova cota do disco do aplicativo cf. Não válida para escalar um grupo de contêineres.

-m *MEMORY_SIZE* (opcional): o novo tamanho de memória para o aplicativo cf. Não válida para escalar um grupo de contêineres.

**Exemplos**:

Exiba o número da instância atual para `my-container-group`:

```
bluemix scale my-container-group
```

Escale o `my-container-group` para 2 instâncias:

```
bluemix scale my-container-group -i 2
```

Escale o `my-java-app` para 3 instâncias, cota do disco de 8 G e tamanho de memória de 1024 M:

```
bluemix scale my-java-app -i 3 -k 8G -m 1024M
```


## bluemix curl
Executar um solicitação de HTTP bruto para {{site.data.keyword.Bluemix_notm}}. *Content-Type* é configurado como *application/json* por padrão. Esse comando envia um solicitação para o servidor do console {{site.data.keyword.Bluemix_notm}} (por exemplo, https://console.ng.bluemix.net) em vez do terminal de API cf (por exemplo, https://api.ng.bluemix.net).

```
bluemix curl PATH [OPTIONS...]
```

**Pré-requisitos**: Terminal, Login

**Opções de comando**:

*PATH* (requerido): O caminho de URL do recurso. Por exemplo, /rest/v2/apps.

*OPTIONS* (opcional): As opções que são suportados pelo comando `bluemix curl` são as mesmas que aquelas para o comando `cf curl`.

**Exemplos**:

Recupere as informações para todos os modelos de texto padrão:

```
bluemix curl /rest/templates
```


## bluemix iam orgs
Esse comando tem a mesma função e as mesmas opções do comando `cf orgs`, exceto que as regiões em que existem as organizações também são exibidas.


## bluemix iam org
Esse comando tem a mesma função e as mesmas opções do comando `cf org`, exceto que as regiões em que existe a organização são exibidas.


## bluemix iam org-create
Esse comando tem a mesma função e opções que o comando `cf create-org`.





## bluemix iam org-replicate
Replique uma organização a partir da região atual para outra região.

```
bluemix iam org-replicate ORG_NAME REGION_NAME
```

**Pré-requisitos**: Terminal, Login

**Opções de comando**:

*ORG_NAME* (requerido): o nome da organização existente que deve ser replicada.

*REGION_NAME* (requerido): o nome da região que hospeda a organização replicada.

**Exemplos**:

Replique a organização `OE_Runtimes_Scaling` para a região `eu-gb`:

```
bluemix iam org-replicate OE_Runtimes_Scaling eu-gb
```














## bluemix iam org-rename
Esse comando tem a mesma função e opções que o comando `cf renomear-org`.


## bluemix iam org-delete
Esse comando tem a mesma função e opções que o comando `cf delete-org`.


## bluemix iam spaces
Esse comando tem a mesma função e opções que o comando `cf spaces`.


## bluemix iam space
Esse comando tem a mesma função e opções que o comando `cf space`.


## bluemix iam space-create
Esse comando tem a mesma função e opções que o comando `cf create-space`.


## bluemix iam space-rename
Esse comando tem a mesma função e opções que o comando `cf rename-space`.


## bluemix iam space-delete
Esse comando tem a mesma função e opções que o comando `cf delete-space`.


## bluemix iam user-create
Esse comando tem a mesma função e opções que o comando `cf create-user`.


## bluemix iam user-delete
Esse comando tem a mesma função e opções que o comando `cf delete-user`.


## bluemix iam org-users
Esse comando tem a mesma função e opções que o comando `cf org-users`.


## bluemix iam org-role-set
Esse comando tem a mesma função e opções que o comando `cf set-org-role`.


## bluemix iam org-role-unset
Esse comando tem a mesma função e opções que o comando `cf unset-org-role`.


## bluemix iam space-users
Esse comando tem a mesma função e opções que o comando `cf space-users`.


## bluemix iam space-role-set
Esse comando tem a mesma função e opções que o comando `cf-set space-role`.


## bluemix iam space-role-unset
Esse comando tem a mesma função e opções que o comando `cf unset-space-role`.


## bluemix catalog templates
Visualize os modelos de texto padrão no Bluemix.

```
bluemix catalog templates [-d]
```

**Pré-requisitos**: Terminal, Login

**Opções de comando**:

-d (opcional): se a opção `-d` for especificada, a descrição de cada modelo também é exibida. Caso contrário, somente o ID e o nome de cada modelo serão mostrados.


## bluemix catalog template-run
Crie um aplicativo cf que seja baseado no modelo especificado com a URL e descrição especificadas. Por padrão, o novo app é iniciado automaticamente.

```
bluemix catalog template-run TEMPLATE_ID CF_APP_NAME [-u URL] [-d DESCRIPTION] [--no-start]
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

*TEMPLATE_ID* (requerido): O modelo no qual o aplicativo será baseado quando for criado. Use `bluemix templates` para ver todos os IDs dos modelos.

*CF_APP_NAME* (requerido): O nome do aplicativo cf a ser criado.

-u *URL* (opcional): A rota do aplicativo. Se não especificada, a rota será configurada pelo {{site.data.keyword.Bluemix_notm}} automaticamente com base no nome do app e domínio padrão.

-d *DESCRIPTION* (opcional): Descrição do aplicativo.

--no-start (opcional): Não inicie o aplicativo automaticamente após ele ser criado. Se não especificado, o aplicativo será iniciado automaticamente após ser criado.

**Exemplos**:

Crie um aplicativo cf `my-app` baseado no modelo `javaHelloWorld`:

```
bluemix catalog template-run javaHelloWorld my-app
```

Crie um aplicativo `my-ruby-app` baseado no modelo `rubyHelloWorld` com a rota `myrubyapp.ng.bluemix.net` e a descrição `Meu primeiro app ruby no {{site.data.keyword.Bluemix_notm}}.`:

```
bluemix catalog template-run rubyHelloWorld my-ruby-app -u myrubyapp.ng.bluemix.net -d "Meu primeiro app ruby no {{site.data.keyword.Bluemix_notm}}."
```

Crie um aplicativo `my-python-app` baseado no modelo `pythonHelloWorld` sem início automático:

```
bluemix catalog template-run pythonHelloWorld my-python-app --no-start
```




## bluemix catalog template-register

Registre um novo modelo de texto padrão no {{site.data.keyword.Bluemix_notm}}.

```
bluemix catalog template-register TEMPLATE_ID TEMPLATE_URL
```

**Pré-requisitos**: Terminal, Login

**Opções de comando**:

*TEMPLATE_ID* (requerido): o ID do novo modelo registrado.

*TEMPLATE_URL* (requerido): a URL que hospeda os metadados do novo modelo.

**Exemplos**:

Crie um modelo com o nome `javaHelloWorld`:

```
bluemix catalog template-register javaHelloWorld http://javaHelloWorld.ng.bluemix.net/info
```

## bluemix catalog template-deregister

Cancele o registro de um modelo de texto padrão existente. 

```
bluemix catalog template-deregister TEMPLATE_ID [-f]
```

**Pré-requisitos**: Terminal, Login

**Opções de comando**:

*TEMPLATE_ID* (requerido): use `bluemix catalog templates` para ver todos os IDs do modelo.

-f (opcional): force a remoção de registro sem confirmação.

**Exemplos**:

Cancele o registro do modelo `javaHelloWorld` sem confirmação:

```
bluemix catalog template-deregister javaHelloWorld -f
```


## bluemix catalog template-registry
Visualize o registro de modelo do {{site.data.keyword.Bluemix_notm}}.

```
bluemix catalog template-registry
```

**Pré-requisitos**: Terminal









## bluemix catalog service-broker

Visualize as informações do broker de serviço especificado.

```
bluemix catalog service-broker SERVICE_BROKER_NAME
```

**Pré-requisitos**: Terminal, Login

**Opções de comando**:

*SERVICE_BROKER_NAME* (requerido): o nome do broker de serviço a ser visitado.


## bluemix catalog service-broker-create
{: #bluemix_catalog_service_broker_create}
Criar um broker de serviço.

```
bluemix catalog service-broker-create SERVICE_BROKER_JSON_TEXT|SERVICE_BROKER_JSON_FILE [--no-billing]
```

**Pré-requisitos**: Terminal, Login

**Opções de comando**:

*SERVICE_BROKER_JSON_TEXT*|*SERVICE_BROKER_JSON_FILE* (requerido): o JSON que descreve o novo broker de serviço a ser criado. É possível usar o nome do arquivo JSON ou usar diretamente o texto JSON.

--no-billing (opcional): se essa opção for especificada, o faturamento será desativado para o broker de serviço.  

**Exemplos**:

Crie um broker de serviço com um arquivo JSON:

```
bluemix catalog service-broker-create ./broker.json
```

Crie um novo broker de serviço com um texto JSON e sem faturamento:

```
bluemix catalog service-broker-create '{"name":"test_broker", ...}' --no-billing
```

O exemplo a seguir mostra um JSON do broker de serviço com todos os campos necessários:

```
{
    "name": "my_broker",  // o nome do broker de serviço
    "broker_url": "http://my_broker.ng.bluemix.net"  // a URL que aponta para os metadados do broker de serviço
    "auth_username": "username",
	"auth_password": "password",  // o nome do usuário e a senha para visitar a URL do broker de serviço. O nome do usuário e a senha devem ser enviados com autorização básica de HTTP.
    "visibilities": [
        {"organization_name": "OE_Runtimes_Scaling"}
    ]
}
```


## bluemix catalog service-broker-update
Atualize um broker de serviço existente.

```
bluemix catalog service-broker-update ORIGINAL_BROKER_NAME SERVICE_BROKER_JSON_TEXT|SERVICE_BROKER_JSON_FILE
```

**Pré-requisitos**: Terminal, Login

**Opções de comando**:

*ORIGINAL_BROKER_NAME* (requerido): o nome do broker de serviço a ser atualizado.

*SERVICE_BROKER_JSON_TEXT*|*SERVICE_BROKER_JSON_FILE* (requerido): o novo JSON que descreve o broker de serviço. É possível usar o nome do arquivo JSON ou usar diretamente o texto JSON.

**Exemplos**:

Atualize um broker de serviço existente `auto-scaling`:

```
bluemix catalog service-broker-update auto-scaling ./auto-scaling.json
```

Veja [bluemix catalog service-broker-create](#bluemix_catalog_service_broker_create) para obter mais detalhes sobre o formato JSON do broker de serviço.


## bluemix catalog service-broker-delete

Exclua um broker de serviço especificado.

```
bluemix catalog service-broker-delete SERVICE_BROKER_NAME [-f]
```

**Pré-requisitos**: Terminal, Login

**Opções de comando**:

*SERVICE_BROKER_NAME* (requerido): o nome do broker de serviço a ser excluído.

-f (opcional): force a exclusão sem confirmação.

**Exemplos**:

Exclua o broker de serviço `auto-scaling` sem confirmação:

```
bluemix catalog service-broker-delete auto-scaling -f
```














## bluemix network routes
Esse comando tem a mesma função e opções que o comando `cf routes`.


## bluemix network route-check
Esse comando tem a mesma função e opções que o comando `cf check-route`.


## bluemix network route-map
Mapeie uma rota para um aplicativo cf ou grupo de contêineres existente que tenha o domínio e o nome do host especificados.

```
bluemix network route-map CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

*CF_APP_NAME*|*CONTAINER_GROUP_NAME* (requerido): O nome do aplicativo cf ou grupo de contêineres a ser mapeado com uma rota.

*DOMAIN* (requerido): O domínio da rota. Por exemplo, mybluemix.net ou ng.bluemix.net. 

-n *HOST_NAME* (opcional): O nome do host da rota. Se não fornecido, o nome do host será configurado para o nome do app ou grupo de contêineres por padrão.

**Exemplos**:

Mapeie uma rota para `my-app` com o domínio especificado: 

```
bluemix network route-map my-app mybluemix.net
```

Mapeie uma rota para 'my-container-group' com o domínio e nome do host especificados:

```
bluemix network route-map my-container-group ng.bluemix.net -n abc
```


## bluemix network route-unmap
Remova o mapeamento da rota especificada de um aplicativo cf ou grupo de contêineres existente.

```
bluemix network route-unmap CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

*CF_APP_NAME*|*CONTAINER_GROUP_NAME* (requerido): O nome do aplicativo cf ou grupo de contêineres.

*DOMAIN* (requerido): O domínio da rota (por exemplo, mybluemix.net ou ng.bluemix.net). 

-n *HOST_NAME* (opcional): O nome do host da rota. Se não fornecido, o nome do host será configurado para o nome do app ou grupo de contêineres por padrão.

**Exemplos**:

Remova o mapeamento `my-app.mybluemix.net` de  `my-app`:

```
bluemix network route-unmap my-app mybluemix.net
```

Remova o mapeamento `abc.ng.bluexmix.net` de `my-container-group`:

```
bluemix network route-unmap my-container-group ng.bluemix.net -n abc
```


## bluemix network route-create
Esse comando tem a mesma função e opções que o comando `cf create-route`.


## bluemix network route-delete
Esse comando tem a mesma função e opções que o comando `cf delete-route`.


## bluemix network orphaned-routes-delete
Esse comando tem a mesma função e opções que o comando `cf delete-orphaned-routes`.


## bluemix network domains
Esse comando tem a mesma função e opções que o comando `cf domains`.


## bluemix network domain-create
Esse comando tem a mesma função e opções que o comando `cf create-domain`.


## bluemix network domain-delete
Esse comando tem a mesma função e opções que o comando `cf delete-domain`.


## bluemix network shared-domain-create
Esse comando tem a mesma função e opções que o comando `cf create-shared-domain`.


## bluemix network shared-domain-delete
Esse comando tem a mesma função e opções que o comando `cf delete-shared-domain`.




## bluemix security cert

Liste as informações de certificado para o host especificado.

```
bluemix security cert HOST_NAME
```

**Pré-requisitos**: Terminal, Login

**Opções de comando**:

*HOST_NAME* (requerido): o nome do servidor que hospeda o certificado.

**Exemplos**:

Veja o certificado no host `ibmcxo-eventconnect.com`:

```
bluemix security cert ibmcxo-eventconnect.com
```


## bluemix security cert-add

Inclua um certificado no domínio especificado na organização atual.

```
bluemix security cert-add DOMAIN -k PRIVATE_KEY_FILE -c CERT_FILE [-p PASSWORD][-i INTERMEDIATE_CERT_FILE] [--verify-client]
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

*DOMAIN* (requerido): o domínio ao qual o certificado é incluído.

-k *PRIVATE_KEY_FILE* (requerido): o caminho do arquivo de chave privado.

-c *CERT_FILE* (requerido): o caminho do arquivo de certificado.

-p *PASSWORD* (opcional): a senha do certificado.

-i *INTERMEDIATE_CERT_FILE* (opcional): o caminho do arquivo de certificado intermediário.

--verify-client (opcional): indica se deve ativar a verificação do certificado de cliente. 

**Exemplos**:

Inclua um certificado no domínio `ibmcxo-eventconnect.com`:

```
bluemix security cert-add ibmcxo-eventconnect.com -k key_file.key -c cert_file.crt -p 123 -i inter_cert.cert
```


## bluemix security cert-remove
Remova um certificado do domínio especificado na organização atual.

```
bluemix security cert-remove DOMAIN [-f]
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

*DOMAIN* (requerido): o domínio do qual remover o certificado.

-f (opcional): force a exclusão sem confirmação.








## bluemix plugin repos
Liste todos os repositórios de plug-in que estão registrados na CLI do {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin repos
```

**Pré-requisitos**: Nenhum


## bluemix plugin repo-add
Inclua um novo repositório de plug-in na CLI do {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin repo-add REPO_NAME REPO_URL
```

**Pré-requisitos**: Nenhum

**Opções de comando**:

*REPO_NAME* (requerido): O nome do repositório a ser incluído. É possível definir seu próprio nome para cada repositório.

*REPO_URL* (requerido): A URL do repositório a ser incluído. A URL do repositório deve conter o protocolo (por exemplo, http://plugins.ng.bluemix.net em vez de plugins.ng.bluemix.net). http://plugins.ng.bluemix.net é o repositório de plug-in oficial da CLI do {{site.data.keyword.Bluemix_notm}}.

**Exemplos**:

Inclua o repositório de plug-in oficial da CLI do Bluemix CLI como `bluemix-repo`:

```
bluemix plugin repo-add bluemix-repo http://plugins.ng.bluemix.net
```


## bluemix plugin repo-remove
Remova um repositório de plug-in da CLI do {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin repo-remove REPO_NAME
```

**Pré-requisitos**: Nenhum

**Opções de comando**:

*REPO_NAME* (requerido): O nome do repositório a ser removido.

**Exemplos**:

Remova o repositório `bluemix-repo` da CLI do {{site.data.keyword.Bluemix_notm}}:

```
bluemix plugin repo-remove bluemix-repo
```


## bluemix plugin repo-plugin-list
Liste todos os plug-ins disponíveis em todos os repositórios incluídos ou um repositório específico.

```
bluemix plugin repo-plugin-list [-r REPO_NAME]
```

**Pré-requisitos**: Nenhum

**Opções de comando**:

-r *REPO_NAME* (opcional): Liste somente os plug-ins no repositório especificado.

**Exemplos**:

Liste todos os plug-ins em todos os repositórios incluídos:

```
bluemix plugin repo-plugin-list
```

Liste todos os plug-ins no repositório `bluemix-repo`:

```
bluemix plugin repo-plugin-list -r bluemix-repo
```


## bluemix plugin list
Liste todos os plug-ins instalados na CLI do {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin list
```

**Pré-requisitos**: Nenhum


## bluemix plugin install
Instale a versão específica de plug-in na CLI do {{site.data.keyword.Bluemix_notm}} a partir do caminho ou repositório especificado.

```
bluemix plugin install PLUGIN_PATH|PLUGIN_NAME [-r REPO_NAME][-v VERSION]
```

**Pré-requisitos**: Nenhum

**Opções de comando**:

*PLUGIN_PATH*|*PLUGIN_NAME* (requerido): se `-r *REPO_NAME*` não for especificado, o plug-in será instalado a partir do caminho local ou da URL remota.

-r *REPO_NAME* (opcional): O nome do repositório no qual o plug-in binário está localizado.
-v *VERSION* (opcional): a versão do plug-in a ser instalado. Se ela não for fornecida, a versão mais recente do plug-in será instalada. Essa opção é válida somente quando você instala o plug-in a partir do repositório.

**Exemplos**:

Instale um plug-in a partir do arquivo local:

```
bluemix plugin install /downloads/new_plugin
```

Instale um plug-in a partir da URL remota:

```
bluemix plugin install http://plugins.ng.bluemix.net/downloads/new_plugin
```

Instale o plug-in `IBM-Containers` da versão mais recente do repositório `bluemix-repo`:

```
bluemix plugin install IBM-Containers -r bluemix-repo
```
Instale o plug-in `IBM-Containers` com a versão `0.5.800` do repositório `bluemix-repo`:

```
bluemix plugin install IBM-Containers -r bluemix-repo -v 0.5.800
```






## bluemix plugin uninstall
Desinstale o plug-in especificado a partir da CLI do {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin uninstall PLUGIN_NAME
```

**Pré-requisitos**: Nenhum

**Opções de comando**:

*PLUGIN_NAME* (requerido): O nome do plug-in a ser desinstalado.

**Exemplos**:

Desinstale o plug-in `IBM-Containers` que foi instalado anteriormente:

```
bluemix plugin uninstall IBM-Containers
```
