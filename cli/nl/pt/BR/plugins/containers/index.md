---



copyright:

  years: 2015, 2017

lastupdated: "2017-01-12"


---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# IBM Containers CLI
{: #containercli}

*Versão:* 1.0.0

A CLI do IBM Containers é um plug-in da CLI do {{site.data.keyword.Bluemix_notm}} para gerenciar contêineres e grupos de contêineres no Bluemix.
{: shortdesc}

**Nota:** *Pré-requisitos* listam quais ações são necessárias antes de usar o comando. Os comandos que não têm ações de pré-requisito listam **Nenhum**. Caso contrário, os pré-requisitos podem incluir uma ou mais das ações a seguir:
<dl>
<dt>Nó de Extremidade</dt>
<dd>Um terminal de API deve ser configurado por meio de <code>bluemix api</code> antes de usar o comando.</dd>
<dt>Login</dt>
<dd>É necessário efetuar login usando o comando <code>bluemix login</code> antes de usar esse comando. Se
estiver efetuando login com o ID federado, use a opção '--sso' para
autenticar com a senha descartável.</dd>
<dt>Destino</dt>
<dd>O comando <code>bluemix target</code> deve ser usado para configurar uma organização e um espaço antes de usar esse comando.</dd>
<dt>Docker</dt>
<dd>A CLI do Docker (docker) é necessária para executar comandos no plug-in da CLI do IBM Containers.</dd>
</dl>

<table summary="comandos do Bluemix que podem ser usados para gerenciar contêineres no Bluemix.">
<caption>Tabela 1. Comandos para gerenciar contêineres no Bluemix</caption>
 <thead>
 <th colspan="5">Comandos para gerenciar contêineres no Bluemix</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix ic attach](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_attach)</td>
 <td>[bluemix ic build](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_build)</td>
 <td>[bluemix ic cp](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_cp)</td>
 <td>[bluemix ic cpi](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_cpi)</td>
 <td>[bluemix ic exec](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_exec)</td>
 </tr>
 <tr>
 <td>[bluemix ic group-create](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_create)</td>
 <td>[bluemix ic group-inspect](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_inspect)</td>
 <td>[bluemix ic group-instances](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_instances)</td>
 <td>[bluemix ic group-remove](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_remove)</td>
 <td>[bluemix ic group-update](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_update)</td>
 </tr>
 <tr>
  <td>[bluemix ic groups](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_groups)</td>
  <td>[bluemix ic info](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_info)</td>
  <td>[bluemix ic init](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_init)</td>
  <td>[bluemix ic images](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_images)</td>
  <td>[bluemix ic inspect](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_inspect)</td>
 </tr>
 <tr>
 <td>[bluemix ic ip-bind](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ip_bind)</td>
 <td>[bluemix ic ip-release](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ip_release)</td>
 <td>[bluemix ic ip-request](/docs/cli/reference/bluemix_cli/index.html#ip_request)</td>
 <td>[bluemix ic ip-unbind](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ip_unbind)</td>
 <td>[bluemix ic ips](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ips)</td>
 </tr>
 <tr>
 <td>[bluemix ic kill](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_kill)</td>
 <td>[bluemix ic logs](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_logs)</td>
 <td>[bluemix ic namespace-get](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_namespace_get)</td>
 <td>[bluemix ic namespace-set](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_namespace_set)</td>
 <td>[bluemix ic pause](/docs/cli/reference/bluemix_cli/index.html#pause)</td>
 </tr>
 <tr>
 <td>[bluemix ic port](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_port)</td>
 <td>[bluemix ic ps](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ps)</td>
 <td>[bluemix ic rename](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_rename)</td>
 <td>[bluemix ic reprovision](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_reprovision)</td>
 <td>[bluemix ic restart](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_restart)</td>
 </tr>
 <tr>
 <td>[bluemix ic rm](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_rm)</td>
 <td>[bluemix ic rmi](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_rmi)</td>
 <td>[bluemix ic route-map](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_route_map)</td>
 <td>[bluemix ic route-unmap](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_route_unmap)</td>
 <td>[bluemix ic run](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_run)</td>
 </tr>
 <tr>
 <td>[bluemix ic service-bind](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_service_bind)</td>
 <td>[bluemix ic service-unbind](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_service_unbind)</td>
 <td>[bluemix ic start](/docs/cli/reference/bluemix_cli/index.html#ic_start)</td>
 <td>[bluemix ic stats](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_stats)</td>
 <td>[bluemix ic stop](/docs/cli/reference/bluemix_cli/index.html#ic_stop)</td>
 </tr>
 <tr>
 <td>[bluemix ic top](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_top)</td>
 <td>[bluemix ic unpause](/docs/cli/reference/bluemix_cli/index.html#unpause)</td>
 <td>[bluemix ic unprovision](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_unprovision)</td>
 <td>[bluemix ic volume-inspect](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_inspect)</td>
 <td>[bluemix ic volume-create](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_create)</td>
 </tr>
 <tr>
 <td>[bluemix ic volume-fs](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs)</td>
 <td>[bluemix ic volume-fs-create](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs_create)</td>
 <td>[bluemix ic volume-fs-remove](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs_remove)</td>
 <td>[bluemix ic volume-fs-inspect](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs_inspect)</td>
 <td>[bluemix ic volume-fs-flavors](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs_flavors)</td>
 </tr>
 <tr>
 <td>[bluemix ic volume-remove](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_remove)</td>
 <td>[bluemix ic volumes](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volumes)</td>
 <td>[bluemix ic wait](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_wait)</td>
 <td>[bluemix ic wait-status](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_wait_status)</td>
 <td>[bluemix ic version](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_version)</td>
 </tr>
  </tbody>
 </table>


## bluemix ic attach
{: #bluemix_ic_attach}

Controlar um contêiner em execução ou visualizar sua saída. Use `CTRL+C` para sair e parar o contêiner. Esse comando chama a CLI do Docker. Para obter mais informações, veja o comando [attach ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/attach/){: new_window} na ajuda do Docker.

```
bluemix ic attach [--no-stdin] [--sig-proxy] CONTAINER
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:

   <dl>
   <dt>--no-stdin (opcional)</dt>
   <dd>Não inclua a entrada padrão.</dd>
   <dt>--sig-proxy (opcional)</dt>
   <dd>Efetue proxy de todos os sinais recebidos para o processo. O valor padrão é
<i>true</i>.</dd>
   <dt><i>CONTAINER</i> (obrigatório)</dt>
   <dd>O nome ou ID do contêiner.</dd>
    </dl>

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para conectar-se ao contêiner `my_container`:
```
bluemix ic attach my_container
```



## bluemix ic build
{: #bluemix_ic_build}

Chame o serviço de construção IBM Containers para construir uma imagem do Docker localmente ou em seu repositório privado do {{site.data.keyword.Bluemix_notm}}. Esse comando chama a CLI do Docker. Para obter mais informações, veja o comando [build ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/build/){: new_window} na ajuda do Docker.

```
bluemix ic build -t TAG|--tag TAG [--no-cache] [-p|--pull] [-q|--quiet] DOCKERFILE_LOCATION
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:
   <dl>
   <dt>-t <i>TAG</i>|--tag <i>TAG</i> (necessário)</dt>
   <dd>O nome de repositório a ser aplicado na imagem que é criada.</dd>
   <dt>--no-cache (opcional)</dt>
   <dd>Não use o cache quando a imagem é construída. O padrão é <i>false</i>.</dd>
   <dt>--pull (opcional)</dt>
   <dd>Tentativa de realizar pull da imagem base a partir do registro mesmo se for armazenada em cache.</dd>
   <dt>-q|--quiet (opcional)</dt>
   <dd>Suprima a saída detalhada que é gerada pelos contêineres. O padrão é <i>false</i>.</dd>
   <dt><i>DOCKERFILE_LOCATION</i> (obrigatório)</dt>
   <dd>O caminho para o Dockerfile e o contexto no host local.</dd>
    </dl>

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para construir uma imagem denominada *myimage*. O Dockerfile e outros artefatos a serem usados na construção estão no mesmo diretório a partir do qual o comando está em execução. Como o registro e o namespace são incluídos com o nome da imagem, a imagem será construída no repositório privado do {{site.data.keyword.Bluemix_notm}} de sua organização.
```
bluemix ic build -t registry.ng.bluemix.net/mynamespace/myimage .
```


## bluemix ic cp
{: #bluemix_ic_cp}
Copie arquivos ou pastas entre um contêiner e o sistema de arquivos local. Esse comando chama a CLI do Docker. Para obter mais informações, veja o comando [cp ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/cp/){: new_window} na ajuda do Docker.


## bluemix ic cpi
{: #bluemix_ic_cpi}

Acesse uma imagem do Docker Hub ou uma imagem de seu registro local e copie a imagem para seu repositório privado do {{site.data.keyword.Bluemix_notm}}.

```
bluemix ic cpi SOURCE_IMAGE DESTINATION_IMAGE
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:
   <dl>
   <dt><i>SOURCE_IMAGE</i> (obrigatório)</dt>
   <dd>O repositório de origem e o nome da imagem.</dd>
   <dt><i>DESTINATION_IMAGE</i> (obrigatório)</dt>
   <dd>A URL de repositório privado do {{site.data.keyword.Bluemix_notm}}, que inclui o namespace e o nome da imagem de destino. Uma marcação para a imagem é opcional.</dd>
   </dl>

<strong>Exemplos</strong>:

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

Executar um comando em um contêiner. Para obter mais informações, veja o comando [exec ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/exec/){: new_window} na ajuda do Docker.

```
bluemix ic exec [-d|--detach] [-it] [-u USER|--user USER] CONTAINER [CMD]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:

   <dl>
   <dt>-d|--detach (opcional)</dt>
   <dd>Execute o comando especificado no segundo plano.</dd>
   <dt>-it (opcional)</dt>
   <dd>Modo interativo. Manter a exibição da entrada padrão. Digite <i>exit</i> para sair.</dd>
   <dt>-u <i>USER</i>|--user <i>USER</i> (opcional)</dt>
   <dd>O nome do usuário.</dd>
   <dt><i>CONTAINER</i> (obrigatório)</dt>
   <dd>O nome ou ID do contêiner.</dd>
   <dt><i>CMD</i> (opcional)</dt>
   <dd>O comando a ser executado no contêiner ou nos contêineres especificados.</dd>
   </dl>

<strong>Exemplos</strong>:

Execute o comando `bash` no contêiner `my_container` no modo interativo:

```
bluemix ic exec -it my_container bash
```

Execute o comando `date` no contêiner `my_container`:

```
bluemix ic exec my_container date
```


## bluemix ic group-create
{: #bluemix_ic_group_create}

Crie um grupo de contêiner escalável.

```
bluemix ic group-create [--publish,-p PORT] --name GROUP_NAME [--memory,-m MEMORY_SIZE] [-n,--hostname HOSTNAME] [-d,--domain DOMAIN] [--env,-e ENV_KEY=ENV_VAL] [--env-file ENVIRO

NMENT_VARIABLE_FILE] [-P false|true] [--volume] [--min MIN_INSTANCE_COUNT] [--max MAX_INSTANCE_COUNT] [--desired DESIRED_INSTANCE_COUNT] [--anti false|true] [--auto false|true] IMAGE_NAME [CMD [CMD ...]]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:
   <dl>
    <dt><i>IMAGE_NAME</i> (obrigatório)</dt>
   <dd>A imagem a ser incluída em cada instância de contêiner no grupo de contêiner. É possível listar comandos após a imagem, mas não coloque nenhuma opção após a imagem. Inclua todas as opções antes de especificar uma imagem. <br><br>Se você usar uma imagem no repositório privado do {{site.data.keyword.Bluemix_notm}} de sua organização, especifique a imagem no formato: <i>registry.ng.bluemix.net/NAMESPACE/IMAGE</i>. <br><br>Se você usar uma imagem fornecida pelo IBM Containers, não inclua o namespace de sua organização. Especifique a imagem no formato: <i>registry.ng.bluemix.net/IMAGE</i>. </dd>
   <dt>--name <i>GROUP_NAME</i> (obrigatório)</dt>
   <dd>Designe um nome ao grupo. <i>-n</i> está descontinuado.<br>
   <strong>Dica:</strong> o nome do contêiner deve iniciar com uma letra. O nome pode incluir letras maiúsculas, letras minúsculas, números, pontos., sublinhados _ ou hifens -.</dd>
   <dt>-m <i>MEMORY_SIZE</i>|--memory <i>MEMORY_SIZE</i> (opcional)</dt>
   <dd>Designe um limite de memória ao grupo em MB. Ao criar um grupo de contêiner a partir da CLI, o valor padrão para cada instância de contêiner é <i>64</i> MB. Ao criar um grupo de contêiner a partir do Painel do {{site.data.keyword.Bluemix_notm}}, o valor padrão para cada instância de contêiner é <i>256</i> MB. Os valores aceitos são <i>64</i>, <i>256</i>, <i>512</i>, <i>1024</i> e <i>2048</i>. Após um limite de memória ser designado, o valor não poderá ser mudado.</dd>
   <dt>-n <i>HOSTNAME</i>|--hostname <i>HOSTNAME</i> (opcional)</dt>
   <dd>O nome do host, como <i>mycontainerhost</i>. O host e o domínio são combinados para formar a URL da rota pública completa, como <i>http://mycontainerhost.mybluemix.net</i>. Ao revisar os detalhes de um grupo de contêineres com o comando <i>bluemix ic group-inspect</i>, o host e o domínio são listados juntos como a rota.</dd>
   <dt>-d <i>DOMAIN</i>|--domain <i>DOMAIN</i> (opcional)</dt>
   <dd>Geralmente, o domínio é <i>.mybluemix.net</i>. O host e o domínio são combinados para formar a URL da rota pública completa, como <i>http://mycontainerhost.mybluemix.net</i>. Ao revisar os detalhes de um grupo de contêineres com o comando <i>bluemix ic group-inspect</i>, o host e o domínio são listados juntos como a rota.</dd>
   <dt>-e <i>ENV_KEY=ENV_VAL</i>|--env <i>ENV_KEY=ENV_VAL</i> (opcional)</dt>
   <dd>Configure a variável de ambiente. Liste diversas chaves separadamente. Se aspas forem incluídas, inclua-as em torno do nome da variável de ambiente e do valor. Por
exemplo: `-e "key1=value1" -e "key2=value2" -e "key3=value3"`.  A tabela a seguir mostra algumas variáveis de ambiente comumente usadas que podem ser especificadas:</dd>
    </dl>


|  Variável do ambiente                              |     Descrição                            |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;appname&gt;*       | Faça a ligação de um serviço a um contêiner. Use a variável de ambiente `CCS_BIND_APP` para ligar um aplicativo ao contêiner. O app é ligado ao serviço de destino e age como uma ponte que permite que o {{site.data.keyword.Bluemix_notm}} traga as informações de `VCAP_SERVICES` de seu app de ponte para a instância do contêiner em execução. Para obter mais informações sobre como criar um app de ponte, consulte [Ligando um serviço a um contêiner](../../../containers/container_integrations_binding.html){: new_window}. |
| CCS_BIND_SRV=*&lt;service_instance_name1&gt;*,*&lt;service_instance_name2&gt;* | Para ligar um serviço Bluemix diretamente a um contêiner, sem usar um app de ponte, use CCS_BIND_SRV. Essa ligação permite que o Bluemix injete as informações de VCAP_SERVICES na instância do contêiner em execução. Para listar vários serviços do Bluemix, inclua-os como parte da mesma variável de ambiente. |
| LOG_LOCATIONS=*&lt;path_to_file&gt;* | Inclua um arquivo de log a ser monitorado no contêiner. Inclua a variável de ambiente `LOG_LOCATIONS` com um caminho para o arquivo de log. |
{: caption="Table 2. Commonly used environment variables" caption-side="top"}

 <dl>
   <dt>--env-file <i>ENVIRONMENT_VARIABLE_FILE</i> (opcional)</dt>
   <dd> Importe variáveis de ambiente de um arquivo em que ENVFILE é o caminho para seu
arquivo no diretório local. Cada linha do arquivo representa um par key=value. </dd>
   <dt>--volume <i>VOLUME</i>:<i>CONTAINER_PATH</i>[:ro] (opcional)</dt>
   <dd>Anexe um volume a um contêiner especificando os detalhes no formato <i>VolumeId:ContainerPath[:ro]</i>.
   <ul>
   <li><i>VOLUME</i>: O ID ou o nome do volume.</li>
   <li><i>CONTAINER_PATH</i>: O caminho absoluto para o volume no contêiner.</li>
   <li>ro: opcional. Especificar <i>ro</i> torna o volume somente leitura em vez de leitura/gravação padrão.</li></ul>
   </dd>
   <dt>-p <i>PORT</i>|--publish <i>PORT</i> (opcional)</dt>
   <dd>Exponha a porta para o tráfego HTTP. Contêineres em seu grupo devem atender na porta HTTP. As solicitações HTTPS não podem ser feitas. Para os grupos de contêineres, não é possível incluir várias portas. <br><br>Ao especificar uma porta, você disponibiliza o app para o Balanceador de carga do {{site.data.keyword.Bluemix_notm}} ou para contêineres que estão tentando atingir o host no mesmo espaço do {{site.data.keyword.Bluemix_notm}}. Em seguida, o balanceador de carga ou contêineres do {{site.data.keyword.Bluemix_notm}} podem usar a porta para atingir o host e o app no mesmo espaço do {{site.data.keyword.Bluemix_notm}}. Se uma porta for especificada no Dockerfile para a imagem que você está usando, inclua essa porta. <br>
   <strong>Dicas</strong>: <ul>
   <li>Para a imagem do servidor Liberty certificada pela IBM ou uma versão modificada dessa imagem, insira a porta 9080.</li>
   <li>Para a imagem do Node.js certificada pela IBM ou uma versão modificada dessa imagem, insira a porta 8000.</li>
   </ul>
   </dd>
   <dt>-P (opcional)</dt>
   <dd>Publicar todas as portas</dd>
   <dt>--min <i>MIN_INSTANCE_COUNT</i> (opcional)</dt>
   <dd>O número mínimo de instâncias. O padrão é 1. Se você configurar um número mínimo de instâncias, o valor não poderá ser mudado após a criação do grupo de contêiner.</dd>
   <dt>--max <i>MAX_INSTANCE_COUNT</i> (opcional)</dt>
   <dd>O número máximo de instâncias. O padrão é 2. Se você configurar um número máximo de instâncias, o valor não poderá ser mudado após a criação do grupo de contêiner.</dd>
   <dt>--desired <i>DESIRED_INSTANCE_COUNT</i> (opcional)</dt>
   <dd>O número de instância que você precisa. O padrão é 2.</dd>
   <dt>--auto (opcional)</dt>
   <dd>Quando o grupo de contêiner é criado e a recuperação automática é ativada, o IBM Containers verifica o funcionamento de cada instância com uma solicitação de HTTP para a porta designada.<br>
   Se nenhuma resposta for recebida de uma instância do contêiner em dois intervalos subsequentes de 90 segundos, a instância será removida e substituída por uma nova instância. Nenhuma ação será executada se o contêiner for responsivo. Esse processo é repetido continuamente. Durante uma janela de 30 minutos, se o número total de contêineres diferentes que são membros do grupo for igual ou exceder três vezes o tamanho máximo observado do grupo, a recuperação automática será desativada permanentemente para o grupo de contêiner. Para ativar a recuperação automática novamente, deve-se recriar o grupo de contêineres.</dd>
  <dt>--anti (opcional)</dt>
  <dd> Use antiafinidade para tornar seu grupo de contêiner mais altamente
disponível. A opção --anti força cada instância de contêiner em seu grupo a ser
colocada em um nó de cálculo físico separado, o que reduz as chances de impacto de todos os
contêineres em um grupo devido a uma falha no hardware. Você pode não ser capaz de usar
essa opção com tamanhos de grupo maiores porque cada região e organização do Bluemix tem
um conjunto limitado de nós de cálculo disponíveis para implementação. Se sua
implementação não for bem-sucedida, reduza o número de instâncias de contêiner no grupo
ou remova a opção --anti. </dd>
   <dt><i>CMD</i> (opcional)</dt>
   <dd>O comando e os argumentos são passados para o grupo de contêiner executar. Esse comando deve ser um comando de longa execução. Não use um comando de curta duração que não é executado por muito tempo, por exemplo, <i>/bin/date</i>, pois o comando de curta duração pode fazer o contêiner travar.  <br> <strong>Notas:</strong> <ul>
   <li>O comando e seus argumentos devem vir no final da linha de comandos <i>bluemix ic run</i>.</li>
   <li>Se os argumentos de comando incluírem o hífen -, como em <i>-c</i> no comando de exemplo anterior, o comando deverá ser precedido por dois hifens --.</li>
   </ul></dd>
   </dl>


<strong>Exemplos</strong>:

Crie um grupo de contêiner `my_container_group` usando a imagem `registry.ng.bluemix.net/ibmnode` fornecida pelo IBM Containers e, em seguida, execute o comando de longa execução `ping localhost` nesse grupo de contêiner:

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode ping localhost
```

Crie um grupo de contêiner `my_container_group` usando a imagem `registry.ng.bluemix.net/ibmnode` fornecida pelo IBM Containers e, em seguida, execute o comando de longa execução `tail -f /dev/null` nesse grupo de contêiner:

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode -- tail -f /dev/null
```

Crie um grupo escalável `mygroup` com a recuperação automática ativada usando a imagem `registry.ng.bluemix.net/ibmliberty`. A porta é `9080`, o nome do host é `mycontainerhost` e o nome do domínio é `mybluemix.net`.
```
bluemix ic group-create -p 9080 --auto -n mycontainerhost -d mybluemix.net --name mygroup registry.ng.bluemix.net/ibmliberty
```


## bluemix ic group-inspect
{: #bluemix_ic_group_inspect}

Visualize informações detalhadas, como variáveis de ambiente, portas ou memória, especificadas para um grupo de contêiner quando criado.

```
bluemix ic group-inspect CONTAINER_GROUP
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>CONTAINER_GROUP</i> (obrigatório)</dt>
   <dd>O ID ou o nome do grupo de contêiner.</dd>
   </dl>

<strong>Exemplos</strong>:

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

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>CONTAINER_GROUP</i> (obrigatório)</dt>
   <dd>O ID ou o nome do grupo de contêiner.</dd>
   </dl>

<strong>Exemplos</strong>:

Liste todas as instâncias do grupo de contêiner `my_group`:
```
bluemix ic group-instances my_group
```


## bluemix ic group-remove
{: #bluemix_ic_group_remove}

Remova um grupo de contêiner de um espaço.

```
bluemix ic group-remove [-f|--force] GROUP_NAME [GROUP_NAME2 [...]]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:

   <dl>
   <dt>-f|--force (opcional)</dt>
   <dd>Força a remoção de um contêiner em execução ou com falha.</dd>
   <dt><i>GROUP_NAME</i> (obrigatório)</dt>
   <dd>O ID ou o nome do grupo de contêiner.</dd>
   </dl>


<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para remover um grupo de contêiner, em que `my_group` é o nome do grupo de contêiner.
```
bluemix ic group-remove my_group
```


## bluemix ic group-update
{: #bluemix_ic_group_update}

Atualize um grupo de contêiner.


```
bluemix ic group-update [--anti] [--desired DESIRED_INSTANCE_COUNT] [-e ENV_KEY=ENV_VAL] GROUP_NAME
```

**Dica:** para atualizar o nome do host ou o domínio para um grupo de contêiner, use `bluemix ic route-map [-n HOST][-d DOMAIN] CONTAINER_GROUP`.

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:
 <dl>
   <dt>--anti (opcional)</dt>
   <dd>Use antiafinidade para tornar seu grupo de contêiner mais altamente
disponível. A opção --anti força cada instância de contêiner em seu grupo a ser colocada em um nó de cálculo físico separado, reduzindo as chances de todos os contêineres em um grupo sofrerem um impacto devido a uma falha no hardware. Você pode não ser capaz de usar
essa opção com tamanhos de grupo maiores porque cada região e organização do Bluemix tem
um conjunto limitado de nós de cálculo disponíveis para implementação. Se sua
implementação não for bem-sucedida, reduza o número de instâncias de contêiner no grupo
ou remova a opção --anti.</dd>
   <dt>--desired <i>DESIRED_INSTANCE_COUNT</i> (opcional)</dt>
   <dd>O número de instância que você precisa. O padrão é <i>2</i>.</dd>
   <dt>-e <i>ENV_KEY=ENV_VAL</i>(opcional)</dt>
   <dd>Configure a variável de ambiente. Liste diversas chaves separadamente. Se aspas forem incluídas, inclua-as em torno do nome da variável de ambiente e do valor. Por
exemplo: `-e "key1=value1" -e "key2=value2" -e "key3=value3"`.</dd>
   <dt><i>GROUP_NAME</i> (obrigatório)</dt>
   <dd>O ID ou o nome do grupo de contêiner.</dd>
   </dl>

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para atualizar o grupo de contêiner `my_group`:
```
bluemix ic group-update --desired 5 my_group
```


## bluemix ic groups
{: #bluemix_ic_groups}

Liste grupos de contêineres no repositório privado do {{site.data.keyword.Bluemix_notm}} da organização.

```
bluemix ic groups [-q]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:
	<dl>
	<dt>-q (opcional)</dt>
   	<dd>Exibir somente IDs de grupos</dd>
	</dl>


## bluemix ic images
{: #bluemix_ic_images}

Visualize uma lista de todas as imagens disponíveis no repositório privado do {{site.data.keyword.Bluemix_notm}} da organização. Para obter mais informações, veja o comando [images ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/images){: new_window} na ajuda do Docker. A lista inclui o ID da imagem, a data de criação e o nome da imagem.

```
bluemix ic images [-a|--all] [-f CONDITION] [--no-trunc] [-q|--quiet]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:

   <dl>
   <dt>-a|--all (opcional)</dt>
   <dd>Inclua todas as camadas de imagem para cada imagem no repositório de sua organização, não apenas a camada mais recente.</dd>
   <dt>-f (opcional)</dt>
   <dd>Filtre a lista de imagens pela condição fornecida.</dd>
   <dt>--no-trunc (opcional)</dt>
   <dd>Não trunque a saída.</dd>
   <dt>-q|--quiet (opcional)</dt>
   <dd>Exiba somente os IDs numéricos.</dd>
   </dl>

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para receber uma lista de imagens disponíveis para a organização:
```
bluemix ic images
```


## bluemix ic info
{: #bluemix_ic_info}

Visualize um conjunto de informações que descreva o estado da instância de serviço de nuvem do contêiner. As informações incluem o limite de contêineres, o uso de contêineres, contêineres que estão em execução, o limite de memória, o uso de memória, o limite de endereço IP flutuante, o uso de endereço IP flutuante, a URL do host CCS, a URL do host de registro e o status do modo de depuração.

```
bluemix ic info
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino


## bluemix ic init
{: #bluemix_ic_init}

Inicialize o ambiente de contêineres em sua máquina local para usar os recursos integrais do serviço IBM Containers.

```
bluemix ic init
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

**Nota:** antes da inicialização, assegure que a CLI do Docker (docker) esteja instalada e configurada em sua variável de ambiente PATH. Para alternar para outra região, use o comando `bluemix region-set`.

<strong>Exemplos</strong>:

Alterne para a região `us-south`:

```
bluemix region-set us-south
```


## bluemix ic inspect
{: #bluemix_ic_inspect}

Visualize as informações sobre um contêiner. Para obter mais informações, veja o comando [inspect ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/inspect){: new_window} na ajuda do Docker.

```
bluemix ic inspect [IMAGE|images|CONTAINER]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>IMAGE</i> (obrigatório)</dt>
   <dd>Visualize informações detalhadas sobre uma imagem específica especificando o nome ou o ID da imagem.</dd>
   <dt>images (necessário)</dt>
   <dd>Visualize informações detalhadas sobre todas as imagens em seu repositório.</dd>
   <dt><i>CONTAINER</i> (obrigatório)</dt>
   <dd>Visualize informações detalhadas sobre um contêiner específico especificando o nome ou o ID do contêiner.</dd>
   </dl>

**Dica:** apenas um de *IMAGEM*, *imagens* ou *CONTÊINER* pode ser especificado por vez.

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para inspecionar um contêiner denominado `proxy`:
```
bluemix ic inspect proxy
```


## bluemix ic ip-bind
{: #bluemix_ic_ip_bind}

Ligar um endereço IP flutuante disponível a um contêiner.

```
bluemix ic ip-bind IP_ADDRESS CONTAINER
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>IP_ADDRESS</i> (obrigatório)</dt>
   <dd>O endereço IP a ser ligado.</dd>
   <dt><i>CONTAINER</i> (obrigatório)</dt>
   <dd>O ID ou o nome do contêiner a ser ligado.</dd>
   </dl>

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para ligar o IP endereço `192.123.12.12` ao contêiner `proxy`:
```
bluemix ic ip-bind 192.123.12.12 proxy
```


## bluemix ic ip-release
{: #bluemix_ic_ip_release}

Liberar um endereço IP flutuante da instância do serviço de nuvem do contêiner.

```
bluemix ic ip-release IP_ADDRESS [IP_ADDRESS2 [...]]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>IP_ADDRESS</i> (obrigatório)</dt>
   <dd>O endereço IP para liberação.</dd>
   </dl>


## bluemix ic ip-request
{: #ip_request}
Solicite um novo endereço IP flutuante.

```
bluemix ic ip-request [-q]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:

   <dl>
   <dt>-q (opcional)</dt>
   <dd>Liste somente os endereços IP, sem os IDs dos contêineres que estão ligados a esses endereços IP.</dd>
   </dl>


## bluemix ic ip-unbind
{: #bluemix_ic_ip_unbind}

Desvincular um endereço IP flutuante de seu contêiner.

Endereços IP públicos são um recurso limitado no IBM Containers. Portanto, endereços IP públicos que são alocados para um espaço e não ligados a
um contêiner são periodicamente recuperados de usuários de avaliação grátis, aproximadamente a cada semana. Endereços IP públicos desvinculados nunca são recuperados de clientes de pagamento por uso ou de clientes de assinatura.

```
bluemix ic ip-unbind IP_ADDRESS CONTAINER
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>IP_ADDRESS</i> (obrigatório)</dt>
   <dd>O endereço IP a ser desvinculado.</dd>
   <dt><i>CONTAINER</i> (obrigatório)</dt>
   <dd>O ID ou o nome do contêiner a ser desvinculado.</dd>
   </dl>

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para desvincular o IP endereço `192.123.12.12` do contêiner `proxy`:
```
bluemix ic ip-unbind 192.123.12.12 proxy
```


## bluemix ic ips
{: #bluemix_ic_ips}

Listar os endereços IP flutuantes disponíveis para o usuário com login efetuado. A lista inclui endereços IP e o ID do contêiner ao qual os endereços IP são vinculadas. Se o endereço IP não for usado, nenhum ID de contêiner será mostrado.

```
bluemix ic ips [-q]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:

   <dl>
   <dt>-q (opcional)</dt>
   <dd>Liste somente os endereços IP, sem os IDs dos contêineres que estão ligados a esses endereços IP.</dd>
   </dl>


<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para receber uma lista de todos os endereços IP da organização.
```
bluemix ic ips -q
```


## bluemix ic kill
{: #bluemix_ic_kill}

Pare um processo em execução em um contêiner sem parar o contêiner. Para obter mais informações, veja o comando [kill ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/kill/){: new_window} na ajuda do Docker.

```
bluemix ic kill [-s CMD|--signal CMD] CONTAINER
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:

   <dl>
   <dt>-s <i>CMD</i>|--signal <i>CMD</i> (opcional)</dt>
   <dd>Envie um comando para o processo que estiver em execução no contêiner.</dd>
   <dt><i>CONTAINER</i> (obrigatório)</dt>
   <dd>O ID ou o nome do contêiner.</dd>
   </dl>


<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para encerrar o processo em um contêiner denominado `proxy`:
```
bluemix ic kill proxy
```


## bluemix ic logs
{: #bluemix_ic_logs}

Mostre os logs de saída ou de erro para um contêiner em execução. Para obter mais informações, veja o comando [logs ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/logs/){: new_window} na ajuda do Docker.
```
bluemix ic logs [OPTIONS] CONTAINER
```


## bluemix ic namespace-get
{: #bluemix_ic_namespace_get}

Visualize o nome do repositório de imagem privada do {{site.data.keyword.Bluemix_notm}} da organização na qual você está com login efetuado.

```
bluemix ic namespace-get
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino


## bluemix ic namespace-set
{: #bluemix_ic_namespace_set}

Configure o nome do repositório de imagem privada do {{site.data.keyword.Bluemix_notm}} da organização na qual você está com login efetuado.

*Restrição*: não é possível usar um hyphen `-` no nome de seu namespace de repositório.

```
bluemix ic namespace-set NAME
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>NAME</i> (obrigatório)</dt>
   <dd>Uma função de vez única para configurar o namespace do repositório para a sua organização, se ele ainda não estiver configurado. Após configurar o namespace, reinicialize o IBM Containers por meio do comando `bluemix ic init` antes de continuar.</dd>
   </dl>


## bluemix ic pause
{: #pause}

Pausar todos os processos em um contêiner em execução. Para obter mais informações, veja o comando [pause ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/pause/){: new_window} na ajuda do Docker. Para parar um contêiner, consulte o comando [bluemix ic unpause](#unpause).

```
bluemix ic pause CONTAINER
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:
   <dl>
   <dt><i>CONTAINER</i> (obrigatório)</dt>
   <dd>O nome ou ID do contêiner.</dd>
   </dl>

<strong>Respostas</strong>:

- Contêiner pausado com sucesso.

- O comando falhou com o serviço de nuvem do contêiner

 `{message}`

 Em que
`{message}` é o erro relacionado.

- Comando com falha - Não foi possível se conectar ao serviço de nuvem do contêiner

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para pausar um contêiner denominado `proxy`:
```
bluemix ic pause proxy
```


## bluemix ic port
{: #bluemix_ic_port}

Liste mapeamentos de porta ou um mapeamento específico para o contêiner. Esse comando agrupa o comando `docker port`. Para obter mais informações, veja o comando [port ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/port/){: new_window} na ajuda do Docker.


## bluemix ic ps
{: #bluemix_ic_ps}
Visualize uma lista de contêineres que estão em execução no namespace do usuário com login efetuado. Por padrão, esse comando mostra somente os contêineres que estão em execução. Para obter mais informações, veja o comando [ps ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/ps/){: new_window} na ajuda do Docker.

```
bluemix ic ps [-a|--all] [--filter env=SEARCH_CRITERIA] [-s|--size] [-l NUM|--limit NUM] [-q|--quiet]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:

   <dl>
   <dt>-a|--all (opcional)</dt>
   <dd>Mostre todos os contêineres, em execução e interrompidos.</dd>
   <dt>--filter env=<i>SEARCH_CRITERIA</i> (opcional)</dt>
   <dd>Procure contêineres que possuem um valor específico da variável de ambiente. É possível filtrar seus contêineres por qualquer chave ou valor de variável de ambiente listados na seção Env da resposta da CLI ao inspecionar um contêiner. Substitua SEARCH_CRITERIA pela chave ou valor que você está procurando. Seus
critérios de procura não precisam ser uma correspondência exata. </dd>
   <dt>-s|--size (opcional)</dt>
   <dd>Liste os tamanhos dos contêineres.</dd>
   <dt>-l <i>NUM</i>|--limit <i>NUM</i> (opcional)</dt>
   <dd>Liste os contêineres criados mais recentemente, em que <i>NUM</i> é o número dos contêineres criados mais recentemente que você deseja retornar. <br><br> Por exemplo, se você criou contêineres
<i>node1</i> até <i>node5</i> sequencialmente, o comando <i>bluemix ic ps --limit 2</i> retornará node4 e node5 porque eles são os últimos dois contêineres criados. </dd>
   <dt>-q|--quiet (opcional)</dt>
   <dd>Exiba somente os IDs de contêineres.</dd>
   </dl>


<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para ver todos os contêineres em execução e interrompidos:
```
bluemix ic ps -a
```


## bluemix ic rename
{: #bluemix_ic_rename}
Renomear um contêiner. Para obter mais informações, veja o comando [rename ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/rename/){: new_window} na ajuda do Docker.

```
bluemix ic rename OLD_NAME NEW_NAME
```
<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:

<dl>
   <dt><i>OLD_NAME</i> (obrigatório)</dt>
   <dd>O nome antigo do contêiner.</dd>
   <dt><i>NEW_NAME</i> (obrigatório)</dt>
   <dd>O novo nome do contêiner.</dd>
   </dl>


## bluemix ic reprovision
{: #bluemix_ic_reprovision}

Recrie o serviço IBM Containers no espaço do Bluemix em que você efetuou login. A
cota original para o espaço é mantida.

<strong>Importante</strong>: quando você executa esse comando, nenhum dos seus contêineres únicos e grupos nesse espaço será migrado para o espaço reprovisionado e eles serão removidos durante o processo de migração.

```
bluemix ic reprovision [--force|-f] [ENVIRONMENT_NAME]
```
<strong>Opções de comando</strong>:

<dl>
   <dt>--force|-f (opcional)</dt>
   <dd>Força a recriação do serviço IBM Containers no espaço do Bluemix.</dd>
   <dt><i>AVAILABILITY_ZONE</i> (opcional)</dt>
   <dd>O nome da zona de disponibilidade do IBM Containers em que seus contêineres são implementados. Se nenhuma zona de disponibilidade estiver especificada, a zona de disponibilidade padrão que está configurada para a região será usada.</dd>
   </dl>


## bluemix ic restart
{: #bluemix_ic_restart}

Reiniciar um contêiner. Para obter mais informações, veja o comando [restart ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/restart/){: new_window} na ajuda do Docker.

```
bluemix ic restart CONTAINER [-t SECS|--time SECS]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>CONTAINER</i> (obrigatório)</dt>
   <dd>O nome ou ID do contêiner.</dd>
   <dt>-t <i>SECS</i>|--time <i>SECS</i> (opcional)</dt>
   <dd>O número de segundos a aguardar antes que o contêiner seja reiniciado.</dd>
   </dl>


<strong>Respostas</strong>:

- Contêiner reiniciado com sucesso.

- O comando falhou com o serviço de nuvem do contêiner

 `{message}`

 Em que
`{message}` é o erro relacionado.

- Comando com falha - Não foi possível se conectar ao serviço de nuvem do contêiner

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para reiniciar um contêiner denominado `proxy`:
```
bluemix ic restart proxy
```


## bluemix ic rm
{: #bluemix_ic_rm}

Remover um contêiner. Para obter mais informações, veja o comando [rm ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/rm/){: new_window} na ajuda do Docker.

```
bluemix ic rm [-f|--force] CONTAINER
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:

   <dl>
   <dt>-f|--force (opcional)</dt>
   <dd>Força a remoção de um contêiner em execução ou com falha.</dd>
   <dt><i>CONTAINER</i> (obrigatório)</dt>
   <dd>O nome ou ID do contêiner.</dd>
   </dl>

<strong>Respostas</strong>:

- Contêiner removido com sucesso.

- O comando falhou com o serviço de nuvem do contêiner

 `{message}`

 Em que
`{message}` é o erro relacionado.

- Comando com falha - Não foi possível se conectar ao serviço de nuvem do contêiner.

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para remover um contêiner denominado `proxy`:
```
bluemix ic rm proxy
```


## bluemix ic rmi
{: #bluemix_ic_rmi}

Remover uma imagem do namespace do usuário com login efetuado. Para obter mais informações, veja o comando [rmi ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/rmi/){: new_window} na ajuda do Docker.

```
bluemix ic rmi [-R REGISTRY|--registry REGISTRY] IMAGE
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:

   <dl>
   <dt>-R <i>REGISTRY</i>|--registry <i>REGISTRY</i> (opcional)</dt>
   <dd>Alterar o host de registro. O padrão é usar o registro que você especifica no comando <i>bluemix ic init</i>.</dd>
   <dt><i>IMAGE</i> (obrigatório)</dt>
   <dd>O nome da imagem que você deseja remover. Se uma tag não for especificada no nome da imagem, a imagem identificada por último (<i>latest</i>) será excluída, por padrão.</dd>
   </dl>

<strong>Respostas</strong>:

- Removido: `{IMAGE}`

 Em que `{IMAGE}` é o nome da imagem que foi removida.

- Erro! Nenhum host de registro especificado.

- Remoção de imagem com falha - Não foi possível se conectar ao registro de nuvem do contêiner

- O comando falhou com o serviço de nuvem do contêiner

 `{message}`

 Em que
`{message}` é o erro relacionado.

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para remover a imagem `mynamespace/myimage:latest`:
```
bluemix ic rmi registry.ng.bluemix.net/mynamespace/myimage:latest
```


## bluemix ic route-map
{: #bluemix_ic_route_map}

Estabelecer a rota para o tráfego de Internet a ser usada para acessar o grupo de contêiner. Você pode usar esse comando para estabelecer uma nova rota ou atualizar uma rota existente.

```
bluemix ic route-map [-n HOST|--hostname HOST] [-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:

   <dl>
   <dt>-n <i>HOST</i>|--hostname <i>HOST</i> (opcional)</dt>
   <dd>O nome do host para a rota. O nome do host é a primeira parte da URL da rota pública completa, como <i>mycontainerhost</i> na URL <i>mycontainerhost.mybluemix.net</i>.</dd>
   <dt>-d <i>DOMAIN</i>|--domain <i>DOMAIN</i> (opcional)</dt>
   <dd>O nome do domínio para a rota, que é a segunda parte da URL da rota pública completa. Na maioria dos casos, o domínio é <i>mybluemix.net</i>. Também é possível usar esse parâmetro para especificar um domínio privado.</dd>
   <dt><i>CONTAINER_GROUP</i> (obrigatório)</dt>
   <dd>O ID ou o nome do grupo de contêiner.</dd>
   </dl>

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para mapear a rota para o grupo que é chamado `GROUP1`, em que `my_host` é o nome do host e `mybluemix.net` é o domínio.
```
bluemix ic route-map -n my_host -d mybluemix.net GROUP1
```


## bluemix ic route-unmap
{: #bluemix_ic_route_unmap}

Estabelecer a rota para o tráfego de Internet a ser usada para acessar o grupo de contêiner. Você pode usar esse comando para estabelecer uma nova rota ou atualizar uma rota existente.

```
bluemix ic route-unmap [-n HOST|--hostname HOST] [-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:

   <dl>
   <dt>-n <i>HOST</i>|--hostname <i>HOST</i> (opcional)</dt>
   <dd>O nome do host para a rota.</dd>
   <dt>-d <i>DOMAIN</i>|--domain <i>DOMAIN</i> (opcional)</dt>
   <dd>O nome de domínio para a rota.</dd>
   <dt><i>CONTAINER_GROUP</i> (obrigatório)</dt>
   <dd>O ID ou o nome do grupo de contêiner.</dd>
   </dl>

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para remover mapeamento da rota para o grupo chamado `GROUP1`, em que `my_host` é o nome do host e
`organization.com` é o domínio.
```
bluemix ic route-unmap -n my_host -d organization.com GROUP1
```


## bluemix ic run
{: #bluemix_ic_run}

Iniciar um novo contêiner no serviço de nuvem de contêiner a partir de um nome de imagem. Para obter mais informações, veja o comando [run ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/run/){: new_window} na ajuda do Docker.


```
bluemix ic run [-p PORT|--publish PORT] [-P] [-m MEMORY|--memory MEMORY] [-e ENV|--env ENV] [--volume VOLUME:CONTAINER_PATH] -n NAME|--name NAME [--link NAME:ALIAS] [-it] IMAGE [CMD [CMD ...]]
```
**Nota:** assegure-se de que a ferramenta de comando do Cloud Foundry esteja instalada e de que você tenha um token do Cloud Foundry. O login bem-sucedido usando `bluemix
login` e `bluemix ic init` gera o token e os certificados necessários.


<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:

   <dl>
   <dt>-p <i>PORT</i>|--publish <i>PORT</i> (opcional)</dt>
   <dd>Exponha a porta para o tráfego HTTP. Inclua quaisquer portas especificadas no Dockerfile para a imagem que você está usando. É possível incluir várias portas com várias
opções <i>-p</i>. Expor uma porta irá automaticamente ligar um endereço IP público ao contêiner se um endereço IP público estiver disponível. <br><br>Se você tiver um endereço IP existente no espaço que deseja ligar ao contêiner, será possível especificar o endereço IP em vez de ligá-lo posteriormente. O endereço IP deve ser especificado no formato: &lt;ip-address&gt;:&lt;container-port&gt;:&lt;container-port&gt; <br><br>Para obter mais informações sobre como solicitar endereços IP para um espaço, consulte o comando <a href="index.html#ip_request" target="_blank">bluemix ic ip-request</a>. <br><br>Ao especificar uma porta, você está tornando o app disponível para o {{site.data.keyword.Bluemix_notm}} Load Balancer ou para os contêineres no mesmo espaço do {{site.data.keyword.Bluemix_notm}} que estão tentando atingir o host. Se uma porta for especificada no Dockerfile para a imagem que você está usando, inclua essa porta. <br><br><strong>Dicas:</strong><ul><li>Para a imagem do servidor Liberty certificada pela IBM ou uma versão modificada dessa imagem, insira a porta 9080.</li><li>Para a imagem do Node.js certificada pela IBM ou uma versão modificada dessa imagem, insira a porta 8000.</li></ul></dd>
   <dt>-P (opcional)</dt>
   <dd>Exponha automaticamente as portas que estão especificadas no Dockerfile da imagem para o tráfego HTTP.</dd>
   <dt>-m <i>MEMORY</i>|--memory <i>MEMORY</i> (opcional)</dt>
   <dd>Designe um limite de memória ao grupo em MB. Ao criar um grupo de contêiner a partir da CLI, o valor padrão para cada instância de contêiner é 64 MB.  Ao criar um grupo de contêiner a partir do Painel
do {{site.data.keyword.Bluemix_notm}}, o valor padrão para cada instância é 256 MB. Os valores aceitos são 64, 256, 512, 1024 e 2048. Após um limite de memória ser designado, o valor não poderá ser mudado.</dd>
   <dt>-e <i>ENV</i>|--env <i>ENV</i> (opcional)</dt>
   <dd>Configure a variável de ambiente, em que <i>ENV</i> é um par de key=value. Liste diversas chaves separadamente. Se aspas forem incluídas, inclua-as em torno do nome da variável de ambiente e do valor. Por
exemplo: -e "key1=value1" -e "key2=value2" -e "key3=value3". A tabela a seguir mostra algumas variáveis de ambiente comumente usadas que podem ser especificadas:</dd>
   </dl>


|      Variável do ambiente                          |   Descrição                              |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;appname&gt;*       | Faça a ligação de um serviço a um contêiner. Use a variável de ambiente `CCS_BIND_APP` para ligar um aplicativo ao contêiner. O app é ligado ao serviço de destino e age como uma ponte que permite que o {{site.data.keyword.Bluemix_notm}} traga as informações de `VCAP_SERVICES` de seu app de ponte para a instância do contêiner em execução. Para obter mais informações sobre como criar um app de ponte, consulte [Ligando um serviço a um contêiner](../../../containers/container_integrations_binding.html){: new_window}. |
| CCS_BIND_SRV=*&lt;service_instance_name1&gt;*,*&lt;service_instance_name2&gt;* | Para ligar um serviço Bluemix diretamente a um contêiner, sem usar um app de ponte, use CCS_BIND_SRV. Essa ligação permite que o Bluemix injete as informações de VCAP_SERVICES na instância do contêiner em execução. Para listar vários serviços do Bluemix, inclua-os como parte da mesma variável de ambiente. |
| LOG_LOCATIONS=*&lt;path_to_file&gt;* | Inclua um arquivo de log a ser monitorado no contêiner. Inclua a variável de ambiente `LOG_LOCATIONS` com um caminho para o arquivo de log. |
{: caption="Table 3. Commonly used environment variables" caption-side="top"}


   <dl>
   <dt>--volume <i>VOLUME</i>:<i>CONTAINER_PATH</i>[:ro] (opcional)</dt>
   <dd>Anexe um volume a um contêiner especificando os detalhes no formato <i>VolumeId:ContainerPath[:ro]</i>.
   <ul>
   <li><i>VOLUME</i>: O ID ou o nome do volume.</li>
   <li><i>CONTAINER_PATH</i>: O caminho absoluto para o volume no contêiner.</li>
   <li>ro: opcional. Especificar <i>ro</i> torna o volume somente leitura em vez de leitura/gravação padrão.</li></ul>
   </dd>
   <dt>-n <i>NAME</i>|--name <i>NAME</i> (necessário)</dt>
   <dd>Designe um nome ao contêiner. <br> <strong>Dica:</strong> o nome do contêiner deve iniciar com uma letra. O nome pode incluir letras maiúsculas, letras minúsculas, números, pontos., sublinhados _ ou hifens -.</dd>
   <dt>--link <i>NAME</i>:<i>ALIAS</i> (opcional)</dt>
   <dd>Sempre que você quiser que um contêiner se comunique com outro contêiner que estiver em execução, é possível endereçá-lo usando um alias para o nome do host.</dd>
   <dt>-it (opcional)</dt>
   <dd>Execute o contêiner em um modo interativo. Após a criação do contêiner, manter a exibição da entrada padrão. Digite <i>exit</i> para sair.</dd>
   <dt><i>IMAGE</i> (obrigatório)</dt>
   <dd>A imagem a ser incluída no contêiner. É possível listar comandos após a imagem, mas não coloque nenhuma opção após a imagem. Inclua todas as opções antes de especificar uma imagem. Inclua todas as opções antes de especificar uma imagem. <br><br>Se você usar uma imagem no repositório privado do {{site.data.keyword.Bluemix_notm}} de sua organização, especifique a imagem no formato: <i>registry.ng.bluemix.net/NAMESPACE/IMAGE</i>. <br><br>Se você usar uma imagem que é fornecida pelo IBM Containers, especifique a imagem no formato: <i>registry.ng.bluemix.net/IMAGE</i>. </dd>
   <dt><i>CMD</i> (opcional)</dt>
   <dd>O comando e os argumentos são passados para o grupo de contêiner executar. Esse comando deve ser um comando de longa execução. Não use um comando de curta duração que não é executado por muito tempo, por exemplo, <i>/bin/date</i>, pois o comando de curta duração pode fazer o contêiner travar.</dd>
   </dl>


<strong>Exemplos</strong>:

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


## bluemix ic service-bind
{: #bluemix_ic_service-bind}

Inclua um serviço em um grupo de contêiner em execução. Esse comando está
disponível apenas para grupos de contêineres. Contêineres únicos devem ligar um serviço
como parte do comando bluemix ic run.

```
bluemix ic service-bind GROUP_NAME SERVICE_INSTANCE
```
<strong>Opções de comando</strong>:

   <dl>
   <dt><i>GROUP_NAME</i> (obrigatório)</dt>
   <dd>O ID ou nome do grupo.</dd>
   <dt><i>SERVICE_INSTANCE</i> (obrigatório)</dt>
   <dd>O nome da instância de serviço a ser incluída no grupo de contêiner.</dd>
   </dl>


## bluemix ic service-unbind
{: #bluemix_ic_service-unbind}

Remova um serviço de um grupo de contêiner em execução. Esse comando está
disponível apenas para grupos de contêineres. Contêineres únicos devem remover o contêiner e criar um
novo sem o serviço.

```
bluemix ic service-unbind GROUP_NAME SERVICE_INSTANCE
```
<strong>Opções de comando</strong>:

   <dl>
   <dt><i>GROUP_NAME</i> (obrigatório)</dt>
   <dd>O ID ou nome do grupo.</dd>
   <dt><i>SERVICE_INSTANCE</i> (obrigatório)</dt>
   <dd>O nome da instância de serviço a ser incluída no grupo de contêiner.</dd>
   </dl>


## bluemix ic start
{: #ic_start}
Iniciar um contêiner interrompido. Para obter mais informações, veja o comando [start ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/start/){: new_window} na ajuda do Docker. Para parar um contêiner, consulte o comando [bluemix ic stop](#ic_stop).

```
bluemix ic start CONTAINER
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>CONTAINER</i> (obrigatório)</dt>
   <dd>O nome ou ID do contêiner.</dd>
   </dl>


<strong>Respostas</strong>:

- Contêiner iniciado com sucesso.

- O comando falhou com o serviço de nuvem do contêiner

 `{message}`

 Em que
`{message}` é o erro relacionado.

- Comando com falha - Não foi possível se conectar ao serviço de nuvem do contêiner

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para iniciar um contêiner denominado `proxy`.
```
bluemix ic start proxy
```


## bluemix ic stats
{: #bluemix_ic_stats}

Para um ou mais contêineres, visualizar estatísticas de uso em tempo real. Use `CTRL+C` para sair. Para obter mais informações, veja o comando [stats ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/stats/){: new_window} na ajuda do Docker.

```
bluemix ic stats [--no-stream] CONTAINER [CONTAINER]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>CONTAINER</i> (obrigatório)</dt>
   <dd>O nome ou ID do contêiner.</dd>
   <dt>--no-stream (opcional)</dt>
   <dd>Exiba somente o resultado mais recente e não inclua nenhuma informação que o preceda.</dd>
   </dl>

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para as estatísticas mais recentes sobre um contêiner:
```
bluemix ic stats --no-stream my_container
```


## bluemix ic stop
{: #ic_stop}
Parar um contêiner em execução. Para obter mais informações, veja o comando [stop ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/stop/){: new_window} na ajuda do Docker. Para iniciar um contêiner, consulte o comando [bluemix ic start](#ic_start).

```
bluemix ic stop CONTAINER [-t SECS|--time SECS]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>CONTAINER</i> (obrigatório)</dt>
   <dd>O nome ou ID do contêiner.</dd>
   <dt>-t <i>SECS</i>|--time <i>SECS</i> (opcional)</dt>
   <dd>O número de segundos a esperar antes que o contêiner seja eliminado.</dd>
   </dl>

<strong>Respostas</strong>:

- Contêiner interrompido com sucesso.

- O comando falhou com o serviço de nuvem do contêiner

 `{message}`

 Em que
`{message}` é o erro relacionado.

- Comando com falha - Não foi possível se conectar ao serviço de nuvem do contêiner

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para parar um contêiner denominado `proxy`.
```
bluemix ic stop proxy
```


## bluemix ic top
{: #bluemix_ic_top}

Mostrar os processos que estão em execução no contêiner. Para obter mais informações, veja o comando [top ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/top/){: new_window} na ajuda do Docker.

```
bluemix ic top CONTAINER [CONTAINER]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>CONTAINER</i> (obrigatório)</dt>
   <dd>O nome ou ID do contêiner.</dd>
   </dl>

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para exibir os processos em um contêiner chamado `my_container`.
```
bluemix ic top my_container
```


## bluemix ic unpause
{: #unpause}

Remover pausa de todos os processos em um contêiner em execução. Para obter mais informações, veja o comando [unpause ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/unpause/){: new_window} na ajuda do Docker. Para pausar um contêiner, consulte o comando [bluemix ic pause](#pause).

```
bluemix ic unpause CONTAINER
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>CONTAINER</i> (obrigatório)</dt>
   <dd>O nome ou ID do contêiner.</dd>
   </dl>

<strong>Respostas</strong>:

- Contêiner removido da pausa com sucesso.

- O comando falhou com o serviço de nuvem do contêiner

 `{message}`

 Em que
`{message}` é o erro relacionado.

- Comando com falha - Não foi possível se conectar ao serviço de nuvem do contêiner

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para remover da pausa um contêiner denominado `proxy`:
```
bluemix ic unpause proxy
```


## bluemix ic unprovision
{: #bluemix_ic_unprovision}

Exclua o serviço IBM Containers do espaço do Bluemix em que você efetuou login.

<strong>Atenção</strong>: Quando você executar esse comando, todos os contêineres
únicos e grupos de contêineres serão perdidos. Seu espaço ainda estará disponível no
Bluemix. Para começar a usar o IBM Containers novamente, deve-se executar `bluemix ic reprovision` para provisionar o serviço IBM Containers novamente.

```
bluemix ic reprovision [--force|-f]
```
<strong>Opções de comando</strong>:

<dl>
   <dt>--force|-f (opcional)</dt>
   <dd>Força a exclusão do Bluemix do espaço do Bluemix.</dd>
 </dl>


## bluemix ic version
{: #bluemix_ic_version}

Mostre a versão do Docker e a API do IBM Containers.

```
bluemix ic version
```

<strong>Pré-requisitos</strong>: Docker

Para ver a versão do IBM Containers, execute `bluemix ic info`. Para obter mais informações, veja o comando [version ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/version/){: new_window} na ajuda do Docker.


## bluemix ic volume-create
{: #bluemix_ic_volume_create}

Crie um volume.

```
bluemix ic volume-create VOLUME_NAME FS_NAME
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>FS_NAME</i> (opcional)</dt>
   <dd>O nome do compartilhamento de arquivo. Se nenhum compartilhamento de arquivo estiver disponível ou nomeado, o volume será construído
no compartilhamento de arquivo padrão do espaço.</dd>
   <dt><i>VOLUME_NAME</i> (obrigatório)</dt>
   <dd>O nome do volume. O nome pode conter letras minúsculas, números, sublinhados _ e hifens -.</dd>
   </dl>


<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para criar um volume.
```
bluemix ic volume-create volume_name fileshare_name
```


## bluemix ic volume-fs
{: #bluemix_ic_volume_fs}

Liste os compartilhamentos de arquivos.

```
bluemix ic volume-fs
```


## bluemix ic volume-fs-create
{: #bluemix_ic_volume_fs_create}

Criar um compartilhamento de arquivo.

```
bluemix ic volume-fs-create FILE_SHARE_NAME
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>FILE_SHARE_NAME</i> (obrigatório)</dt>
   <dd>O nome do compartilhamento de arquivo. O nome pode conter letras minúsculas, números, sublinhados _ e hifens -.</dd>
   </dl>

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para criar um compartilhamento de arquivo.
```
bluemix ic volume-fs-create my_file_share
```


## bluemix ic volume-fs-flavors
{: #bluemix_ic_volume_fs_flavors}

Liste todos os tipos de compartilhamento de arquivo.

```
bluemix ic volume-fs-flavors
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino


## bluemix ic volume-fs-inspect
{: #bluemix_ic_volume_fs_inspect}

Inspecione um compartilhamento de arquivo.

```
bluemix ic volume-fs-inspect FILE_SHARE_NAME
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:

  <dl>
  <dt><i>FILE_SHARE_NAME</i> (obrigatório)</dt>
   <dd>O nome do compartilhamento de arquivo.</dd>
   </dl>

<strong>Exemplos</strong>:

O exemplo a seguir é uma solicitação para inspecionar um compartilhamento de arquivo, em que `my_file_share` é o nome do compartilhamento de arquivo.
```
bluemix ic volume-fs-inspect my_file_share
```


## bluemix ic volume-fs-remove
{: #bluemix_ic_volume_fs_remove}

Remover um compartilhamento de arquivo.

```
bluemix ic volume-fs-remove FILE_SHARE_NAME
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>FILE_SHARE_NAME</i> (obrigatório)</dt>
   <dd>O nome do compartilhamento de arquivo.</dd>
   </dl>

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para remover um compartilhamento de arquivo, em que `my_file_share` é o nome do compartilhamento de arquivo.
```
bluemix ic volume-fs-remove my_file_share
```


## bluemix ic volume-inspect
{: #bluemix_ic_volume_inspect}

Inspecione um volume.

```
bluemix ic volume-inspect VOLUME_NAME
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>VOLUME_NAME</i> (obrigatório)</dt>
   <dd>O nome do volume.</dd>
   </dl>

<strong>Exemplos</strong>:

O exemplo a seguir é uma solicitação para inspecionar um volume, em que `volume_name` é o nome do volume.
```
bluemix ic volume-inspect volume_name
```


## bluemix ic volume-remove
{: #bluemix_ic_volume_remove}

Remova um volume.

```
bluemix ic volume-remove VOLUME_NAME
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>VOLUME_NAME</i> (obrigatório)</dt>
   <dd>O nome do volume.</dd>
    </dl>

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para remover um volume, em que `volume_name` é o nome do volume.
```
bluemix ic volume-remove volume_name
```


## bluemix ic volumes
{: #bluemix_ic_volumes}

Liste os volumes.

```
bluemix ic volumes
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino


## bluemix ic wait
{: #bluemix_ic_wait}

Sair de um contêiner e exibir o código de saída como confirmação. Para obter mais informações, veja o comando [wait ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/wait/){: new_window} na ajuda do Docker.

```
bluemix ic wait CONTAINER [CONTAINER]
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>CONTAINER</i> (obrigatório)</dt>
   <dd>O nome ou ID do contêiner.</dd>
   </dl>

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para sair de um contêiner denominado `my_container`:
```
bluemix ic wait my_container
```


## bluemix ic wait-status
{: #bluemix_ic_wait_status}

Aguarde até que um único contêiner ou um grupo de contêiner atinja um estado não
temporário. Durante esse tempo de espera, a linha de comandos
não é retornada e você não pode inserir os comandos. Assim que o contêiner atinge um
estado não temporário, uma mensagem de OK é exibida. Para contêineres únicos, os estados
não temporários incluem Executando, Encerramento, Travado, Pausado ou Suspenso. Para
grupos de contêineres, os estados não temporários incluem CREATE_COMPLETE,
UPDATE_COMPLETE ou FAILED

```
bluemix ic wait-status CONTAINER
```

<strong>Pré-requisitos</strong>: Terminal, Login, Destino, Docker

<strong>Opções de comando</strong>:

   <dl>
   <dt><i>CONTAINER</i> (obrigatório)</dt>
   <dd>O nome ou ID do contêiner.</dd>
   </dl>

<strong>Exemplos</strong>:

O exemplo a seguir mostra uma solicitação para sair de um contêiner denominado `my_container`:
```
bluemix ic wait my_container
```
