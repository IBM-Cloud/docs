---

 

copyright:

  years: 2015, 2016

 

---
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Comandos do Cloud Foundry (cf)

*Última atualização: 29 de janeiro de 2016*

É possível usar os comandos do Cloud Foundry (cf) para gerenciar os seus apps.
{:shortdesc}

As informações a seguir listam os comandos cf usados mais comumente para gerenciar apps. Para listar todos os comandos cf e suas informações de ajuda, use `cf help`. Use `cf command_name -h` para visualizar informações detalhadas da ajuda para um comando específico.

*Nota:* Se a sua rede contiver um servidor proxy HTTP entre o host que executa os comandos cf e o terminal da API do Cloud Foundry, deve-se especificar o nome do host ou endereço IP do servidor proxy configurando a variável de ambiente `HTTP_PROXY`. Para obter detalhes, consulte [Usando a CLI cf com um Servidor Proxy HTTP](http://docs.cloudfoundry.org/devguide/installcf/http-proxy.html).

## cf api

Exibe ou especifica a URL do terminal da API do {{site.data.keyword.Bluemix_notm}}.
```
cf api BluemixServerURL
```
<dl>
<dt>BluemixServerURL</dt>
<dd>A URL do terminal da API do Bluemix que você deve especificar ao se conectar ao {{site.data.keyword.Bluemix_notm}}. Normalmente, essa URL é https://api.{DomainName}.
Se você deseja exibir a URL do terminal da API que estiver usando atualmente, não será necessário especificar esse parâmetro para o comando cf api.</dd>
<dt>*--skip-ssl-validation*</dt>
<dd>Desativa o processo de validação SSL. O uso desse parâmetro pode causar problemas de segurança.</dd>
<dt>*--unset*</dt>
<dd>Remove as informações de conexão para todos os terminais API.</dd>
</dl>

## cf apps

Lista todos os aplicativos que você implementou no espaço atual. O status
de cada aplicativo também é exibido.

Suponha que tenha uma instância para um app, na coluna de instâncias da resposta do comando cf apps, você verá 1/1 se seu app estiver ativo e 0/1 se seu app estiver inativo. Se você vir ?/1, que indica que o estado da instância do app é desconhecido, será possível copiar a URL do app para seu navegador para verificar se o app responde ou acompanhar o log pelo comando `cf logs appname` para ver se o app está gerando conteúdo de log.

## cf bind-service

Liga uma instância de serviço existente ao seu aplicativo.
```
cf bind-service appname service_instance
```

Por exemplo, se você tiver uma instância de serviço nomeada `my_dataworks` em sua organização e espaço atuais, é possível usar `cf bind-service my_app
my_dataworks` para ligar essa instância de serviço ao seu aplicativo.

<dl>
<dt>appname</dt>
<dd>O nome do aplicativo.</dd>
<dt>service_instance</dt>
<dd>O nome da instância de serviço existente.</dd>
</dl>

## cf create-service

Cria uma instância de serviço.
```
cf create-service service_name service_plan service_instance
```
Por exemplo, é possível usar `cf create-service DataWorks free my_dataworks` para criar uma instância do serviço {{site.data.keyword.dataworks_short}} com um plano grátis.

<dl>
<dt>nome_do_serviço</dt>
<dd>O nome do serviço.</dd>
<dt>service_plan</dt>
<dd>O nome do plano de serviço.</dd>
<dt>service_instance</dt>
<dd>O nome que você deseja usar para a nova instância de serviço que você criar.</dd>
</dl>

## cf create-space

Cria um espaço.
```
cf create-space space_name
```
<dl>
<dt>space_name</dt>
<dd>O nome do espaço.</dd>
<dt>*-o *</dt>
<dd>O nome da organização dentro do qual você deseja criar um espaço.</dd>
<dt>*-q
*</dt>
<dd>A cota para designar ao espaço recentemente criado. Se não especificado, uma cota padrão será designada automaticamente.</dd>
</dl>

## cf delete

Exclui um aplicativo existente.
```
cf delete appname
```
<dl>
<dt>appname</dt>
<dd>O nome do aplicativo.<dd>
<dt>*-f*</dt>
<dd>Força a exclusão do aplicativo sem nenhuma confirmação. Esse parâmetro é opcional.</dd>
<dt>*-r*</dt>
<dd>Exclui todos os nomes de domínio que são associados com o aplicativo. Esse parâmetro é opcional.</dd>
</dl>

## cf delete-space

Exclui um espaço.
```
cf delete-space space_name
```
<dl>
<dt>space_name</dt>
<dd>O nome do espaço.</dd>
<dt>*-f*</dt>
<dd>Força a exclusão do espaço sem nenhuma confirmação. Esse parâmetro é opcional.</dd>
*Nota:* A exclusão de um espaço é uma operação irreversível.
</dl>

## cf events

Exibe eventos de tempo de execução que estão relacionados a um aplicativo.
```
cf events appname
```
<dl>
<dt>appname</dt>
<dd>O nome do aplicativo.</dd>
</dl>

## cf help

Exibe informações da ajuda para todos os comandos cf ou para um comando cf específico se o parâmetro command_name for usado.
```
cf help command_name
```
<dl>
<dt>command_name</dt>
<dd>O nome de um comando. Se desejar informações de ajuda que sejam específicas para um comando, é possível usar esse
parâmetro.</dd>
<dd>Se você não especificar esse parâmetro, informações de ajuda de todos os comandos cf serão exibidas.</dd>
</dl>


## cf login

Efetua seu
login no {{site.data.keyword.Bluemix_notm}}.
```
cf login
```
É possível usar um ou mais dos parâmetros a seguir ao emitir o comando cf login:
<dl>
<dt>*-a* https://api.{DomainName}</dt>
<dd>A URL do terminal da API do
{{site.data.keyword.Bluemix_notm}}. Esse parâmetro é opcional.</dd>
<dt>*-u*user_name</dt>
<dd>Seu nome de usuário. Esse parâmetro é opcional.</dd>
<dt>*-p*password</dt>
<dd>Sua senha.</dd>
<dd>*Importante:* Se você fornecer sua senha usando o parâmetro *-p* na interface de linha de comandos, a senha poderá ser registrada no histórico da linha de comandos. Por motivos de segurança, evite fornecer a senha usando o parâmetro -p. Em vez disso,
insira a senha quando a interface da linha de comandos solicitar.</dd>
<dt>*-o*organization_name</dt>
<dd>O nome da organização na qual você deseja efetuar login.</dd>
<dt>*-s*space_name</dt>
<dd>O nome do espaço no qual você deseja efetuar login.</dd>
<dt>*--skip-ssl-validation*</dt>
<dd>Desativa o processo de validação SSL. O uso desse parâmetro pode causar problemas de segurança.</dd>
</dl>

*Nota:* Se você fornecer a sua senha no parâmetro *-p* desse comando, sua senha poderá ser registrada no arquivo histórico do comando shell e poderá ser visível para outros usuários do sistema operacional local.


## cf logs

Exibe os fluxos de log STDOUT e STDERR de um aplicativo.
```
cf logs appname
```
<dl>
<dt>appname</dt>
<dd>O nome do aplicativo.</dd>
<dt>*--recent*</dt>
<dd>Recupera logs recentes.</dd>
</dl>

## cf marketplace

Lista todos os serviços que estão disponíveis no mercado. Os serviços listados por esse comando também são mostrados no Catálogo do {{site.data.keyword.Bluemix_notm}}.
```
cf marketplace
```

## cf push

Implementa um novo aplicativo no Bluemix ou atualiza um aplicativo existente no Bluemix.
```
cf push appname 
```
<dl>
<dt>appname</dt>
<dd>O nome do aplicativo.</dd>
<dt>*-b*buildpack_name</dt>
<dd>O nome do buildpack. O buildpack_name pode ser um buildpack customizado por nome ou uma URL Git, por exemplo, `my-buildpack` ou
`https://github.com/heroku/heroku-buildpack-play.git`.</dd>
<dt>*-c*start_command</dt>
<dd>O comando start do seu aplicativo. Para usar o comando inicial padrão, especifique um valor de null para essa opção. Por
exemplo:</dd>
<dd>```
cf push appname -c null
```</dd>
<dd>Também
é possível usar esta opção para executar arquivos de script. Por exemplo:
```
cf push appname -c “bash ./<run.sh>"
```</dd>
<dt>*-f* manifest_path</dt>
<dd>O caminho do arquivo de manifesto. O arquivo manifest padrão é manifest.yml sob o diretório-raiz de seu aplicativo.</dd>
<dt>*-i*instance_number</dt>
<dd>O número de instâncias.</dd>
<dt>*-k*disk_limit</dt>
<dd>O limite de disco para o aplicativo, por exemplo, *256M*, *1024M*
oi *1G*.</dd>
<dt>*-m*memory_limit</dt>
<dd>O limite de memória para o aplicativo, por exemplo, *256M*, *1024M*
ou *1G*.</dd>
<dt>*-n*host_name</dt>
<dd>O nome do host para o aplicativo, por exemplo, *my-subdomain*.</dd>
<dt>*-p*app_path</dt>
<dd>O caminho para o diretório do aplicativo ou o archive do aplicativo</dd>
<dt>*-t*timeout</dt>
<dd>Tempo máximo, em segundos, para o aplicativo iniciar. Outros tempos-limite do lado do servidor podem substituir esse
valor.</dd>
<dt>*-s* stackname</dt>
<dd>A pilha para executar os apps. Uma pilha é um sistema de arquivos pré-construído que inclui o sistema operacional. Use `cf stacks` para visualizar as pilhas disponíveis no {{site.data.keyword.Bluemix_notm}}.</dd>
<dt>*--no-hostname*</dt>
<dd>Mapeia o domínio do sistema do Bluemix para esse aplicativo.</dd>
<dt>*--no-manifest*</dt>
<dd>Ignora o arquivo de manifesto padrão.</dd>
<dt>*--no-route*</dt>
<dd>Não mapeia uma rota para esse aplicativo.</dd>
<dt>*--no-start*</dt>
<dd>Não inicia o aplicativo após sua implementação.</dd>
<dt>*--random-route*</dt>
<dd>Cria uma rota aleatória para o aplicativo.</dd>
</dl>

## cf scale

Exibe ou muda o número da instância, o limite de espaço em disco e o limite de memória para um aplicativo.
```
cf scale appname -i instance_number -k disk_limit -m memory_limit
```
<dl>
<dt>appname</dt>
<dd>O nome do aplicativo.</dd>
<dt>*-i*instance_number</dt>
<dd>O número de instâncias</dd>
<dt>*-k*disk_limit</dt>
<dd>O limite de disco para o aplicativo, por exemplo, *256M*, *1024M*
oi *1G*.</dd>
<dt>*-m*memory_limit</dt>
<dd>O limite de memória para o aplicativo, por exemplo, *256M*, *1024M*
ou *1G*.</dd>
<dt>*-f*</dt>
<dd>Força o aplicativo a reiniciar sem prompt.</dd>
</dl>

## cf services

Lista todos os serviços que estão disponíveis no espaço
atual.
```
cf services
```

## cf set-env

Configura uma variável de ambiente para um aplicativo.
```
cf set-env appname var_name var_value
```
<dl>
<dt>appname</dt>
<dd>O nome do aplicativo.</dd>
<dt>var_name</dt>
<dd>O nome da variável de ambiente.</dd>
<dt>var_value</dt>
<dd>O valor da variável de ambiente.</dd>
</dl>

## cf stacks

Lista todas as
pilhas. Uma pilha é um sistema de arquivos pré-construído, incluindo um
sistema operacional que pode executar apps.
```
cf stacks
```

## cf stop

Para um aplicativo.
```
cf stop appname
```
<dl>
<dt>appname</dt>
<dd>O nome do aplicativo.</dd>
</dl>

## cf -v

Exibe a versão da interface da linha de comandos do cf.
```
cf -v
```

# rellinks
{: #rellinks}
## general 
{: #general}
* [Cartão de referência rápida - comandos cf](ftp://public.dhe.ibm.com/cloud/bluemix/cli_reference_card.pdf)
