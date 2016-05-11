---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Comandos do {{site.data.keyword.Bluemix_notm}} (bx)
{: #bluemix_cli}

*Última atualização: 15 de abril de 2016*

A interface de linha de comandos (CLI) do {{site.data.keyword.Bluemix_notm}} fornece um conjunto de comandos que são agrupados por namespace para que os usuários interajam com o {{site.data.keyword.Bluemix_notm}}. Alguns comandos do {{site.data.keyword.Bluemix_notm}} são wrappers de comandos cf existentes, enquanto que outros fornecem recursos para usuários do {{site.data.keyword.Bluemix_notm}}. As informações a seguir listam todos os comandos que são suportados pela CLI do {{site.data.keyword.Bluemix_notm}} e inclui seus nomes, opções, uso, pré-requisitos, descrições e exemplos.
{:shortdesc}
 
**Nota:** *Pré-requisitos* listam quais ações são necessárias antes de usar o comando. Os comandos que não têm ações de pré-requisito listam **Nenhum**. Caso contrário, os pré-requisitos podem incluir uma ou mais das ações a seguir:
<dl>
<dt>Nó de Extremidade</dt>
<dd>Um terminal de API deve ser configurado por meio de <code>bluemix api</code> antes de usar o comando.</dd>
<dt>Login</dt>
<dd>É necessário efetuar login usando o comando <code>bluemix login</code> antes de usar esse comando.</dd>
<dt>Destino</dt>
<dd>O comando <code>bluemix target</code> deve ser usado para configurar uma organização e um espaço antes de usar esse comando.</dd>
<dt>Docker</dt>
<dd>A CLI do Docker (docker) deve estar instalada para executar esse comando.</dd>
</dl>

É possível usar os comando a seguir do {{site.data.keyword.Bluemix_notm}}:

 <table role="presentation"> 
 <tbody> 
 <tr> 
 <td>[bluemix help](index.html#bluemix_help)</td> 
 <td>[bluemix api](index.html#bluemix_api)</td> 
 <td>[bluemix login](index.html#bluemix_login)</td>
 <td>[bluemix logout](index.html#bluemix_logout)</td>
 <td>[bluemix target](index.html#bluemix_target)</td>
 </tr> 
 <tr> 
 <td> 
 [bluemix info](index.html#bluemix_info) </td> 
 <td>[bluemix config](index.html#bluemix_config)</td> 
 <td>[bluemix list](index.html#bluemix_list)</td>
 <td>[bluemix scale](index.html#bluemix_scale)</td>
 <td>[bluemix curl](index.html#bluemix_curl)</td>
 </tr>
 
 <tr> 
 <td>[bluemix iam orgs](index.html#bluemix_iam_orgs) </td> 
 <td>[bluemix iam org](index.html#bluemix_iam_org)</td> 
 <td>[bluemix iam org-create](index.html#bluemix_iam_org_create)</td>
 <td>[bluemix iam org-replicate](index.html#bluemix_iam_org_replicate)</td>
 <td>[bluemix iam org-rename](index.html#bluemix_iam_org_rename)</td>
 </tr>
 
 <tr> 
 <td>[bluemix iam org-delete](index.html#bluemix_iam_org_delete) </td> 
 <td>[bluemix iam spaces](index.html#bluemix_iam_spaces)</td> 
 <td>[bluemix iam space](index.html#bluemix_iam_space)</td>
 <td>[bluemix iam space-create](index.html#bluemix_iam_space_create)</td>
 <td>[bluemix iam space-rename](index.html#bluemix_iam_space_rename)</td>
 </tr>
 
 <tr> 
 <td>[bluemix iam space-delete](index.html#bluemix_iam_space_delete) </td> 
 <td>[bluemix iam account-users](index.html#bluemix_iam_account-users)</td> 
 <td>[bluemix iam account-user-invite](index.html#bluemix_iam_account-user-invite)</td>
 <td>[bluemix iam org-users](index.html#bluemix_iam_org_users)</td>
 <td>[bluemix iam org-role-set](index.html#bluemix_iam_org_role_set)</td>
 </tr>
 
 <tr> 
 <td>[bluemix iam org-role-unset](index.html#bluemix_iam_org_role_unset) </td> 
 <td>[bluemix iam space-users](index.html#bluemix_iam_space_users)</td> 
 <td>[bluemix iam space-role-set](index.html#bluemix_iam_space_role_set)</td>
 <td>[bluemix iam space-role-unset](index.html#bluemix_iam_space_role_unset)</td>
 <td>[bluemix app push](index.html#bluemix_app_push)</td>
 </tr>
 
 <tr> 
 <td>[bluemix app list](index.html#bluemix_app_list) </td> 
 <td>[bluemix app show](index.html#bluemix_app_show)</td> 
 <td>[bluemix app scale](index.html#bluemix_app_scale)</td>
 <td>[bluemix app delete](index.html#bluemix_app_delete)</td>
 <td>[bluemix app rename](index.html#bluemix_app_rename)</td>
 </tr>
 
 <tr> 
 <td>[bluemix app start](index.html#bluemix_app_start) </td> 
 <td>[bluemix app stop](index.html#bluemix_app_stop)</td> 
 <td>[bluemix app restart](index.html#bluemix_app_restart)</td>
 <td>[bluemix app restage](index.html#bluemix_app_restage)</td>
 <td>[bluemix app instance-restart](index.html#bluemix_app_instance_restart)</td>
 </tr>
 
 <tr> 
 <td>[bluemix app events](index.html#bluemix_app_events) </td> 
 <td>[bluemix app files](index.html#bluemix_app_files)</td> 
 <td>[bluemix app logs](index.html#bluemix_app_logs)</td>
 <td>[bluemix app env](index.html#bluemix_app_env)</td>
 <td>[bluemix app env-set](index.html#bluemix_app_env_set)</td>
 </tr>
 
 <tr> 
 <td>[bluemix app env-unset](index.html#bluemix_app_env_unset) </td> 
 <td>[bluemix app stacks](index.html#bluemix_app_stacks)</td> 
 <td>[bluemix app stack](index.html#bluemix_app_stack)</td>
 <td>[bluemix app manifest-create](index.html#bluemix_app_manifest_create)</td>
 <td>[bluemix service offerings](index.html#bluemix_service_offerings)</td>
 </tr>
 
 <tr> 
 <td>[bluemix service list](index.html#bluemix_service_list) </td> 
 <td>[bluemix service show](index.html#bluemix_service_show)</td> 
 <td>[bluemix service create](index.html#bluemix_service_create)</td>
 <td>[bluemix service update](index.html#bluemix_service_update)</td>
 <td>[bluemix service delete](index.html#bluemix_service_delete)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix service rename](index.html#bluemix_service_rename) </td> 
 <td>[bluemix service bind](index.html#bluemix_service_bind)</td> 
 <td>[bluemix service unbind](index.html#bluemix_service_unbind)</td>
 <td>[bluemix service key-create](index.html#bluemix_service_key_create)</td>
 <td>[bluemix service key-delete](index.html#bluemix_service_key_delete)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix service keys](index.html#bluemix_service_keys) </td> 
 <td>[bluemix service key-show](index.html#bluemix_service_key_show)</td> 
 <td>[bluemix service user-provided-create](index.html#bluemix_service_user_provided_create)</td>
 <td>[bluemix service user-provided-update](index.html#bluemix_service_user_provided_update)</td>
 <td>[bluemix catalog templates](index.html#bluemix_catalog_templates)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix catalog template](index.html#bluemix_catalog_template) </td> 
 <td>[bluemix catalog template-run](index.html#bluemix_catalog_template_run)</td> 
 <td>[bluemix network regions](index.html#bluemix_network_regions)</td>
 <td>[bluemix network region-set](index.html#bluemix_network_region_set)</td>
 <td>[bluemix network routes](index.html#bluemix_network_routes)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix network route-check](index.html#bluemix_network_route_check)</td> 
 <td>[bluemix network route-map](index.html#bluemix_network_route_map)</td> 
 <td>[bluemix network route-unmap](index.html#bluemix_network_route_unmap)</td>
 <td>[bluemix network route-create](index.html#bluemix_network_route_create)</td>
 <td>[bluemix network route-delete](index.html#bluemix_network_route_delete)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix network orphaned-routes-delete](index.html#bluemix_network_orphaned_routes_delete)</td> 
 <td>[bluemix network domains](index.html#bluemix_network_domains)</td> 
 <td>[bluemix network domain-create](index.html#bluemix_network_domain_create)</td>
 <td>[bluemix network domain-delete](index.html#bluemix_network_domain_delete)</td>
 <td>[bluemix network shared-domain-create](index.html#bluemix_network_shared_domain_create)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix network shared-domain-delete](index.html#bluemix_network_shared_domain_delete)</td> 
 <td>[bluemix security cert](index.html#bluemix_security_cert)</td> 
 <td>[bluemix security cert-add](index.html#bluemix_security_cert_add)</td>
 <td>[bluemix security cert-remove](index.html#bluemix_security_cert_remove)</td>
 <td>[bluemix plugin repos](index.html#bluemix_plugin_repos)</td>
 </tr>
 
 <tr> 
 <td>[bluemix plugin repo-add](index.html#bluemix_plugin_repo_add)</td> 
 <td>[bluemix plugin repo-remove](index.html#bluemix_plugin_repo_remove)</td> 
 <td>[bluemix plugin repo-plugins](index.html#bluemix_plugin_repo_plugins)</td>
 <td>[bluemix plugin list](index.html#bluemix_plugin_list)</td>
 <td>[bluemix plugin install](index.html#bluemix_plugin_install)</td>
 </tr>
 
 <tr> 
 <td>[bluemix plugin uninstall](index.html#bluemix_plugin_uninstall)</td> 
 <td>[bluemix ic init](index.html#bluemix_ic_init)</td> 
 <td>[bluemix ic attach](index.html#bluemix_ic_attach)</td>
 <td>[bluemix ic build](index.html#bluemix_ic_build)</td>
 <td>[bluemix ic create](index.html#bluemix_ic_create)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic cpi](index.html#bluemix_ic_cpi)</td> 
 <td>[bluemix ic exec](index.html#bluemix_ic_exec)</td> 
 <td>[bluemix ic groups](index.html#bluemix_ic_groups)</td>
 <td>[bluemix ic group-inspect](index.html#bluemix_ic_group_inspect)</td>
 <td>[bluemix ic group-instances](index.html#bluemix_ic_group_instances)</td>
 </tr>
 
 <tr> 
 <td>[bluemix ic group-create](index.html#bluemix_ic_group_create)</td> 
 <td>[bluemix ic group-update](index.html#bluemix_ic_group_update)</td> 
 <td>[bluemix ic group-remove](index.html#bluemix_ic_group_remove)</td>
 <td>[bluemix ic images](index.html#bluemix_ic_images)</td>
 <td>[bluemix ic inspect](index.html#bluemix_ic_inspect)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic info](index.html#bluemix_ic_info)</td> 
 <td>[bluemix ic ips](index.html#bluemix_ic_ips)</td> 
 <td>[bluemix ic ip-request](index.html#ip_request)</td>
 <td>[bluemix ic ip-release](index.html#bluemix_ic_ip_release)</td>
 <td>[bluemix ic ip-bind](index.html#bluemix_ic_ip_bind)</td>
 </tr>
 
 <tr> 
 <td>[bluemix ic ip-unbind](index.html#bluemix_ic_ip_unbind)</td> 
 <td>[bluemix ic kill](index.html#bluemix_ic_kill)</td> 
 <td>[bluemix ic namespace-get](index.html#bluemix_ic_namespace_get)</td>
 <td>[bluemix ic namespace-set](index.html#bluemix_ic_namespace_set)</td>
 <td>[bluemix ic pause](index.html#pause)</td>
 </tr>
 
 <tr> 
 <td>[bluemix ic unpause](index.html#unpause)</td> 
 <td>[bluemix ic port](index.html#bluemix_ic_port)</td> 
 <td>[bluemix ic ps](index.html#bluemix_ic_ps)</td>
 <td>[bluemix ic restart](index.html#bluemix_ic_restart)</td>
 <td>[bluemix ic rm](index.html#bluemix_ic_rm)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic rmi](index.html#bluemix_ic_rmi)</td> 
 <td>[bluemix ic run](index.html#bluemix_ic_run)</td> 
 <td>[bluemix ic route-map](index.html#bluemix_ic_route_map)</td>
 <td>[bluemix ic route-unmap](index.html#bluemix_ic_route_unmap)</td>
 <td>[bluemix ic start](index.html#ic_start)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic stop](index.html#ic_stop)</td> 
 <td>[bluemix ic stats](index.html#bluemix_ic_stats)</td> 
 <td>[bluemix ic top](index.html#bluemix_ic_top)</td>
 <td>[bluemix ic volumes](index.html#bluemix_ic_volumes)</td>
 <td>[bluemix ic volume-inspect](index.html#bluemix_ic_volume_inspect)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic volume-create](index.html#bluemix_ic_volume_create)</td> 
 <td>[bluemix ic volume-remove](index.html#bluemix_ic_volume_remove)</td> 
 <td>[bluemix ic volume-fs](index.html#bluemix_ic_volume_fs)</td> 
 <td>[bluemix ic volume-fs-create](index.html#bluemix_ic_volume_fs_create)</td> 
 <td>[bluemix ic volume-fs-remove](index.html#bluemix_ic_volume_fs_remove)</td> 
 </tr>
 
 <tr>
 <td>[bluemix ic volume-fs-inspect](index.html#bluemix_ic_volume_fs_inspect)</td>
 <td>[bluemix ic volume-fs-flavors](index.html#bluemix_ic_volume_fs_flavors)</td> 
 <td>[bluemix ic wait](index.html#bluemix_ic_wait)</td>
 <td>[bluemix ic version](index.html#bluemix_ic_version)</td>
 </tr>
 
 
 </tbody> 
 </table> 

  

## bluemix help
{: #bluemix_help}
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

Exiba a ajuda para o comando `info`:

```
bluemix help info
```

Exiba a ajuda para o namespace `ic`:

```
bluemix help ic
```

ou 

```
bluemix ic help
```

Exiba a ajuda para o comando `group-create` sob o namespace `ic`:

```
bluemix ic help group-create
```


## bluemix api
{: #bluemix_api}
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
{: #bluemix_login}

Efetue login do usuário. Esse comando agrupa o comando `cf login`. As opções de comando são as mesmas que as opções de comando de `cf login`.

```
bluemix login [OPTIONS...]
```

**Pré-requisitos**: Terminal

**Opções de comando**:
Para obter informações sobre as opções suportadas pelo comando `login`, veja as informações de uso do comando `cf login` para comandos cf para gerenciar aplicativos.


## bluemix logout
{: #bluemix_logout}

Efetue logout do usuário. Esse comando agrupa o comando `cf logout`.

```
bluemix logout
```

**Pré-requisitos**: Nenhum


## bluemix target
{: #bluemix_target}


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
{: #bluemix_info}

Visualize as informações básicas do {{site.data.keyword.Bluemix_notm}}, incluindo a região atual, a versão do controlador de nuvem e alguns terminais úteis, como terminais para login e a troca de token de acesso.

```
bluemix info
```

**Pré-requisitos**: Terminal


## bluemix config
{: #bluemix_config}


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
{: #bluemix_list}

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

Somente um destes, `apps`, `containers`, `container-groups` ou `vm-groups`, pode ser especificado por vez. Se nenhum deles for especificado, todos os apps cf, contêineres, grupos de contêineres e grupos de VMS serão listados.

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
{: #bluemix_scale}

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
{: #bluemix_curl}

Executar um solicitação de HTTP bruto para {{site.data.keyword.Bluemix_notm}}. *Content-Type* é configurado como *application/json* por padrão. Esse comando envia a solicitação para o {{site.data.keyword.Bluemix_notm}} Multi-Cloud Control Proxy. Para caminhos suportados, consulte as definições de caminho da API no [documento da API do CloudFoundry](http://apidocs.cloudfoundry.org/){: new_window}.

```
bluemix curl PATH [OPTIONS...]
```

**Pré-requisitos**: Terminal, Login

**Opções de comando**:

*PATH* (requerido): O caminho de URL do recurso. Por exemplo, /v2/apps.

*OPTIONS* (opcional): As opções que são suportados pelo comando `bluemix curl` são as mesmas que aquelas para o comando `cf curl`.

**Exemplos**:

Visualize as informações para todas as organizações da conta atual: 

```
bluemix curl /v2/organizations
```


## bluemix iam orgs
{: #bluemix_iam_orgs}

Liste todas as organizações

```
bluemix iam orgs [-r REGION --guid]
```

**Pré-requisitos**: Terminal, Login

**Opções de comando**:

*-r REGION* (opcional): Para qual região as informações da organização são mostradas. Se configurado como 'all', todas as organizações em todas as regiões serão listadas.

*--guid* (opcional): Exiba o GUID das organizações.

**Exemplos**:
Liste todas as organizações na região: `us-south` com o GUID exibido

```
bluemix iam orgs -r us-south --guid
```

## bluemix iam org
{: #bluemix_iam_org}

Mostre as informações para a organização especificada.

```
bluemix iam org ORG_NAME [--guid]
```

**Pré-requisitos**: Terminal, Login

**Opções de comando**:

*ORG_NAME* (requerido): O nome da organização.

*--guid* (opcional): Exiba o GUID da organização.


**Exemplos**:
Mostrar as informações da organização `IBM` com o GUID exibido

```
bluemix iam org IBM --guid
```

## bluemix iam org-create
{: #bluemix_iam_org_create}

Criar uma nova organização. Essa operação pode ser executada somente pelo proprietário da conta. 

```
bluemix iam org-create ORG_NAME
```

**Pré-requisitos**: Terminal, Login

**Opções de comando**:

*ORG_NAME* (requerido): O nome da organização que está sendo criada.

**Exemplos**:
Crie uma organização denominada `IBM`.

```
bluemix iam org-create IBM
```


## bluemix iam org-replicate
{: #bluemix_iam_org_replicate}

Replique uma organização a partir da região atual para outra região.

```
bluemix iam org-replicate ORG_NAME REGION_NAME
```

**Pré-requisitos**: Terminal, Login

**Opções de comando**:

*ORG_NAME* (requerido): o nome da organização existente que deve ser replicada.

*REGION_NAME* (requerido): o nome da região que hospeda a organização replicada.

**Exemplos**:

Replique a organização `myorg` para a região `eu-gb`:

```
bluemix iam org-replicate myorg eu-gb
```


## bluemix iam org-rename
{: #bluemix_iam_org_rename}

Renomeie uma organização. Essa operação pode ser executada somente por um gerenciador de organização. 

```
bluemix iam org-rename OLD_ORG_NAME NEW_ORG_NAME
```

**Pré-requisitos**: Terminal, Login

**Opções de comando**:

*OLD_ORG_NAME* (requerido): O nome antigo da organização que deve ser renomeada. 

*NEW_ORG_NAME* (requerido): O novo nome da organização para o qual ela é renomeada. 


## bluemix iam org-delete
{: #bluemix_iam_org_delete}

Exclua a organização especificada na região atual. 

```
bluemix iam org-delete ORG_NAME [-f --all]
```

**Pré-requisitos**: Terminal, Login

**Opções de comando**:

*ORG_NAME* (requerido): O nome da organização existente que deve ser excluída. 

*-f* (opcional): Force a exclusão sem confirmação. 

*--all* (opcional): Exclua a organização de todas as regiões.


## bluemix iam spaces
{: #bluemix_iam_spaces}

Esse comando tem a mesma função e opções que o comando `cf spaces`.


## bluemix iam space
{: #bluemix_iam_space}

Esse comando tem a mesma função e opções que o comando `cf space`.


## bluemix iam space-create
{: #bluemix_iam_space_create}

Esse comando tem a mesma função e opções que o comando `cf create-space`.


## bluemix iam space-rename
{: #bluemix_iam_space_rename}


Esse comando tem a mesma função e opções que o comando `cf rename-space`.


## bluemix iam space-delete
{: #bluemix_iam_space_delete}


Esse comando tem a mesma função e opções que o comando `cf delete-space`.


## bluemix iam account-users
{: #bluemix_iam_account_users}

Exibe os usuários associados à conta. Essa operação pode ser executada somente pelo proprietário da conta. 

```
bluemix iam account-users
```

## bluemix iam account-user-invite
{: #bluemix_iam_account-user_inviate}


Convida um usuário para a conta com uma função de organização e espaço já configurada. Essa operação pode ser executada somente pelo proprietário da conta. 

```
bluemix iam account-user-invite USER_NAME ORG_NAME ORG_ROLE SPACE_NAME SPACE_ROLE
```

**Pré-requisitos**: Terminal, Login


**Opções de comando**:

*USER_NAME* (requerido): O nome do usuário que está sendo convidado. 

*ORG_NAME* (requerido): O nome da organização para a qual esse usuário é convidado. 

*ORG_ROLE* (requerido): o nome da função de organização para a qual esse usuário é convidado. Por
exemplo:

<dl>
<dt>OrgManager</dt>
<dd>Essa função pode convidar e gerenciar usuários, selecionar e mudar planos e configurar limites de gastos. </dd>
<dt>BillingManager</dt>
<dd>Essa função pode criar e gerenciar a conta de cobrança e informações de pagamento. </dd>
<dt>OrgAuditor</dt>
<dd>Essa função possui acesso somente leitura para informações e relatórios da organização. </dd>
</dl> 

*SPACE_NAME* (requerido): O nome do espaço para o qual esse usuário é convidado. 

*SPACE_ROLE* (requerido): O nome da função de espaço para a qual esse usuário é convidado. Por
exemplo:

<dl>
<dt>SpaceManager</dt>
<dd>Essa função pode convidar e gerenciar usuários e ativar recursos para um determinado espaço. </dd>
<dt>SpaceDeveloper</dt>
<dd>Essa função pode criar e gerenciar apps e serviços e ver logs e relatórios. </dd>
<dt>SpaceAuditor</dt>
<dd>Essa função pode visualizar logs, relatórios e configurações para o espaço. </dd>
</dl> 

**Exemplos**:

Convide o usuário `Mary` para a organização `IBM` como função `OrgManager` e o espaço `Cloud` como função `SpaceAuditor`: 

```
bluemix iam account-user-inviate Mary IBM OrgManager Cloud SpaceAuditor
```

## bluemix iam org-users
{: #bluemix_iam_org_users}

Exiba usuários na organização especificada por função. 

```
bluemix iam org-users ORG_NAME [-a]
```

**Pré-requisitos**: Terminal, Login

**Opções de comando**:

*ORG_NAME* (requerido): O nome da organização.

*-a* (opcional): Liste todos os usuários na organização especificada, não agrupados por função. 


## bluemix iam org-role-set
{: #bluemix_iam_org_role_set}

Designe uma função de organização a um usuário. Essa operação pode ser executada somente por um gerenciador de organização. 

```
bluemix iam org-role-set USER_NAME ORG_NAME ORG_ROLE
```

**Pré-requisitos**: Terminal, Login

**Opções de comando**:

*USER_NAME* (requerido): O nome do usuário que está sendo designado. 

*ORG_NAME* (requerido): O nome da organização à qual esse usuário está designado. 

*ORG_ROLE* (requerido): O nome da função de organização à qual esse usuário está designado. Por
exemplo:

<dl>
<dt>OrgManager</dt>
<dd>Essa função pode convidar e gerenciar usuários, selecionar e mudar planos e configurar limites de gastos. </dd>
<dt>BillingManager</dt>
<dd>Essa função pode criar e gerenciar a conta de cobrança e informações de pagamento. </dd>
<dt>OrgAuditor</dt>
<dd>Essa função possui acesso somente leitura para informações e relatórios da organização. </dd>
</dl> 

**Exemplos**:

Designe o usuário `Mary` à organização do `IBM` como função `OrgManager`: 

```
bluemix iam org-role-set Mary IBM OrgManager
```


## bluemix iam org-role-unset
{: #bluemix_iam_org_role_unset}

Remover uma função de organização de um usuário. Essa operação pode ser executada somente por um gerenciador de organização. 

```
bluemix iam org-role-unset USER_NAME ORG_NAME ORG_ROLE
```

**Pré-requisitos**: Terminal, Login

**Opções de comando**:

*USER_NAME* (requerido): O nome do usuário que está sendo removido. 

*ORG_NAME* (requerido): O nome da organização da qual esse usuário é removido. 

*ORG_ROLE* (requerido): O nome da função de organização da qual esse usuário é removido. Por
exemplo:

<dl>
<dt>OrgManager</dt>
<dd>Essa função pode convidar e gerenciar usuários, selecionar e mudar planos e configurar limites de gastos. </dd>
<dt>BillingManager</dt>
<dd>Essa função pode criar e gerenciar a conta de cobrança e informações de pagamento. </dd>
<dt>OrgAuditor</dt>
<dd>Essa função possui acesso somente leitura para informações e relatórios da organização. </dd>
</dl> 

**Exemplos**:

Remova o usuário `Mary` da organização `IBM` como função `OrgManager`: 

```
bluemix iam org-role-unset Mary IBM OrgManager
```


## bluemix iam space-users
{: #bluemix_iam_space_users}

Exiba usuários no espaço especificado por função. 

```
bluemix iam space-users ORG_NAME SPACE_NAME
```

**Pré-requisitos**: Terminal, Login

**Opções de comando**:

*ORG_NAME* (requerido): O nome da organização

*SPACE_NAME* (requerido): O nome do espaço. 


## bluemix iam space-role-set
{: #bluemix_iam_space_role_set}

Designe uma função de espaço a um usuário. Essa operação pode ser executada somente por um gerenciador de espaço. 

```
bluemix iam space-role-set USER_NAME ORG_NAME SPACE_NAME SPACE_ROLE
```

**Pré-requisitos**: Terminal, Login

**Opções de comando**:

*USER_NAME* (requerido): O nome do usuário que está sendo designado. 

*ORG_NAME* (requerido): O nome da organização à qual esse usuário está designado. 

*SPACE_NAME* (requerido): O nome do espaço ao qual esse usuário é designado. 

*SPACE_ROLE* (requerido): O nome da função de espaço à qual esse usuário é designado. Por
exemplo:

<dl>
<dt>SpaceManager</dt>
<dd>Essa função pode convidar e gerenciar usuários e ativar recursos para um determinado espaço. </dd>
<dt>SpaceDeveloper</dt>
<dd>Essa função pode criar e gerenciar apps e serviços e ver logs e relatórios. </dd>
<dt>SpaceAuditor</dt>
<dd>Essa função pode visualizar logs, relatórios e configurações para o espaço. </dd>
</dl> 


**Exemplos**:

Designe o usuário `Mary` à organização `IBM` e espaço `Cloud` como função `SpaceManager`: 

```
bluemix iam space-role-set Mary IBM Cloud SpaceManager
```

## bluemix iam space-role-unset
{: #bluemix_iam_space_role_unset}

Remova uma função de espaço de um usuário. Essa operação pode ser executada somente por um gerenciador de espaço. 

```
bluemix iam space-role-unset USER_NAME ORG_NAME SPACE_NAME SPACE_ROLE
```

**Pré-requisitos**: Terminal, Login

**Opções de comando**:

*USER_NAME* (requerido): O nome do usuário que está sendo removido. 

*ORG_NAME* (requerido): O nome da organização da qual esse usuário é removido. 

*SPACE_NAME* (requerido): O nome do espaço do qual esse usuário é removido. 

*SPACE_ROLE* (requerido): O nome da função de espaço da qual esse usuário é removido. Por
exemplo:

<dl>
<dt>SpaceManager</dt>
<dd>Essa função pode convidar e gerenciar usuários e ativar recursos para um determinado espaço. </dd>
<dt>SpaceDeveloper</dt>
<dd>Essa função pode criar e gerenciar apps e serviços e ver logs e relatórios. </dd>
<dt>SpaceAuditor</dt>
<dd>Essa função pode visualizar logs, relatórios e configurações para o espaço. </dd>
</dl> 

**Exemplos**:

Remova o usuário `Mary` da organização `IBM` e espaço `Cloud` como função `SpaceManager`: 

```
bluemix iam space-role-unset Mary IBM Cloud SpaceManager
```


## bluemix app push
{: #bluemix_app_push}

Esse comando tem a mesma função e opções que o comando `cf push`.


## bluemix app list
{: #bluemix_app_list}

Esse comando tem a mesma função e opções que o comando `cf apps`.


## bluemix app show
{: #bluemix_app_show}

Esse comando tem a mesma função e opções que o comando `cf app`.


## bluemix app scale
{: #bluemix_app_scale}

Esse comando tem a mesma função e opções que o comando `cf scale`.


## bluemix app delete
{: #bluemix_app_delete}

Esse comando tem a mesma função e opções que o comando `cf delete`.


## bluemix app rename
{: #bluemix_app_rename}

Esse comando tem a mesma função e opções que o comando `cf rename`.


## bluemix app start
{: #bluemix_app_start}

Esse comando tem a mesma função e opções que o comando `cf start`.


## bluemix app stop
{: #bluemix_app_stop}

Esse comando tem a mesma função e opções que o comando `cf stop`.


## bluemix app restart
{: #bluemix_app_restart}

Esse comando tem a mesma função e opções que o comando `cf restart`.


## bluemix app restage
{: #bluemix_app_restage}


Esse comando tem a mesma função e opções que o comando `cf restage`.


## bluemix app instance-restart
{: #bluemix_app_instance_restart}


Esse comando tem a mesma função e opções que o comando `cf restart-app-instance`.


## bluemix app events
{: #bluemix_app_events}

Esse comando tem a mesma função e opções que o comando `cf events`.


## bluemix app files
{: #bluemix_app_files}

Esse comando tem a mesma função e opções que o comando `cf files`.


## bluemix app logs
{: #bluemix_app_logs}

Esse comando tem a mesma função e opções que o comando `cf logs`.


## bluemix app env
{: #bluemix_app_env}

Esse comando tem a mesma função e opções que o comando `cf env`.


## bluemix app env-set
{: #bluemix_app_env_set}

Esse comando tem a mesma função e opções que o comando `cf set-env`.


## bluemix app env-unset
{: #bluemix_app_env_unset}

Esse comando tem a mesma função e opções que o comando `cf unset-env`.


## bluemix app stacks
{: #bluemix_app_stacks}

Esse comando tem a mesma função e opções que o comando `cf stacks`.


## bluemix app stack
{: #bluemix_app_stack}

Esse comando tem a mesma função e opções que o comando `cf stack`.


## bluemix app manifest-create
{: #bluemix_app_manifest_create}

Esse comando tem a mesma função e opções que o comando `cf create-app-manifest`.


## bluemix service offerings
{: #bluemix_service_offerings}


Esse comando tem a mesma função e opções que o comando `cf marketplace`.


## bluemix service list
{: #bluemix_service_list}

Esse comando tem a mesma função e opções que o comando `cf services`.


## bluemix service show
{: #bluemix_service_show}

Esse comando tem a mesma função e opções que o comando `cf service`.


## bluemix service create
{: #bluemix_service_create}

Esse comando tem a mesma função e opções que o comando `cf create-service`.


## bluemix service update
{: #bluemix_service_update}

Esse comando tem a mesma função e opções que o comando `cf update-service`.


## bluemix service delete
{: #bluemix_service_delete}

Esse comando tem a mesma função e opções que o comando `cf delete-service`.


## bluemix service rename
{: #bluemix_service_rename}

Esse comando tem a mesma função e opções que o comando `cf rename-service`.


## bluemix service bind
{: #bluemix_service_bind}

Esse comando tem a mesma função e opções que o comando `cf bind-service`.


## bluemix service unbind
{: #bluemix_service_unbind}

Esse comando tem a mesma função e opções que o comando `cf unbind-service`.


## bluemix service key-create
{: #bluemix_service_key_create}

Esse comando tem a mesma função e opções que o comando `cf create-service-key`.


## bluemix service key-delete
{: #bluemix_service_key_delete}

Esse comando tem a mesma função e opções que o comando `cf delete-service-key`.


## bluemix service keys
{: #bluemix_service_keys}

Esse comando tem a mesma função e opções que o comando `cf service-keys`.


## bluemix service key-show
{: #bluemix_service_key_show}

Esse comando tem a mesma função e opções que o comando `cf service-key`.


## bluemix service user-provided-create
{: #bluemix_service_user_provided_create}

Esse comando tem a mesma função e opções que o comando `cf create-user-provided-service`.


## bluemix service user-provided-update
{: #bluemix_service_user_provided_update}

Esse comando tem a mesma função e opções que o comando `cf update-user-provided-service`.


## bluemix catalog templates
{: #bluemix_catalog_templates}

Visualize os modelos de modelo no Bluemix.

```
bluemix catalog templates [-d]
```

**Pré-requisitos**: Terminal, Login

**Opções de comando**:

-d (opcional): se a opção `-d` for especificada, a descrição de cada modelo também é exibida. Caso contrário, somente o ID e o nome de cada modelo serão mostrados.


## bluemix catalog template
{: #bluemix_catalog_template}

Visualize as informações detalhadas de um modelo de modelo especificado.

```
bluemix catalog template TEMPLATE_ID
```

**Pré-requisitos**: Terminal, Login

**Opções de comando**:

*TEMPLATE_ID* (obrigatório): o ID do modelo de modelo. Use 'bluemix templates' para visualizar todos os IDs de modelos.

**Exemplos**:

Visualize detalhes do modelo `mobileBackendStarter`:

```
bluemix catalog template mobileBackendStarter
```


## bluemix catalog template-run
{: #bluemix_catalog_template_run}

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


## bluemix network regions
{: #bluemix_network_regions}

Visualize as informações para todas as regiões no {{site.data.keyword.Bluemix_notm}}.

```
bluemix network regions
```

**Pré-requisitos**: Terminal


## bluemix network region-set
{: #bluemix_network_region_set}

Alterne para a região especificada. Esse comando redestina automaticamente para a mesma organização e o mesmo espaço na nova região, se possível. Caso contrário, o comando solicita que o usuário selecione uma nova organização e um novo espaço se o usuário já tiver efetuado login. O terminal de API é mudado apropriadamente.

```
bluemix network region-set REGION_NAME
```

**Pré-requisitos**: Terminal

**Opções de comando**:

*REGION_NAME* (requerido): o nome da região para o qual você deseja alternar. É possível usar o comando `bluemix network regions` para ver todos os nomes de regiões.

**Exemplos**:

Configure a região atual como `eu-gb`:

```
bluemix network region-set eu-gb
```


## bluemix network routes
{: #bluemix_network_routes}

Esse comando tem a mesma função e opções que o comando `cf routes`.


## bluemix network route-check
{: #bluemix_network_route_check}

Esse comando tem a mesma função e opções que o comando `cf check-route`.


## bluemix network route-map
{: #bluemix_network_route_map}

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
{: #bluemix_network_route_unmap}

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
{: #bluemix_network_route_create}

Esse comando tem a mesma função e opções que o comando `cf create-route`.


## bluemix network route-delete
{: #bluemix_network_route_delete}

Esse comando tem a mesma função e opções que o comando `cf delete-route`.


## bluemix network orphaned-routes-delete
{: #bluemix_network_orphaned_routes_delete}

Esse comando tem a mesma função e opções que o comando `cf delete-orphaned-routes`.


## bluemix network domains
{: #bluemix_network_domains}

Esse comando tem a mesma função e opções que o comando `cf domains`.


## bluemix network domain-create
{: #bluemix_network_domain_create}

Esse comando tem a mesma função e opções que o comando `cf create-domain`.


## bluemix network domain-delete
{: #bluemix_network_domain_delete}

Esse comando tem a mesma função e opções que o comando `cf delete-domain`.


## bluemix network shared-domain-create
{: #bluemix_network_shared_domain_create}

Esse comando tem a mesma função e opções que o comando `cf create-shared-domain`.


## bluemix network shared-domain-delete
{: #bluemix_network_shared_domain_delete}

Esse comando tem a mesma função e opções que o comando `cf delete-shared-domain`.


## bluemix security cert
{: #bluemix_security_cert}

Liste as informações de certificado de um domínio. 

```
bluemix security cert DOMAIN_NAME
```

**Pré-requisitos**: Terminal, Login

**Opções de comando**:

*DOMAIN_NAME* (requerido): O domínio que hospeda o certificado. 

**Exemplos**:

Visualize as informações de certificado do domínio `ibmcxo-eventconnect.com`: 

```
bluemix security cert ibmcxo-eventconnect.com
```


## bluemix security cert-add
{: #bluemix_security_cert_add}

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
{: #bluemix_security_cert_remove}

Remova um certificado do domínio especificado na organização atual.

```
bluemix security cert-remove DOMAIN [-f]
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

*DOMAIN* (requerido): o domínio do qual remover o certificado.

-f (opcional): force a exclusão sem confirmação.







## bluemix plugin repos
{: #bluemix_plugin_repos}

Liste todos os repositórios de plug-in que estão registrados na CLI do {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin repos
```

**Pré-requisitos**: Nenhum


## bluemix plugin repo-add
{: #bluemix_plugin_repo_add}

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
{: #bluemix_plugin_repo_remove}

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


## bluemix plugin repo-plugins
{: #bluemix_plugin_repo_plugins}

Liste todos os plug-ins disponíveis em todos os repositórios incluídos ou um repositório específico.

```
bluemix plugin repo-plugins [-r REPO_NAME]
```

**Pré-requisitos**: Nenhum

**Opções de comando**:

-r *REPO_NAME* (opcional): Liste somente os plug-ins no repositório especificado.

**Exemplos**:

Liste todos os plug-ins em todos os repositórios incluídos:

```
bluemix plugin repo-plugins
```

Liste todos os plug-ins no repositório `bluemix-repo`:

```
bluemix plugin repo-plugins -r bluemix-repo
```


## bluemix plugin list
{: #bluemix_plugin_list}

Liste todos os plug-ins instalados na CLI do {{site.data.keyword.Bluemix_notm}}.

```
bluemix plugin list
```

**Pré-requisitos**: Nenhum


## bluemix plugin install
{: #bluemix_plugin_install}

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
{: #bluemix_plugin_uninstall}

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


## bluemix ic init
{: #bluemix_ic_init}

Inicialize o ambiente de contêineres em sua máquina local para usar os recursos integrais do serviço IBM Containers.

```
bluemix ic init
```

**Pré-requisitos**: Terminal, Login, Destino

**Nota:** antes da inicialização, assegure que a CLI do Docker (docker) esteja instalada e configurada em sua variável de ambiente PATH. Para alternar para outra região, use o comando `bluemix region-set`. 

**Exemplos**:

Alterne para a região `us-south`:

```
bluemix region-set us-south
```


## bluemix ic attach
{: #bluemix_ic_attach}

Controlar um contêiner em execução ou visualizar sua saída. Use `CTRL+C` para sair e parar o contêiner. Esse comando chama a CLI do Docker. Para obter mais informações, consulte o comando [attach](https://docs.docker.com/reference/commandline/attach/){: new_window} na ajuda do Docker. 

```
bluemix ic attach [--no-stdin][--sig-proxy] CONTAINER
```

**Pré-requisitos**: Terminal, Login, Destino, Docker

**Opções de comando**:

--no-stdin (opcional): não incluir a entrada padrão.

--sig-proxy  (opcional): efetue proxy de todos os sinais recebidos para o processo. O padrão é **true**.

*CONTAINER* (obrigatório): o nome ou o ID do contêiner.

**Exemplos**:

O exemplo a seguir mostra uma solicitação para conectar-se ao contêiner `my_container`:
```
bluemix ic attach my_container
```


## bluemix ic build
{: #bluemix_ic_build}

Chame o serviço de construção IBM Containers para construir uma imagem do Docker localmente ou em seu repositório privado do {{site.data.keyword.Bluemix_notm}}. Esse comando chama a CLI do Docker. Para obter mais informações, consulte o comando [build](https://docs.docker.com/reference/commandline/build/){: new_window} na ajuda do Docker. 

```
bluemix ic build -t TAG|--tag TAG [--no-cache][-p|--pull] [-q|--quiet] DOCKERFILE_LOCATION
```

**Pré-requisitos**: Terminal, Login, Destino, Docker

**Opções de comando**:

-t *TAG*|--tag *TAG* (obrigatório): o nome de repositório a ser aplicado à imagem criada.

--no-cache (opcional): não usar o cache quando a imagem for construída. O padrão é **false**.

-p|--pull (opcional): tentativa de realizar pull da imagem base a partir do registro mesmo se for armazenado em cache.

-q|--quiet (opcional): suprima a saída detalhada gerada pelos contêineres. O padrão é **false**.

*DOCKERFILE_LOCATION* (obrigatório): o caminho para o Dockerfile e o contexto no host local.

**Exemplos**:

O exemplo a seguir mostra uma solicitação para construir uma imagem denominada *myimage*. O Dockerfile e outros artefatos a serem usados na construção estão no mesmo diretório a partir do qual o comando está em execução. Como o registro e o namespace são incluídos com o nome da imagem, a imagem será construída no repositório privado do {{site.data.keyword.Bluemix_notm}} de sua organização.
```
bluemix ic build -t registry.ng.bluemix.net/mynamespace/myimage .
```


## bluemix ic create
{: #bluemix_ic_create}

Crie um novo contêiner em seu repositório do {{site.data.keyword.Bluemix_notm}}. Esse comando agrupa o comando `docker create`. Para obter mais informações, consulte o comando [create](https://docs.docker.com/reference/commandline/create/){: new_window} na ajuda do Docker.


## bluemix ic cpi
{: #bluemix_ic_cpi}

Acesse uma imagem do Docker Hub ou uma imagem de seu registro local e copie a imagem para seu repositório privado do {{site.data.keyword.Bluemix_notm}}.

```
bluemix ic cpi SOURCE_IMAGE DESTINATION_IMAGE
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

*SOURCE_IMAGE* (obrigatório): o repositório de origem e o nome da imagem.

*DESTINATION_IMAGE* (obrigatório): a URL do repositório privado do {{site.data.keyword.Bluemix_notm}}, que inclui o namespace e o nome da imagem de destino. Uma marcação para a imagem é opcional.

**Exemplos**:

Copie uma imagem do repositório de origem para seu repositório privado e inclua uma tag para a imagem:

```
bluemix ic cpi source_repository/source_image_name private_registry_URL/destination_image_name:tag
```

Copie a imagem `sinatra` do repositório `training` para seu repositório privado `registry.ng.bluemix.net/mynamespace` e o nome da imagem como `mysinatra`. Inclua uma tag `v1` para a imagem `mysinatra`. 

```
bluemix ic cpi training/sinatra registry.ng.bluemix.net/mynamespace/mysinatra:v1
```


## bluemix ic exec
{: #bluemix_ic_exec}


Executar um comando em um contêiner. Para obter mais informações, consulte o comando [exec](https://docs.docker.com/reference/commandline/exec/){: new_window} na ajuda do Docker.

```
bluemix ic exec [-d|--detach][-it] [-u USER|--user USER] CONTAINER [CMD]
```

**Pré-requisitos**: Terminal, Login, Destino, Docker

**Opções de comando**:

-d|--detach (opcional): executar o comando especificado em segundo plano.

-it (opcional): modo interativo. Manter a exibição da entrada padrão. Digite 'exit' para sair.

-u *USER*|--user *USER* (opcional): o nome do usuário.

*CONTAINER* (obrigatório): o nome ou o ID do contêiner.

*CMD* (opcional): o comando a ser executado no contêiner ou contêineres especificados.

**Exemplos**:

Execute o comando `bash` no contêiner `my_container` no modo interativo:

```
bluemix ic exec -it my_container bash
```

Execute o comando `date` no contêiner `my_container`:

```
bluemix ic exec my_container date
```


## bluemix ic groups
{: #bluemix_ic_groups}

Liste grupos de contêineres no repositório privado do {{site.data.keyword.Bluemix_notm}} da organização.

```
bluemix ic groups
```

**Pré-requisitos**: Terminal, Login, Destino


## bluemix ic group-inspect
{: #bluemix_ic_group_inspect}

Visualize informações detalhadas, como variáveis de ambiente, portas ou memória, especificadas para um grupo de contêiner quando criado.

```
bluemix ic group-inspect CONTAINER_GROUP
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

*CONTAINER_GROUP* (obrigatório): o ID ou o nome do grupo de contêiner.

**Exemplos**:

O exemplo a seguir mostra uma solicitação para inspecionar o grupo de contêiner `my_group`:
```
bluemix ic group-inspect my_group
```


## bluemix ic group-instances
{: #bluemix_ic_group_instances}

Liste instâncias de um grupo de contêiner especificado.

```
bluemix ic group-instances CONTAINER_GROUP
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

*CONTAINER_GROUP* (obrigatório): o ID ou o nome do grupo de contêiner.

**Exemplos**:

Liste todas as instâncias do grupo de contêiner `my_group`:
```
bluemix ic group-instances my_group
```


## bluemix ic group-create
{: #bluemix_ic_group_create}

Crie um grupo de contêiner escalável.

```
bluemix ic group-create [-p PORT|--publish port][-m MEMORY|--memory MEMORY] [-e ENV|--env ENV][-v VOLUME:CONTAINER_PATH] [--min MIN][--max MAX] [--desired DESIRED][--auto] [-n HOST|--hostname HOST][-d DOMAIN|--domain DOMAIN] [--name NAME] IMAGE [CMD]
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

-m *MEMORY*|--memory *MEMORY* (opcional): designe um limite de memória ao grupo em MB. Ao criar um grupo de contêiner a partir da CLI, o valor padrão para cada instância de contêiner é `64` MB. Ao criar um grupo de contêiner a partir do Painel do {{site.data.keyword.Bluemix_notm}}, o valor padrão para cada instância de contêiner é `256` MB. Os valores aceitos são `64`, `256`, `512`, `1024` e `2048`. Após um limite de memória ser designado, o valor não poderá ser mudado.

-e *ENV*|--env *ENV* (opcional): configure a variável de ambiente, em que **ENV** é um par 'key=value'. Liste diversas chaves separadamente. Se aspas forem incluídas, inclua-as em torno do nome da variável de ambiente e do valor. Por exemplo: '-e "key1=value1" -e "key2=value2" -e "key3=value3"'.  A tabela a seguir mostra algumas variáveis de ambiente comumente usadas que podem ser especificadas:

|  Variável do ambiente                              |     Descrição                            |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;appname&gt;*       | Faça a ligação de um serviço a um contêiner. Use a variável de ambiente `CCS_BIND_APP` para fazer a ligação de um app ao contêiner. O app é ligado ao serviço de destino e age como uma ponte que permite que o {{site.data.keyword.Bluemix_notm}} traga as informações de `VCAP_SERVICES` de seu app de ponte para a instância do contêiner em execução. Para obter mais informações sobre como criar um app de ponte, consulte [Ligando um serviço a um contêiner](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_binding_ov){: new_window}. |
| CCS_SSH_KEY=*&lt;public_ssh_key&gt;* | Inclua uma chave SSH a um contêiner ao criar o contêiner. É possível incluir a chave SSH usando a variável de ambiente ao criar o contêiner a partir do painel do {{site.data.keyword.Bluemix_notm}} ou a partir da CLI. Para obter mais informações sobre chaves SSH, consulte [Efetuando login em um contêiner](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_cli_login_ssh){: new_window}. |
| LOG_LOCATIONS=*&lt;path_to_file&gt;* | Inclua um arquivo de log a ser monitorado no contêiner. Inclua a variável de ambiente `LOG_LOCATIONS` com um caminho para o arquivo de log. |
*Tabela 1. Variáveis de ambiente comumente usadas*

-v VOLUME:CONTAINER_PATH[:ro]|--volume VOLUME:CONTAINER_PATH[:ro]  (optional):  Anexe um volume a um contêiner especificando os detalhes no formato `VolumeId:ContainerPath[:ro]`.

- *VOLUME*: o ID ou o nome do volume.
- *CONTAINER_PATH*: o caminho absoluto para o volume no contêiner.
- ro: opcional. Especificar 'ro' torna o volume somente leitura em vez do padrão leitura/gravação.

-p *PORT*|--publish *PORT*  (opcional): Expor a porta para o tráfego HTTP. Contêineres em seu grupo devem atender na porta HTTP. As solicitações HTTPS não podem ser feitas. Para os grupos de contêineres, não é possível incluir várias portas.

Ao especificar uma porta, você disponibiliza o app para o Balanceador de carga do {{site.data.keyword.Bluemix_notm}} ou para contêineres que estão tentando atingir o host no mesmo espaço do {{site.data.keyword.Bluemix_notm}}. Em seguida, o balanceador de carga ou contêineres do {{site.data.keyword.Bluemix_notm}} podem usar a porta para atingir o host e o app no mesmo espaço do {{site.data.keyword.Bluemix_notm}}. Se uma porta for especificada no Dockerfile para a imagem que você está usando, inclua essa porta.

**Dica:**

- Para a imagem do servidor Liberty certificada pela IBM ou uma versão modificada dessa imagem, insira a porta 9080.
- Para a imagem do Node.js certificada pela IBM ou uma versão modificada dessa imagem, insira a porta 8000.

--min *MIN* (opcional): o número mínimo de instâncias. O padrão é **1**. Se você configurar um número mínimo de instâncias, o valor não poderá ser mudado após a criação do grupo de contêiner.

--max *MAX* (opcional): o número máximo de instâncias. O padrão é **2**. Se você configurar um número máximo de instâncias, o valor não poderá ser mudado após a criação do grupo de contêiner.

--desired *DESIRED* (opcional): o número de instâncias requerido. O padrão é **2**.

--auto (opcional): quando o grupo de contêiner é criado e a recuperação automática é ativada, o IBM Containers verifica o funcionamento de cada instância com uma solicitação de HTTP para a porta designada.

Se nenhuma resposta for recebida de uma instância do contêiner em dois intervalos subsequentes de 90 segundos, a instância será removida e substituída por uma nova instância. Nenhuma ação será executada se o contêiner for responsivo. Esse processo é repetido continuamente. Durante uma janela de 30 minutos, se o número total de contêineres diferentes que são membros do grupo for igual ou exceder três vezes o tamanho máximo observado do grupo, a recuperação automática será desativada permanentemente para o grupo de contêiner. Para ativar a recuperação automática novamente, deve-se recriar o grupo de contêineres.

-n *HOST*|--hostname *HOST* (opcional): o nome do host, como 'mycontainerhost'. O host e o domínio se combinam para formar a URL da rota pública completa, como 'http://mycontainerhost.mybluemix.net'. Ao revisar os detalhes de um grupo de contêineres com o comando 'bluemix ic group-inspect', o host e o domínio são listados juntos como a rota.

-d *DOMAIN*|--domain *DOMAIN* (opcional): geralmente, o domínio é `.mybluemix.net`. O host e o domínio são combinados para formar a URL da rota pública completa, como `http://mycontainerhost.mybluemix.net`. Ao revisar os detalhes de um grupo de contêineres com o comando `bluemix ic group-inspect`, o host e o domínio são listados juntos como a rota.

--name *NAME* (obrigatório): designe um nome ao grupo. `-n` está descontinuado.

**Dica:** o nome do contêiner deve iniciar com uma letra. O nome pode incluir letras maiúsculas, letras minúsculas, números, pontos `.`, sublinhados `_` ou hifens `–`.

*IMAGE* (obrigatório): a imagem a ser incluída em cada instância de contêiner no grupo de contêiner. É possível listar comandos após a imagem, mas não coloque nenhuma opção após a imagem. Inclua todas as opções antes de especificar uma imagem.

Se você usar uma imagem no repositório privado do {{site.data.keyword.Bluemix_notm}} de sua organização, especifique a imagem no formato: `registry.ng.bluemix.net/NAMESPACE/IMAGE`.

Se você usar uma imagem fornecida pelo IBM Containers, não inclua o namespace de sua organização. Especifique a imagem no formato: `registry.ng.bluemix.net/IMAGE`.

*CMD* (opcional): o comando e os argumentos que são passados para o grupo de contêiner executar. Esse comando deve ser um comando de longa execução. Não use um comando de curta duração que não é executado por muito tempo, por exemplo, **/bin/date**, pois o comando de curta duração pode fazer o contêiner travar.

**Nota:**
- O comando e seus argumentos devem vir no final da linha de comandos `bluemix ic run`.
- Se os argumentos de comando incluírem o hífen `–`, como em `-c` no comando de exemplo anterior, o comando deverá ser precedido por dois hifens, `--`.



**Exemplos**:

Crie um grupo de contêiner `my_container_group` usando a imagem `registry.ng.bluemix.net/ibmnode` fornecida pelo IBM Containers e, em seguida, execute o comando de longa execução `ping localhost` nesse grupo de contêiner:

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode ping localhost
```

Crie um grupo de contêiner `my_container_group` usando a imagem `registry.ng.bluemix.net/ibmnode` fornecida pelo IBM Containers e, em seguida, execute o comando de longa execução `tail -f /dev/null` nesse grupo de contêiner:

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode -- tail -f /dev/null
```

Crie um grupo escalável `mygroup` com a recuperação automática ativada usando a imagem `registry.ng.bluemix.net/ibmliberty`. A porta é `9080`, o nome do host é `mycontainerhost`, o nome do domínio é `.mybluemix.net`.
```
bluemix ic group-create -p 9080 --auto -n mycontainerhost -d .mybluemix.net --name mygroup registry.ng.bluemix.net/ibmliberty 
```


## bluemix ic group-update
{: #bluemix_ic_group_update}

Atualize um grupo de contêiner.


```
bluemix ic group-update [--min MIN][--max MAX] [--desired DESIRED][--auto] CONTAINER_GROUP
```

**Dica:** para atualizar o nome do host ou o domínio para um grupo de contêiner, use `bluemix ic route-map [-n HOST][-d DOMAIN] CONTAINER_GROUP`.

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

--min *MIN* (opcional): o número mínimo de instâncias. O padrão é **1**. Após configurar um número mínimo de instâncias, o valor não poderá ser mudado.

--max *MAX* (opcional): o número máximo de instâncias. O padrão é **2**. Após configurar um número máximo de instâncias, o valor não poderá ser mudado.

--desired *DESIRED* (opcional): o número de instâncias requerido. O padrão é **2**.

**Dica:** somente uma das opções `--min MIN`, `--max MAX` ou `--desired DESIRED` pode ser especificada por vez.

--auto (opcional): reinicialização automática de instâncias com falha ativando a recuperação automática.

*CONTAINER_GROUP* (obrigatório): o ID ou o nome do grupo de contêiner.

**Exemplos**:

O exemplo a seguir mostra uma solicitação para atualizar o grupo de contêiner `my_group`:
```
bluemix ic group-update --max 5 my_group
```


## bluemix ic group-remove
{: #bluemix_ic_group_remove}

Remover um grupo de contêiner do repositório privado do {{site.data.keyword.Bluemix_notm}} da organização.

```
bluemix ic group-remove [-f|--force] CONTAINER_GROUP
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

-f|--force (opcional): força a remoção de um contêiner em execução ou com falha.

*CONTAINER_GROUP* (obrigatório): o ID ou o nome do grupo de contêiner.

**Exemplos**:

O exemplo a seguir mostra uma solicitação para remover um grupo de contêiner, em que `my_group` é o nome do grupo de contêiner.
```
bluemix ic group-remove my_group
```


## bluemix ic images
{: #bluemix_ic_images}

Visualize uma lista de todas as imagens disponíveis no repositório privado do {{site.data.keyword.Bluemix_notm}} da organização. Para obter mais informações, consulte o comando [images](https://docs.docker.com/reference/commandline/images){: new_window} na ajuda do Docker. A lista inclui o ID da imagem, a data de criação e o nome da imagem.

```
bluemix ic images [-a|--all][--no-trunc] [-q|--quiet]
```

**Pré-requisitos**: Terminal, Login, Destino, Docker

**Opções de comando**:

-a|--all (opcional): incluir todas as camadas de imagens para cada imagem no repositório de sua organização, não apenas a camada mais recente.

--no-trunc (opcional): não truncar a saída.

-q|--quiet (opcional): exibir apenas os IDs numéricos.

**Exemplos**:

O exemplo a seguir mostra uma solicitação para receber uma lista de imagens disponíveis para a organização:
```
bluemix ic images
```


## bluemix ic inspect
{: #bluemix_ic_inspect}

Visualize as informações sobre um contêiner. Para obter mais informações, consulte o comando [inspect](https://docs.docker.com/reference/commandline/inspect){: new_window} na ajuda do Docker.

```
bluemix ic inspect [IMAGE|images|CONTAINER]
```

**Pré-requisitos**: Terminal, Login, Destino, Docker

**Opções de comando**:

*IMAGE* (obrigatório): visualizar informações detalhadas sobre uma imagem específica especificando o nome ou o ID da imagem.

images (obrigatório): visualizar informações detalhadas sobre todas as imagens em seu repositório.

*CONTAINER* (obrigatório): visualizar informações detalhadas sobre um contêiner específico especificando o nome ou o ID do contêiner.

**Dica:** somente uma das opções *IMAGE*, images ou *CONTAINER* pode ser especificada por vez. 

**Exemplos**:

O exemplo a seguir mostra uma solicitação para inspecionar um contêiner denominado `proxy`: 
```
bluemix ic inspect proxy
```


## bluemix ic info
{: #bluemix_ic_info}

Visualize um conjunto de informações que descreva o estado da instância de serviço de nuvem do contêiner. As informações incluem o limite de contêineres, o uso de contêineres, contêineres que estão em execução, o limite de memória, o uso de memória, o limite de endereço IP flutuante, o uso de endereço IP flutuante, a URL do host CCS, a URL do host de registro e o status do modo de depuração.

```
bluemix ic info
```

**Pré-requisitos**: Terminal, Login, Destino


## bluemix ic ips
{: #bluemix_ic_ips}

Listar os endereços IP flutuantes disponíveis para o usuário com login efetuado. A lista inclui endereços IP e o ID do contêiner ao qual os endereços IP são vinculadas. Se o endereço IP não for usado, nenhum ID de contêiner será mostrado.

```
bluemix ic ips [-a|--all]
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

-a|--all (opcional): listar todos os endereços IP. Por padrão, somente os endereços IP disponíveis são retornados.

**Exemplos**:

O exemplo a seguir mostra uma solicitação para receber uma lista de todos os endereços IP para a organização, estando disponíveis para uso ou não.
```
bluemix ic ips -a
```


## bluemix ic ip-request
{: #ip_request}
Solicite um novo endereço IP flutuante.

```
bluemix ic ip-request
```

**Pré-requisitos**: Terminal, Login, Destino


## bluemix ic ip-release
{: #bluemix_ic_ip_release}

Liberar um endereço IP flutuante da instância do serviço de nuvem do contêiner.

```
bluemix ic ip-release IP_ADDRESS
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

*IP_ADDRESS* (obrigatório): o endereço IP a ser liberado.


## bluemix ic ip-bind
{: #bluemix_ic_ip_bind}

Ligar um endereço IP flutuante disponível a um contêiner.

```
bluemix ic ip-bind IP_ADDRESS CONTAINER
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

*IP_ADDRESS* (obrigatório): o endereço IP a ser ligado.

*CONTAINER* (obrigatório): o ID ou o nome do contêiner a ser ligado.

**Exemplos**:

O exemplo a seguir mostra uma solicitação para ligar o IP endereço `192.123.12.12` ao contêiner `proxy`:
```
bluemix ic ip-bind 192.123.12.12 proxy
```


## bluemix ic ip-unbind
{: #bluemix_ic_ip_unbind}

Desvincular um endereço IP flutuante de seu contêiner.

Endereços IP públicos são um recurso limitado no IBM Containers. Portanto, endereços IP públicos que são alocados para um espaço e não ligados a
um contêiner são periodicamente recuperados de usuários de avaliação grátis, aproximadamente a cada semana. Endereços IP públicos desvinculados nunca são recuperados de clientes de pagamento por uso ou de clientes de assinatura.

```
bluemix ic ip-unbind IP_ADDRESS CONTAINER
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

*IP_ADDRESS* (obrigatório): o endereço IP a ser desvinculado.

*CONTAINER* (obrigatório): o ID ou o nome do contêiner a ser desvinculado.

**Exemplos**:

O exemplo a seguir mostra uma solicitação para desvincular o IP endereço `192.123.12.12` do contêiner `proxy`:
```
bluemix ic ip-unbind 192.123.12.12 proxy
```


## bluemix ic kill
{: #bluemix_ic_kill}

Pare um processo em execução em um contêiner sem parar o contêiner. Para obter mais informações, consulte o comando [kill](https://docs.docker.com/reference/commandline/kill/){: new_window} na ajuda do Docker.

```
bluemix ic kill [-s CMD|--signal CMD] CONTAINER
```

**Pré-requisitos**: Terminal, Login, Destino, Docker

**Opções de comando**:

-s *CMD*|--signal *CMD* (opcional): enviar um comando ao processo que está em execução no contêiner.

*CONTAINER* (obrigatório): o ID ou o nome do contêiner.

**Exemplos**:

O exemplo a seguir mostra uma solicitação para encerrar o processo em um contêiner denominado `proxy`:
```
bluemix ic kill proxy
```


## bluemix ic namespace-get
{: #bluemix_ic_namespace_get}

Visualize o nome do repositório de imagem privado do {{site.data.keyword.Bluemix_notm}} para a organização à qual você efetuar login.

```
bluemix ic namespace-get
```

**Pré-requisitos**: Terminal, Login, Destino


## bluemix ic namespace-set
{: #bluemix_ic_namespace_set}

Configure o nome do repositório de imagem privado do {{site.data.keyword.Bluemix_notm}} para a organização à qual você efetuar login.

*Restrição*: não é possível usar um hyphen `-` no nome de seu namespace de repositório.

```
bluemix ic namespace-set NAME
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

*NAME* (obrigatório): uma função única para configurar o namespace do repositório de sua organização, se ele ainda não estiver configurado. Após configurar o namespace, reinicialize o IBM Containers por meio do comando `bluemix ic init` antes de continuar.


## bluemix ic pause
{: #pause}

Pausar todos os processos em um contêiner em execução. Para obter mais informações, consulte o comando [pause](https://docs.docker.com/reference/commandline/pause/){: new_window} na ajuda do Docker. Para parar um contêiner, consulte o comando [bluemix ic unpause](#unpause).

```
bluemix ic pause CONTAINER
```

**Pré-requisitos**: Terminal, Login, Destino, Docker

**Opções de comando**:

*CONTAINER* (obrigatório): o nome ou o ID do contêiner.

**Respostas**:

- Contêiner pausado com sucesso.

- O comando falhou com o serviço de nuvem do contêiner

 `{message}`
  
 Em que
`{message}` é o erro relacionado.
 
- Comando com falha - Não foi possível se conectar ao serviço de nuvem do contêiner

**Exemplos**:

O exemplo a seguir mostra uma solicitação para pausar um contêiner denominado `proxy`:
```
bluemix ic pause proxy
```


## bluemix ic unpause
{: #unpause}

Remover pausa de todos os processos em um contêiner em execução. Para obter mais informações, consulte o comando [unpause](https://docs.docker.com/reference/commandline/unpause/){: new_window} na ajuda do Docker. Para pausar um contêiner, consulte o comando [bluemix ic pause](#pause).

```
bluemix ic unpause CONTAINER
```

**Pré-requisitos**: Terminal, Login, Destino, Docker

**Opções de comando**:

*CONTAINER* (obrigatório): o nome ou o ID do contêiner.

**Respostas**:

- Contêiner removido da pausa com sucesso.

- O comando falhou com o serviço de nuvem do contêiner 

 `{message}` 
 
 Em que
`{message}` é o erro relacionado.
 
- Comando com falha - Não foi possível se conectar ao serviço de nuvem do contêiner

**Exemplos**:

O exemplo a seguir mostra uma solicitação para remover da pausa um contêiner denominado `proxy`:
```
bluemix ic unpause proxy
```


## bluemix ic port
{: #bluemix_ic_port}

Liste mapeamentos de porta ou um mapeamento específico para o contêiner. Esse comando agrupa o comando `docker port`. Para obter mais informações, consulte o comando [port](https://docs.docker.com/reference/commandline/port/){: new_window} na ajuda do Docker.


## bluemix ic ps
{: #bluemix_ic_ps}
Visualize uma lista de contêineres que estão em execução no namespace do usuário com login efetuado. Por padrão, esse comando mostra somente os contêineres que estão em execução. Para obter mais informações, consulte o comando [ps](https://docs.docker.com/reference/commandline/ps/){: new_window} na ajuda do Docker.

```
bluemix ic ps [-a|--all][-s|--size] [-l NUM|--limit NUM][-q|--quiet]
```

**Pré-requisitos**: Terminal, Login, Destino, Docker

**Opções de comando**:

-a|--all (opcional): mostrar todos os contêineres, tanto em execução quanto interrompidos.

-s|--size (opcional): listar os tamanhos dos contêineres.

-l *NUM*|--limit *NUM* (opcional): listar os contêineres criados mais recentemente, em que *NUM* é o número dos contêineres criados mais recentemente que você deseja retornar.

Por exemplo, se você tiver criado contêineres 'node1' até 'node5' sequencialmente, o comando 'bluemix ic ps --limit 2' retornará node4 e node5 porque são os últimos dois contêineres criados.

-q|--quiet (opcional): exibir somente IDs de contêineres.

**Exemplos**:

O exemplo a seguir mostra uma solicitação para ver todos os contêineres em execução e interrompidos:
```
bluemix ic ps -a
```


## bluemix ic restart
{: #bluemix_ic_restart}

Reiniciar um contêiner. Para obter mais informações, consulte o comando [restart](https://docs.docker.com/reference/commandline/restart/){: new_window} na ajuda do Docker.

```
bluemix ic restart CONTAINER [-t SECS|--time SECS]
```

**Pré-requisitos**: Terminal, Login, Destino, Docker

**Opções de comando**:

*CONTAINER* (obrigatório): o nome ou o ID do contêiner.

-t *SECS*|--time *SECS* (opcional): o número de segundos a esperar antes que o contêiner seja reiniciado.

**Respostas**:

- Contêiner reiniciado com sucesso.

- O comando falhou com o serviço de nuvem do contêiner 

 `{message}` 
 
 Em que
`{message}` é o erro relacionado.
 
- Comando com falha - Não foi possível se conectar ao serviço de nuvem do contêiner

**Exemplos**:

O exemplo a seguir mostra uma solicitação para reiniciar um contêiner denominado `proxy`:
```
bluemix ic restart proxy
```


## bluemix ic rm
{: #bluemix_ic_rm}

Remover um contêiner. Para obter mais informações, consulte o comando [rm](https://docs.docker.com/reference/commandline/rm/){: new_window} na ajuda do Docker.

```
bluemix ic rm [-f|--force] CONTAINER
```

**Pré-requisitos**: Terminal, Login, Destino, Docker

**Opções de comando**:

-f|--force (opcional): força a remoção de um contêiner em execução ou com falha.

*CONTAINER* (obrigatório): o nome ou o ID do contêiner.

**Respostas**:

- Contêiner removido com sucesso.

- O comando falhou com o serviço de nuvem do contêiner 

 `{message}` 
 
 Em que
`{message}` é o erro relacionado.
 
- Comando com falha - Não foi possível se conectar ao serviço de nuvem do contêiner.

**Exemplos**:

O exemplo a seguir mostra uma solicitação para remover um contêiner denominado `proxy`:
```
bluemix ic rm proxy
```


## bluemix ic rmi
{: #bluemix_ic_rmi}

Remover uma imagem do namespace do usuário com login efetuado. Para obter mais informações, consulte o comando [rmi](https://docs.docker.com/reference/commandline/rmi/){: new_window} na ajuda do Docker.

```
bluemix ic rmi [-R REGISTRY|--registry REGISTRY] IMAGE
```

**Pré-requisitos**: Terminal, Login, Destino, Docker

**Opções de comando**:

-R *REGISTRY*|--registry *REGISTRY* (opcional): mudar o host do registro. O padrão é usar o registro que você especifica no comando `bluemix ic init`.

*IMAGE* (necessário): o nome da imagem que você deseja remover. Se uma tag não for especificada no nome da imagem, a imagem identificada por último (`latest`) será excluída, por padrão.

**Respostas**:

- Removido: `{IMAGE}`

 Em que `{IMAGE}` é o nome da imagem que foi removida.
 
- Erro! Nenhum host de registro especificado.

- Remoção de imagem com falha - Não foi possível se conectar ao registro de nuvem do contêiner

- O comando falhou com o serviço de nuvem do contêiner 

 `{message}`
 
 Em que
`{message}` é o erro relacionado.

**Exemplos**:

O exemplo a seguir mostra uma solicitação para remover a imagem `mynamespace/myimage:latest`:
```
bluemix ic rmi registry.ng.bluemix.net/mynamespace/myimage:latest
```


## bluemix ic run
{: #bluemix_ic_run}

Iniciar um novo contêiner no serviço de nuvem de contêiner a partir de um nome de imagem. Para obter mais informações, consulte o comando [run](https://docs.docker.com/reference/commandline/run/){: new_window} na ajuda do Docker.



```
bluemix ic run [-p PORT|--publish PORT][-P] [-m MEMORY|--memory MEMORY][-e ENV|--env ENV] [-v VOLUME:CONTAINER_PATH] -n NAME|--name NAME [--link NAME:ALIAS][-it] IMAGE [CMD [CMD ...]]
```
**Nota:** assegure que a ferramenta de comando do Cloud Foundry esteja instalada e que você tenha um token do Cloud Foundry. Login bem-sucedido usando 'bluemix login' e 'bluemix ic init' gera o token e os certificados necessários. 


**Pré-requisitos**: Terminal, Login, Destino, Docker

**Opções de comando**:

-p *PORT*|--publish *PORT*  (opcional): Expor a porta para o tráfego HTTP. Inclua quaisquer portas especificadas no Dockerfile para a imagem que você está usando. É possível incluir várias portas com várias opções `-p`. Expor uma porta irá automaticamente ligar um endereço IP público ao contêiner se um endereço IP público estiver disponível.

Se você tiver um endereço IP existente no espaço que deseja ligar ao contêiner, será possível especificar o endereço IP em vez de ligá-lo posteriormente. O endereço IP deve ser especificado no formato: *&lt;ip-address&gt;:&lt;container-port&gt;:&lt;container-port&gt;*

Para obter mais informações sobre como solicitar endereços IP para um espaço, consulte o comando [bluemix ic ip-request](#ip_request).

Ao especificar uma porta, você está tornando o app disponível para o {{site.data.keyword.Bluemix_notm}} Load Balancer ou para os contêineres no mesmo espaço do {{site.data.keyword.Bluemix_notm}} que estão tentando atingir o host. Se uma porta for especificada no Dockerfile para a imagem que você está usando, inclua essa porta.

**Dica:**

- Para a imagem do servidor Liberty certificada pela IBM ou uma versão modificada dessa imagem, insira a porta 9080.
- Para a imagem do Node.js certificada pela IBM ou uma versão modificada dessa imagem, insira a porta 8000.

-P  (opcional):  Expor automaticamente as portas especificadas no Dockerfile da imagem para o tráfego HTTP.

-m *MEMORY*|--memory *MEMORY*  (opcional): Designar um limite de memória ao grupo em MB. Ao criar um grupo de contêiner a partir da CLI, o valor padrão para cada instância de contêiner é `64` MB.  Ao criar um grupo de contêiner a partir do Painel do {{site.data.keyword.Bluemix_notm}}, o valor padrão para cada instância é `256` MB. Os valores aceitos são `64`, `256`, `512`, `1024` e `2048`. Após um limite de memória ser designado, o valor não poderá ser mudado.

-e *ENV*|--env *ENV*  (opcional): Configure a variável de ambiente, em que **ENV** é um par 'key=value'. Liste diversas chaves separadamente. Se aspas forem incluídas, inclua-as em torno do nome da variável de ambiente e do valor. Por exemplo: '-e "key1=value1" -e "key2=value2" -e "key3=value3"'. A tabela a seguir mostra algumas variáveis de ambiente comumente usadas que podem ser especificadas:

|      Variável do ambiente                          |   Descrição                              |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;appname&gt;*       | Faça a ligação de um serviço a um contêiner. Use a variável de ambiente `CCS_BIND_APP` para fazer a ligação de um app ao contêiner. O app é ligado ao serviço de destino e age como uma ponte que permite que o {{site.data.keyword.Bluemix_notm}} traga as informações de `VCAP_SERVICES` de seu app de ponte para a instância do contêiner em execução. Para obter mais informações sobre como criar um app de ponte, consulte [Ligando um serviço a um contêiner](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_binding_ov){: new_window}. |
| CCS_SSH_KEY=*&lt;public_ssh_key&gt;* | Inclua uma chave SSH a um contêiner ao criar o contêiner. É possível incluir a chave SSH usando a variável de ambiente ao criar um contêiner a partir do painel do {{site.data.keyword.Bluemix_notm}} ou a partir da CLI. Para obter mais informações sobre chaves SSH, consulte [Efetuando login em um contêiner](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_cli_login_ssh){: new_window}. |
| LOG_LOCATIONS=*&lt;path_to_file&gt;* | Inclua um arquivo de log a ser monitorado no contêiner. Inclua a variável de ambiente `LOG_LOCATIONS` com um caminho para o arquivo de log. |
*Tabela 2. Variáveis de ambiente comumente usadas*

-v VOLUME:CONTAINER_PATH[:ro]|--volume VOLUME:CONTAINER_PATH[:ro]  (optional):  Anexe um volume a um contêiner especificando os detalhes no formato a seguir 'VolumeId:ContainerPath[:ro]'.

- *VOLUME*: o ID ou o nome do volume.
- *CONTAINER_PATH*: o caminho absoluto para o volume no contêiner.
- ro: opcional. Especificar 'ro' torna o volume somente leitura em vez do padrão leitura/gravação.

-n *NAME*|--name *NAME* (obrigatório): designar um nome para o contêiner.

*Dica:* o nome do contêiner deve iniciar com uma letra. O nome pode incluir letras maiúsculas, letras minúsculas, números, pontos `.`, sublinhados `_` ou hifens `–`.

--link *NAME*:*ALIAS* (opcional): sempre que desejar que um contêiner se comunique com outro contêiner que está em execução, será possível abordá-lo usando um alias para o nome do host.

-it (opcional): executar o contêiner em um modo interativo. Após a criação do contêiner, manter a exibição da entrada padrão. Digite `exit` para sair.

*IMAGE* (requerido): a imagem a ser incluída no contêiner. É possível listar comandos após a imagem, mas não coloque nenhuma opção após a imagem. Inclua todas as opções antes de especificar uma imagem.

Se estiver usando uma imagem no repositório privado do {{site.data.keyword.Bluemix_notm}} de sua organização, especifique a imagem no formato: *registry.ng.bluemix.net/NAMESPACE/IMAGE*.

Se estiver usando uma imagem fornecida pelo IBM Containers, especifique a imagem no formato: *registry.ng.bluemix.net/IMAGE*.

*CMD* (opcional): o comando e os argumentos que são passados para o contêiner executar. Esse comando deve ser um comando de longa execução. Não use um comando de curta duração que não é executado por muito tempo, como `/bin/date`, porque o comando de curta duração pode fazer o contêiner travar.



**Exemplos**:

Execute o comando de longa execução `sh -c "while true; do date; sleep 20; done"` no contêiner `my_container` construído na imagem `registry.ng.bluemix.net/ibmnode`. 
```
bluemix ic run --name my_container registry.ng.bluemix.net/ibmnode -- sh -c "while true; do date; sleep 20; done"
```


Crie e, em seguida, inicie um contêiner `proxy` com um limite de memória de `1024` MB usando a imagem `my_namespace/nginx`, em que `my_namespace` é o namespace associado aos usuários que efetuaram login.
```
bluemix ic run -n proxy -m 1024 registry.ng.bluemix.net/my_namespace/nginx
```

Crie e, em seguida, inicie um contêiner usando a imagem `my_namespace/blog`, passe as credenciais como variáveis ambientais. `my_namespace` é o namespace associado aos usuários que efetuaram login.
```
bluemix ic run -n my_container -e USER=johnsmith -e PASS=password registry.ng.bluemix.net/my_namespace/blog
```

Inclua um volume em um contêiner usando a imagem `my_namespace/blog`, em que `my_namespace` é o namespace associado aos usuários que efetuaram login.
```
bluemix ic run -n my_container -v VolId1:/first/path -v VolId2:/second/path registry.ng.bluemix.net/my_namespace/blog
```


## bluemix ic route-map
{: #bluemix_ic_route_map}

Estabelecer a rota para o tráfego de Internet a ser usada para acessar o grupo de contêiner. Você pode usar esse comando para estabelecer uma nova rota ou atualizar uma rota existente.

```
bluemix ic route-map [-n HOST|--hostname HOST][-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

-n *HOST*|--hostname *HOST* (opcional): o nome do host para a rota. O nome do host é a primeira parte da URL da rota pública completa, como `mycontainerhost` na URL `mycontainerhost.mybluemix.net`.

-d *DOMAIN*|--domain *DOMAIN* (opcional): o nome do domínio para a rota, que é a segunda parte da URL da rota pública completa. Na maioria dos casos, o domínio é 'mybluemix.net'. Também é possível usar esse parâmetro para especificar um domínio privado.

*CONTAINER_GROUP* (obrigatório): o ID ou o nome do grupo de contêiner.

**Exemplos**:

O exemplo a seguir mostra uma solicitação para mapear a rota para o grupo chamado 'GROUP1', em que 'my_host' é o nome do host, 'organization.com' é o domínio.
```
bluemix ic route-map -n my_host -d organization.com GROUP1
```


## bluemix ic route-unmap
{: #bluemix_ic_route_unmap}

Estabelecer a rota para o tráfego de Internet a ser usada para acessar o grupo de contêiner. Você pode usar esse comando para estabelecer uma nova rota ou atualizar uma rota existente.

```
bluemix ic route-unmap [-n HOST|--hostname HOST][-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

-n *HOST*|--hostname *HOST* (opcional): o nome do host para a rota.

-d *DOMAIN*|--domain *DOMAIN* (opcional): o nome de domínio para a rota.

*CONTAINER_GROUP* (obrigatório): o ID ou o nome do grupo de contêiner.

**Exemplos**:

O exemplo a seguir mostra uma solicitação para remover mapeamento da rota para o grupo chamado 'GROUP1', em que 'my_host' é o nome do host e 'organization.com' é o domínio.
```
bluemix ic route-unmap -n my_host -d organization.com GROUP1
```


## bluemix ic start
{: #ic_start}
Iniciar um contêiner interrompido. Para obter mais informações, consulte o comando [start](https://docs.docker.com/reference/commandline/start/){: new_window} na ajuda do Docker. Para parar um contêiner, consulte o comando [bluemix ic stop](#ic_stop).

```
bluemix ic start CONTAINER
```

**Pré-requisitos**: Terminal, Login, Destino, Docker

**Opções de comando**:

*CONTAINER* (obrigatório): o nome ou o ID do contêiner.

**Respostas**:

- Contêiner iniciado com sucesso.

- O comando falhou com o serviço de nuvem do contêiner

 `{message}`
  
 Em que
`{message}` é o erro relacionado.
 
- Comando com falha - Não foi possível se conectar ao serviço de nuvem do contêiner

**Exemplos**:

O exemplo a seguir mostra uma solicitação para iniciar um contêiner denominado `proxy`.
```
bluemix ic start proxy
```


## bluemix ic stop  
{: #ic_stop}
Parar um contêiner em execução. Para obter mais informações, consulte o comando [stop](https://docs.docker.com/reference/commandline/stop/){: new_window} na ajuda do Docker. Para iniciar um contêiner, consulte o comando [bluemix ic start](#ic_start).

```
bluemix ic stop CONTAINER [-t SECS|--time SECS]
```

**Pré-requisitos**: Terminal, Login, Destino, Docker

**Opções de comando**:

*CONTAINER* (obrigatório): o nome ou o ID do contêiner.

-t *SECS*|--time *SECS* (opcional): o número de segundos a esperar antes que o contêiner seja encerrado.

**Respostas**:

- Contêiner interrompido com sucesso.

- O comando falhou com o serviço de nuvem do contêiner

 `{message}`
  
 Em que
`{message}` é o erro relacionado.
 
- Comando com falha - Não foi possível se conectar ao serviço de nuvem do contêiner

**Exemplos**:

O exemplo a seguir mostra uma solicitação para parar um contêiner denominado `proxy`.
```
bluemix ic stop proxy
```


## bluemix ic stats
{: #bluemix_ic_stats}

Para um ou mais contêineres, visualizar estatísticas de uso em tempo real. Use `CTRL+C` para sair. Para obter mais informações, consulte o comando [stats](https://docs.docker.com/reference/commandline/stats/){: new_window} na ajuda do Docker.

```
bluemix ic stats [--no-stream] CONTAINER [CONTAINER]
```

**Pré-requisitos**: Terminal, Login, Destino, Docker

**Opções de comando**:

*CONTAINER* (obrigatório): o nome ou o ID do contêiner.

--no-stream (opcional): exibir apenas o resultado mais recente e não inclua nenhuma informação que a preceda.

**Exemplos**:

O exemplo a seguir mostra uma solicitação para as estatísticas mais recentes sobre um contêiner:
```
bluemix ic stats --no-stream my_container
```


## bluemix ic top
{: #bluemix_ic_top}

Mostrar os processos que estão em execução no contêiner. Para obter mais informações, consulte o comando [top](https://docs.docker.com/reference/commandline/top/){: new_window} na ajuda do Docker.

```
bluemix ic top CONTAINER [CONTAINER]
```

**Pré-requisitos**: Terminal, Login, Destino, Docker

**Opções de comando**:

*CONTAINER* (obrigatório): o nome ou o ID do contêiner.

**Exemplos**:

O exemplo a seguir mostra uma solicitação para exibir os processos em um contêiner chamado `my_container`.
```
bluemix ic top my_container
```


## bluemix ic volumes
{: #bluemix_ic_volumes}

Liste os volumes.

```
bluemix ic volumes
```

**Pré-requisitos**: Terminal, Login, Destino


## bluemix ic volume-inspect
{: #bluemix_ic_volume_inspect}

Inspecione um volume.

```
bluemix ic volume-inspect VOLUME_NAME
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

*VOLUME_NAME* (obrigatório): o nome do volume.

**Exemplos**:

O exemplo a seguir é uma solicitação para inspecionar um volume, em que `volume_name` é o nome do volume.
```
bluemix ic volume-inspect volume_name
```


## bluemix ic volume-create
{: #bluemix_ic_volume_create}

Crie um volume.

```
bluemix ic volume-create VOLUME_NAME
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

*VOLUME_NAME* (obrigatório): o nome do volume. O nome pode conter letras minúsculas, números, sublinhados `_` e hifens `–`.

**Exemplos**:

O exemplo a seguir mostra uma solicitação para criar um volume.
```
bluemix ic volume-create volume_name 
```


## bluemix ic volume-remove
{: #bluemix_ic_volume_remove}

Remova um volume.

```
bluemix ic volume-remove VOLUME_NAME
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

*VOLUME_NAME* (obrigatório): o nome do volume.

**Exemplos**:

O exemplo a seguir mostra uma solicitação para remover um volume, em que `volume_name` é o nome do volume.
```
bluemix ic volume-remove volume_name
```

## bluemix ic volume-fs
{: #bluemix_ic_volume_fs}

Liste os sistemas de arquivos.

```
bluemix ic volume-fs
```

## bluemix ic volume-fs-create
{: #bluemix_ic_volume_fs_create}

Crie um novo sistema de arquivos. 

```
bluemix ic volume-fs-create FILE_SYSTEM_NAME
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

*FILE_SYSTEM_NAME* (requerido): O nome do sistema de arquivos. O nome pode conter letras minúsculas, números, sublinhados `_` e hifens `–`.

**Exemplos**:

O exemplo a seguir mostra uma solicitação para criar um sistema de arquivos.
```
bluemix ic volume-fs-create my_file_system 
```

## bluemix ic volume-fs-remove
{: #bluemix_ic_volume_fs_remove}

Remover um sistema de arquivos.

```
bluemix ic volume-fs-remove FILE_SYSTEM_NAME
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

*FILE_SYSTEM_NAME* (requerido): O nome do sistema de arquivos. 

**Exemplos**:

O exemplo a seguir mostra uma solicitação para remover um sistema de arquivos, em que `my_file_system` é o nome do sistema de arquivos.
```
bluemix ic volume-fs-remove my_file_system
```

## bluemix ic volume-fs-inspect
{: #bluemix_ic_volume_fs_inspect}

Inspecione um sistema de arquivos. 

```
bluemix ic volume-fs-inspect FILE_SYSTEM_NAME
```

**Pré-requisitos**: Terminal, Login, Destino

**Opções de comando**:

*FILE_SYSTEM_NAME* (requerido): O nome do sistema de arquivos. 

**Exemplos**:

O exemplo a seguir é uma solicitação para inspecionar um sistema de arquivos, em que `my_file_system` é o nome do volume.
```
bluemix ic volume-fs-inspect my_file_system
```
## bluemix ic volume-fs-flavors
{: #bluemix_ic_volume_fs_flavors}

Liste todos os tipos de sistema de arquivos. 

```
bluemix ic volume-fs-flavors
```

**Pré-requisitos**: Terminal, Login, Destino

## bluemix ic wait
{: #bluemix_ic_wait}

Sair de um contêiner e exibir o código de saída como confirmação. Para obter mais informações, consulte o comando [wait](https://docs.docker.com/reference/commandline/wait/){: new_window} na ajuda do Docker.

```
bluemix ic wait CONTAINER [CONTAINER]
```

**Pré-requisitos**: Terminal, Login, Destino, Docker

**Opções de comando**:

*CONTAINER* (obrigatório): o nome ou o ID do contêiner.

**Exemplos**:

O exemplo a seguir mostra uma solicitação para sair de um contêiner denominado `my_container`:
```
bluemix ic wait my_container
```


## bluemix ic version
{: #bluemix_ic_version}

Mostre a versão do Docker. 

```
bluemix ic version
```

**Pré-requisitos**: Docker

Para ver a versão do IBM Containers, execute `bluemix ic info`. Para obter mais informações, consulte o comando [version](https://docs.docker.com/reference/commandline/version/){: new_window} na ajuda do Docker.
