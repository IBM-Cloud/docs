---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-10"

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}





# Resolução de problemas para gerenciar aplicativos
{: #managingapps}


Problemas gerais com o gerenciamento de apps podem incluir apps que não podem ser atualizados ou caracteres de byte duplo que não são exibidos. Em muitos casos, é possível recuperar-se desses problemas seguindo algumas etapas simples.
{:shortdesc}


## Você possui mudanças não salvas
{: #ts_unsaved_changes}

Ao navegar na página de detalhes do app, talvez não seja possível executar quaisquer ações e você pode ser solicitado a salvar as mudanças para que possa continuar.

Ao tentar verificar seu app ou serviços na página de detalhes do app, você continua obtendo a mensagem de erro a seguir:
{: tsSymptoms}

`Você possui mudanças não salvas na página app_name. Salve ou cancele as mudanças.`

Ao rolar o seu mouse sobre o campo **INSTÂNCIAS** ou **COTA DE MEMÓRIA** na área de janela de tempo de execução, os valores mudam. Esse comportamento é por design; no entanto, a mensagem de erro solicita que você salve a memória ou as configurações da instância antes de navegar para fora da página.
{: tsCauses}

Feche a janela da mensagem e, em seguida, clique no botão **RECONFIGURAR** na área de janela de tempo de execução.
{: tsResolve}

## O failover automático entre regiões do Bluemix não está disponível
{: #ts_failover}

Não é possível usar failover automático entre regiões do {{site.data.keyword.Bluemix_notm}}. No entanto, é possível usar um provedor de DNS que suporte failover entre vários
endereços IP como solução alternativa.

Quando um região do {{site.data.keyword.Bluemix_notm}} se torna indisponível, os apps em execução nessa região também ficam indisponíveis, ainda que os mesmos apps estejam em execução em outra região do {{site.data.keyword.Bluemix_notm}}.
{: tsSymptoms}

O {{site.data.keyword.Bluemix_notm}} ainda não fornece failover automático de uma região para outra.
{: tsCauses}

É possível usar um provedor de DNS que suporte failover inteligente entre vários endereços de IDs e configurar manualmente as definições de DNS para ativar o failover automático entre regiões do {{site.data.keyword.Bluemix_notm}}. Os provedores de DNS com essa capacidade incluem NSONE, Akamai, Dyn.
{: tsResolve}

Ao configurar suas definições de DNS, deve-se especificar os endereços IP públicos das regiões do {{site.data.keyword.Bluemix_notm}} em que seu apps estão em execução. Para obter o endereço IP público
de uma região do {{site.data.keyword.Bluemix_notm}},
use o comando `nslookup`. Por exemplo, é possível
digitar o comando a seguir em uma janela de linha de comandos:
```
nslookup stage1.mybluemix.net
```

## Impossível alternar apps para o modo de depuração
{: #ts_debug}

Você poderá não ser capaz de ativar o modo de depuração se a versão da Java virtual machine (JVM) for 8 ou inferior.

Depois que você seleciona **Ativar depuração de aplicativo**, as ferramentas tentam alternar o app para o modo de depuração. Em seguida, o ambiente de trabalho Eclipse inicia uma sessão de depuração. Quando as ferramentas ativam o modo de depuração com êxito, o status do aplicativo da web exibe `Atualizando modo`, `Desenvolvendo` e `Depurando`.
{: tsSymptoms}

No entanto, quando as ferramentas falham ao ativar o modo de depuração, o status do aplicativo da web exibe somente `Atualizando modo` e `Desenvolvendo` e não exibe `Depurando`. As ferramentas também podem exibir a mensagem de erro a seguir na visualização de Console:

```
bluemixMgmgClient - ???? [pool-1-thread-1] .... ERRO --- ClientProxyImpl: Não é possível criar a conexões de websocket para MyWebProj
com.ibm.ws.cloudoe.management.client.exception.ApplicationManagementException: javax.websocket.DeploymentException: A solicitação de HTTP para iniciar a conexão de WebSocket falhou
em com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:161)
em com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl$RunServerTask.run(ClientProxyImpl.java:267)
em java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:522)
em java.util.concurrent.FutureTask.run(FutureTask.java:277)
em java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1153)
em java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
em java.lang.Thread.run(Thread.java:785)
Causado por: javax.websocket.DeploymentException: A solicitação de HTTP para iniciar a conexão de WebSocket falhou
em org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:315)
em com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:158)
... 6 mais
Causado por: java.util.concurrent.TimeoutException
em org.apache.tomcat.websocket.AsyncChannelWrapperSecure$WrapperFuture.get(AsyncChannelWrapperSecure.java:505)
em org.apache.tomcat.websocket.WsWebSocketContainer.processResponse(WsWebSocketContainer.java:542)
em org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:296)
... 7 mais
[2016-01-15 13:33:51.075] bluemixMgmgClient - ????  [pool-1-thread-1] .... ERRO --- ClientProxyImpl: Não é possível criar a conexões de websocket para MyWebProj
com.ibm.ws.cloudoe.management.client.exception.ApplicationManagementException: javax.websocket.DeploymentException: A solicitação de HTTP para iniciar a conexão de WebSocket falhou
em com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:161)
em com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl$RunServerTask.run(ClientProxyImpl.java:267)
em java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:522)
em java.util.concurrent.FutureTask.run(FutureTask.java:277)
em java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1153)
em java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
em java.lang.Thread.run(Thread.java:785)
Causado por: javax.websocket.DeploymentException: A solicitação de HTTP para iniciar a conexão de WebSocket falhou
em org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:315)
em com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:158)
... 6 mais
Causado por: java.util.concurrent.TimeoutException
em org.apache.tomcat.websocket.AsyncChannelWrapperSecure$WrapperFuture.get(AsyncChannelWrapperSecure.java:505)
em org.apache.tomcat.websocket.WsWebSocketContainer.processResponse(WsWebSocketContainer.java:542)
em org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:296)
... 7 mais
```

As versões da Java virtual machine (JVM) a seguir não podem estabelecer uma sessão de depuração: IBM JVM 7, IBM JVM 8 e versões anteriores do Oracle JVM 8.
{: tsCauses}

Se a sua JVM do ambiente de trabalho for uma dessas versões, você poderá ter problemas ao criar uma sessão de depuração. Sua JVM de ambiente de trabalho é geralmente a JVM do sistema de seu computador local. Sua JVM do sistema não é a mesma que a JVM de seu aplicativo Java&trade; do {{site.data.keyword.Bluemix_notm}} em execução. O aplicativo Java do {{site.data.keyword.Bluemix_notm}} quase sempre é executado no IBM JVM e, às vezes, no OpenJDK JVM.

Para verificar a versão de Java que o {{site.data.keyword.eclipsetoolsfull}} executa, conclua as etapas a seguir:
{: tsResolve}

  1. No IBM Eclipse Tools for Bluemix, selecione **Ajuda** > **Sobre o Eclipse** > **Detalhes da instalação** > **Configuração**.
  2. Localize a propriedade `eclipse.vm` na lista. A linha a seguir é um exemplo de uma propriedade `eclipse.vm`:

	```
	eclipse.vm=C:\Program Files\IBM\ibm-java-sdk-80-win-x86_64\bin\..\jre\bin\j9vm\jvm.dll
	```

  3. Na linha de comandos, insira `java -version` a partir do diretório `bin` de sua instalação do Java. Suas informações da versão do IBM JVM são exibidas.

Se a sua JVM de ambiente de trabalho for IBM JVM 7 ou 8, ou uma versão anterior do Oracle JVM 8, conclua as etapas a seguir para alternar para o Oracle JVM 8:

  1. Faça download e, em seguida, instale o Oracle JVM 8; veja [Downloads do Java SE ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](http://www.oracle.com/technetwork/java/javase/downloads/index.html){: new_window} para obter detalhes.
  2. Reinicie o Eclipse.
  3. Verifique se a propriedade `eclipse.vm` aponta para sua nova instalação do Oracle JVM 8.


## Não é possível reutilizar nomes de apps excluídos
{: #ts_reuse_appname}

Depois de excluir um app, é possível reutilizar o nome do app somente depois de excluir a rota do app.

Quando você tentar reutilizar o nome do app, receberá a mensagem a seguir:
{: tsSymptoms}

`O nome já é usado por outro app.`

Quando um app é excluído, sua rota, que é a URL do app, não é automaticamente excluída. Portanto, não está disponível para reutilização. Deve-se acessar o espaço em que o app foi criado para excluir a rota para que ele possa ser reutilizado.
{: tsCauses}

Conclua as etapas a seguir para excluir a rota não usada:
{: tsResolve}

  1. Verifique se a rota pertence ao espaço atual inserindo o comando a seguir:
     ```
	 cf routes
	 ```
  2. Se a rota não pertencer ao espaço atual, alterne para o espaço ou a organização à qual ela pertence inserindo o comando a seguir:
     ```
	 cf target -o org_name -s space_name
	 ```
  3. Exclua a rota do app inserindo o comando a seguir:
     ```
	 cf delete-route domain_name -n host_name
	 ```
	 Por
exemplo:
	 ```
	 cf delete-route mybluemix.net -n app001
	 ```

## Não é possível recuperar espaços na organização
{: #ts_retrieve_space}

Não será possível criar um app ou um serviço se a sua organização atual não tiver um espaço associado a ela.

Ao tentar criar um aplicativo no Bluemix, você vê a mensagem de erro a seguir:
{: tsSymptoms}

`BXNUI0515E: os espaços na organização não foram recuperados. Ou ocorreu um problema de conexão de rede ou sua organização atual não possui um espaço associado a ela.`

Esse erro geralmente ocorre na primeira vez que você tenta criar um app ou um serviço por meio do Catálogo quando um espaço ainda não foi criado.
{: tsCauses}

Certifique-se de que você criou um espaço em sua organização atual. Para criar um espaço, use um dos métodos a seguir:
{: tsResolve}

  * Na barra de menus, clique em **Gerenciar > Conta > Organizações**. Selecione a organização em que você deseja criar o espaço e clique em **Criar um espaço**.
  * Na interface de linha de comandos cf, digite `cf create-space <space_name> -o <organization_name>`.

Tente novamente. Se essa mensagem ocorrer novamente, acesse a página [Status do Bluemix ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](http://ibm.biz/bluemixstatus){: new_window} para verificar se um serviço ou um componente tem um problema.


## Não é possível executar as ações solicitadas
{: #ts_authority}

Pode ser que você não consiga concluir as ações sem autoridade de acesso apropriada.

Ao tentar executar ações para uma instância de serviço ou uma instância de app, não é possível concluir as ações solicitadas e ver uma das mensagens de erro a seguir:
{: tsSymptoms}

`BXNUI0514E: você não é um desenvolvedor para nenhum dos espaços na organização <orgName>.`

`Erro do servidor, código de status: 403, código de erro: 10003, mensagem: você não tem autorização para executar a ação solicitada.`

Você não possui o nível apropriado de autoridade para executar as ações.
{: tsCauses}

Para obter o nível de autoridade apropriado, use um dos métodos a seguir:
{: tsResolve}
 * Selecione outra organização e outro espaço para os quais tenha a função de desenvolvedor.
 * Peça ao gerenciador de organização para mudar sua função para desenvolvedor ou para criar um espaço e, em seguida, designar a função de desenvolvedor a você. Veja [Gerenciando organizações e espaços](/docs/admin/orgs_spaces.html) para obter detalhes.

## Não é possível acessar serviços do Bluemix devido a erros de autorização
{: #ts_vcap}

Poderão ocorrer erros de autorização quando seu app acessar um serviço {{site.data.keyword.Bluemix_notm}} se as credenciais de serviço estiverem codificadas permanentemente no app.

Depois de configurar seu app para se comunicar com um serviço {{site.data.keyword.Bluemix_notm}}, você implementará o app no {{site.data.keyword.Bluemix_notm}}. No entanto, não é possível usar o app para acessar o serviço {{site.data.keyword.Bluemix_notm}} e receber um erro de autorização.
{: tsSymptoms}

As credenciais codificadas permanentemente no app podem não estar corretas. Toda vez que o serviço for recriado, as credenciais para acessá-lo mudarão.
{: tsCauses}

Em vez de codificar permanentemente as credenciais no app, use parâmetros de conexão a partir da variável de ambiente VCAP_SERVICES. Os métodos para usar parâmetros de conexão a partir da variável de ambiente VCAP_SERVICES variam, dependendo das linguagens do programa. Por exemplo, para apps Node.js, é possível usar o comando a seguir:
{: tsResolve}

```
process.env.VCAP_SERVICES
```
Para obter mais informações sobre os comandos que podem ser usados em outras linguagens de programa, veja [Java ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](http://docs.run.pivotal.io/buildpacks/java/java-tips.html#env-var){: new_window} e [Ruby ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](http://docs.run.pivotal.io/buildpacks/ruby/ruby-tips.html#env-var){: new_window}.


## Não é possível implementar apps usando o IBM Eclipse Tools for Bluemix
{: #ts_bm_tools_facet}

Quando uma máscara não suportada é aplicada ao projeto Eclipse, talvez você não consiga implementar os apps no {{site.data.keyword.Bluemix_notm}} usando o IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}.

É possível implementar com sucesso seu app no {{site.data.keyword.Bluemix_notm}} usando a CLI do Cloud Foundry. No entanto, não é possível implementar o app no {{site.data.keyword.Bluemix_notm}} usando o IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} e você vê a mensagem de erro: `A máscara de projeto <facet_name> não é suportada.` Por exemplo:
{: tsSymptoms}
`A máscara de projeto Cloud Foundry Standalone Application versão 1.0 não é suportada.`

O IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} mapeia projetos para tempos de execução do {{site.data.keyword.Bluemix_notm}} por máscaras de projeto. As máscaras definem os requisitos para projetos Java EE no Eclipse e são usadas como parte da configuração de tempo de execução para que diferentes tempos de execução sejam associados a diferentes projetos. Caso a máscara aplicada ao projeto não seja suportada pelo IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}, talvez não seja possível implementar o app usando o IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}.
{: tsCauses}

Deve-se remover a máscara do projeto Eclipse para que seja possível implementar seu app usando o IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}.
{: tsResolve}

Para remover a máscara, no IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}, clique em **Projeto>Propriedades>Máscaras de projeto** para o projeto. Em seguida, limpe a caixa de seleção para a máscara não suportada.


## Erros 502 Gateway inválido são recebidos
{: #ts_502_error}

Se você receber os erros 502 Gateway inválido ao interagir com apps no {{site.data.keyword.Bluemix_notm}}, verifique a página de status do {{site.data.keyword.Bluemix_notm}} e, em seguida, execute as ações apropriadas.

Você recebe mensagens de erro que iniciam com 502 Gateway inválido. Por exemplo, você pode ver `502 Gateway inválido: o terminal registrado falhou em manipular a solicitação.`
{: tsSymptoms}

Um erro de Gateway inválido geralmente acontece quando você visita um website que usa um servidor proxy para armazenar e retransmitir os dados do servidor principal que hospeda o site. O servidor principal e o servidor proxy podem não estar conectados corretamente, portanto, você vê o código de status 502 do HTTP na janela do navegador. Esse código de status indica que o servidor principal do site não recebeu a implementação HTTP esperada do servidor proxy.
{: tsCauses}

Outras causas menos comuns de um erro de Gateway inválido são os dropouts do provedor de serviços da Internet (ISP), configurações de firewall inválidas e erros de cache do navegador.

Se você suspeitar que um serviço {{site.data.keyword.Bluemix_notm}} está inativo, verifique primeiramente a página [Status do {{site.data.keyword.Bluemix_notm}}![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](http://ibm.biz/bluemixstatus){: new_window}. Uma solução alternativa poderia ser usar o serviço em outra região do {{site.data.keyword.Bluemix_notm}}. As informações detalhadas estão disponíveis em [Usando serviços em outra região ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](/docs/services/reqnsi.html#cross_region_service){: new_window}. Se o status de serviço for normal, tente as etapas a seguir para resolver o problema:
{: tsResolve}

  * Tente novamente a ação:
    * Recarregar a página pressionando F5 em seu teclado ou clicando no botão de atualização. Se essa etapa não funcionar, limpe o cache e os cookies de seu navegador e, em seguida, recarregue novamente.
    * Usar um navegador diferente.
    * Reinicializar seu roteador, seu modem e seu computador. Reinicializar esses dispositivos pode limpar diversos erros que conduzem ao erro 502.
  * Aguardar e tentar novamente mais tarde. Em algumas instâncias, os problemas temporários podem ocorrer com seu provedor de serviços da Internet ou serviços do {{site.data.keyword.Bluemix_notm}}. É possível aguardar até que os problemas temporários sejam resolvidos.
  * Se o problema ainda existir, entre em contato com o suporte do {{site.data.keyword.Bluemix_notm}}. Veja [Entrando em contato com o Suporte do {{site.data.keyword.Bluemix_notm}} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](/docs/support/index.html#contacting-bluemix-support){: new_window} para obter mais informações.

## Cota do disco excedida
{: #ts_disk_quota}

Se o espaço em disco se esgotar, será possível modificar manualmente a cota do disco para obter mais espaço em disco.

Quando o espaço em disco se esgotar, você poderá ver uma mensagem que indica se a cota do disco foi excedida. Para resolver o problema, você pode ter tentado aumentar a escala de sua instância de app para obter mais espaço em disco. Por exemplo, você pode escalar de 256 MB para 1256 MB, mudando a cota de memória na página de detalhes do app. No entanto, como a cota do disco permaneceu a mesma, você não obteve mais espaço em disco.
{: tsSymptoms}

A cota padrão do disco que é alocada para um app é de 1 GB. Se você precisar de mais espaço em disco, deve especificar manualmente a cota do disco.
{: tsCauses}

Use um dos métodos a seguir para especificar sua cota do disco. A cota máxima de disco que você pode especificar é de 2 GB. Se 2 GB ainda não forem suficientes, tente um serviço externo como
[Armazenamento de objetos](/docs/services/ObjectStorage/index.html).
{: tsResolve}

  * No arquivo manifest.yml, inclua o item a seguir:
    ```
	disk_quota: <disk_quota>
	```
  * Use a opção **-k** com o comando `cf push` quando enviar por push seu app para {{site.data.keyword.Bluemix_notm}}:
    ```
	cf push appname -p app_path -k <disk_quota>
	```


## Apps Android não podem receber {{site.data.keyword.mobilepushshort}}
{: #ts_push}

Os apps Android em certas regiões em que o Google não está acessível não podem receber as notificações que você envia por meio do serviço IBM {{site.data.keyword.mobilepushshort}}. Nesse caso, uma solução alternativa é usar serviços de terceiros.

Você liga um serviço {{site.data.keyword.mobilepushshort}} ao seu app Bluemix e envia uma mensagem aos dispositivos registrados. No entanto, os apps que são desenvolvidos na plataforma Android não podem receber suas notificações em certas regiões.
{: tsSymptoms}

O serviço IBM {{site.data.keyword.mobilepushshort}} usa o serviço Google Cloud Messaging (GCM) para despachar notificações para apps móveis que são desenvolvidos na plataforma Android. Para ativar o recebimento de notificações em apps Android, o serviço Google Cloud Messaging (GCM) deve estar acessível para apps móveis. Em regiões em que os apps Android não puderem acessar o serviço GCM, os apps Android não poderão receber {{site.data.keyword.mobilepushshort}}.
{: tsCauses}

Como solução alternativa, use serviços de terceiros que não dependam do serviço GCM, por exemplo, [Pushy ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://pushy.me){: new_window}, [igetui ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](http://www.getui.com/){: new_window} e [jpush ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://www.jpush.cn/){: new_window}.
{: tsResolve}


## O limite de serviços da organização foi excedido
{: #ts_servicelimit}

Se você for um usuário da conta para teste, talvez não possa criar um app no {{site.data.keyword.Bluemix_notm}} se tiver excedido seu limite de serviços da organização.

Ao tentar criar um app no {{site.data.keyword.Bluemix_notm}}, você vê a mensagem de erro a seguir:
{: tsSymptoms}

`BXNUI2032E: O recurso <service_instances> não foi criado. Ocorreu um erro enquanto o Cloud Foundry estava sendo contatado para criar o recurso. Mensagem do Cloud Foundry: "Você excedeu seu limite de serviços da organização."`

Esse erro ocorre quando você excede o limite no número de instâncias de serviços que pode ter para sua conta. O número máximo de instâncias de serviços para uma conta para teste é 10.
{: tsCauses}

Exclua todas as instâncias de serviços que não forem necessárias ou remova o limite no número de instâncias de serviço que você pode ter.
{: tsResolve}

  * Para excluir uma instância de serviços, é possível usar o console do {{site.data.keyword.Bluemix_notm}} ou a interface da linha de comandos.

    Para usar o console do {{site.data.keyword.Bluemix_notm}} para excluir uma instância de serviço, conclua as etapas a seguir:
	  1. No painel Serviços, clique no menu **Ações** para o serviço que você deseja excluir.
	  2. Clique em **Excluir serviço**. Você será então solicitado a remontar o app ao qual a instância de serviço foi ligada.

    Para usar a interface de linha de comandos para excluir uma instância de serviço, conclua as etapas a seguir:
	  1. Desvincule a instância de serviço de um app digitando `cf unbind-service <appname> <service_instance_name>`.
	  2. Exclua a instância de serviço digitando `cf delete-service <service_instance_name>`.
	  3. Depois de excluir a instância de serviço, você talvez deseje remontar o app ao qual a instância de serviço foi ligada digitando `cf restage <appname>`.

  * Para remover o limite no número de instâncias de serviços que você pode ter, converta sua conta de avaliação em uma conta paga. Para obter informações sobre como converter sua conta para teste para uma conta paga, veja [Como mudar seu plano](/docs/pricing/index.html#changing).

## Os executáveis não podem ser executados no Bluemix
{: #ts_executable}

Talvez você não possa executar os executáveis no {{site.data.keyword.Bluemix_notm}} quando eles forem desenvolvidos e construídos em um ambiente diferente.

Não será possível executar executáveis no {{site.data.keyword.Bluemix_notm}} quando eles tiverem sido desenvolvidos e construídos em um ambiente diferente.
{: tsSymptoms}

Se o conteúdo que você deseja enviar por push para o {{site.data.keyword.Bluemix_notm}} já for um executável, o conteúdo foi construído anteriormente e não precisa ser construído no {{site.data.keyword.Bluemix_notm}}. Nesse caso, nenhum buildpack é necessário para o executável ser executado no {{site.data.keyword.Bluemix_notm}}. No entanto, você deve indicar explicitamente ao {{site.data.keyword.Bluemix_notm}} que nenhum buildpack é necessário.
{: tsCauses}

Ao enviar por push o executável para o {{site.data.keyword.Bluemix_notm}}, deve-se especificar um buildpack nulo, o qual indica que nenhum buildpack é necessário. Especifique um buildpack nulo usando a opção **-b** com o comando `cf push`:
{: tsResolve}

```
cf push appname -p app_path -c <start_command> -b <null-buildpack>
```
Por exemplo:
```
cf push appname -p app_path -c ./RunMeNow -b https://github.com/ryandotsmith/null-buildpack
```

## O limite de memória da organização foi excedido
{: #ts_outofmemory}

Se você for um usuário de conta para teste, talvez não consiga implementar um app no {{site.data.keyword.Bluemix_notm}} caso tenha excedido o limite de memória da sua organização. É possível reduzir a memória que seus apps usam ou aumentar a cota de memória de sua conta. A cota máxima de memória de uma conta para teste é 2 GB e pode ser aumentada somente movendo para uma conta paga.

Ao implementar um app no {{site.data.keyword.Bluemix_notm}}, você vê a mensagem de erro a seguir:
{: tsSymptoms}

`Erro de Servidor COM FALHA, código de status: 400, código de erro: 100005, mensagem: Você excedeu seu limite de memória da organização.`

Esse erro ocorre quando a quantia de memória restante para a sua organização é menor que a quantia de memória requerida pelo aplicativo que você deseja implementar. A cota máxima de memória para uma conta de avaliação é 2 GB.
{: tsCauses}

É possível aumentar a cota de memória de sua conta ou reduzir a memória que seus apps usam.
{: tsResolve}

  * Para aumentar a cota de memória de sua conta, converta sua conta de avaliação em uma conta paga. Para obter informações sobre como converter sua conta para teste para uma conta paga, veja [Contas pagas](/docs/pricing/index.html#pay-accounts).
  * Para reduzir a memória que seus apps usam, use o console do {{site.data.keyword.Bluemix_notm}} ou a interface da linha de comandos cf.

    Se você usar o console do {{site.data.keyword.Bluemix_notm}}, conclua as etapas a seguir:

    1. No Painel Apps, selecione seu app. A página de detalhes do app é aberta.
    2. Na área de janela de tempo de execução, é possível reduzir o limite máximo de memória ou os números de instâncias do app, ou ambos, para seu app.

    Se você usar a interface de linha de comandos cf, conclua as seguintes etapas:

    1. Verifique quanta memória está sendo usada para seus apps:

	  ```
	  cf apps
	  ```

	  O comando cf apps lista todos os aplicativos que você implementou no espaço atual. O status de cada app também é exibido.

    2. Para reduzir a quantia de memória que é usada por seu app, reduza o número de instâncias do app ou o limite máximo de memória, ou ambos:

	  ```
	  cf push appname -p app_path -i instance_number -m memory_limit
      ```

    3. Reinicie seu app para que as mudanças entrem em vigor.


## Os apps não são reiniciados automaticamente
{: #ts_apps_not_auto_restarted}

Um app não é reiniciado automaticamente quando um serviço que você liga ao app para de funcionar.	  

Quando um serviço que você liga a um app trava, problemas como indisponibilidades, exceções e falhas na conexão pode ocorrer no app. O {{site.data.keyword.Bluemix_notm}} não reinicia automaticamente o app para recuperar desses problemas.
{: tsSymptoms}

Esse comportamento é de acordo com o design do Cloud Foundry.
{: tsCauses}

É possível reiniciar manualmente o app digitando o comando a seguir na interface de linha de comandos:
{: tsResolve}

```
cf push appname -p app_path
```
Além disso, é possível codificar o app para identificar e recuperar de problemas como indisponibilidades, exceções e falhas na conexão.

## As variáveis definidas pelo usuário são perdidas quando um app é enviado por push
{: #ts_varsnotretained}

Ao enviar por push um app para o {{site.data.keyword.Bluemix_notm}} a partir do IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}, as variáveis especificadas são reconfiguradas a menos que você salve as salve no arquivo manifest.

As variáveis especificadas são perdidas depois que você envia por push um app para o {{site.data.keyword.Bluemix_notm}} a partir do IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}.
{: tsSymptoms}

As variáveis que você especificou são salvas somente se salvá-las para o arquivo manifest.
{: tsCauses}

Ao enviar por push um app para o {{site.data.keyword.Bluemix_notm}} a partir do IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}, selecione a caixa de seleção **Salvar no arquivo manifest** na página de detalhes do Aplicativo do assistente do Aplicativo. Em seguida, as variáveis que você especificou no assistente são salvas para o arquivo manifest de seu aplicativo. Na próxima vez em que abrir o assistente, as variáveis serão exibidas automaticamente.
{: tsResolve}

<!-- begin STAGING ONLY -->

## O Bluemix Live Sync Debug não é iniciado na linha de comandos
{: #ts_no_debug}

Você ativou o recurso IBM Bluemix Live Sync Debug para seu app usando a linha de comandos, mas não é possível acessar a interface de Depuração.  

Você ativou o recurso de depuração para seu aplicativo configurando a variável de
ambiente **BLUEMIX_APP_MGMT_ENABLE**. No entanto, não é possível acessar a interface com o usuário de Depuração em `app_url/bluemix-debug/manage`.
{: tsSymptoms}

O recurso de Depuração não pode ser ativado nestas situações:
{: tsCauses}

  * Quando o `manifest` contém o atributo de comando
  * Quando você usa a opção **-c** para enviar por push um app
para o {{site.data.keyword.Bluemix_notm}}

Use uma das opções a seguir para resolver o problema:
{: tsResolve}

  * A prática recomendada é usar o buildpack IBM Node.js para iniciar o app. Para obter mais informações, consulte a seção Comando de inicialização do tópico [Implementando um aplicativo Node.js no {{site.data.keyword.Bluemix_notm}}](/docs/runtimes/nodejs/index.html#nodejs_runtime).
  * Desative o comando para seu app existente revisando o atributo de
comando no `manifest.yml` para o comando: null ou editando seu
comando push para incluir `-c Null`.
  * Remova o atributo de **comando** do `manifest.yml`. Em
seguida, exclua o app atual do {{site.data.keyword.Bluemix_notm}} e envie por
push o app novamente.

<!-- end STAGING ONLY -->  


## As organizações não podem ser localizadas no Bluemix
{: #ts_orgs}

Talvez você não consiga localizar sua organização no {{site.data.keyword.Bluemix_notm}} ao trabalhar em uma região {{site.data.keyword.Bluemix_notm}}.

É possível efetuar login com sucesso no console do {{site.data.keyword.Bluemix_notm}}, mas não é possível enviar os apps por push usando a interface da linha de comandos cf ou o plug-in do Eclipse.
{: tsSymptoms}

Ao tentar enviar por push um aplicativo
para o {{site.data.keyword.Bluemix_notm}}
usando a interface de linha de comandos cf, você vê uma das mensagens de erro
a seguir com o nome da organização especificado na mensagem:

`Erro ao localizar a org.`

`Organização não localizada`

Ao tentar
enviar por push um aplicativo para o {{site.data.keyword.Bluemix_notm}}
usando o Cloud Foundry Eclipse Plugin, você vê a mensagem de erro
a seguir:

`Cloudspace não localizado.`

Esse problema ocorre porque o terminal de API da região com a qual você deseja trabalhar não está especificado e a organização que está sendo procurada pode estar em uma região diferente.
{: tsCauses}

Se você estiver enviando por push seu aplicativo para o {{site.data.keyword.Bluemix_notm}} usando a interface de linha de comandos cf, insira o comando cf api e especifique o terminal de API da região. Por exemplo, insira o comando a seguir para se conectar à região da Europa, Reino Unido, do {{site.data.keyword.Bluemix_notm}}:
{: tsResolve}

```
cf api https://api.eu-gb.bluemix.net
```
Se
você estiver enviando por push seu aplicativo para {{site.data.keyword.Bluemix_notm}}, usando as ferramentas
Eclipse, primeiro deve criar um servidor {{site.data.keyword.Bluemix_notm}} e especificar o terminal da
API da região {{site.data.keyword.Bluemix_notm}} em que foi criada a sua organização. Para obter informações adicionais
sobre como usar as ferramentas do Eclipse, consulte [Implementando apps com o IBM Eclipse Tools for Bluemix](/docs/manageapps/eclipsetools/eclipsetools.html).  

## As rotas do app não podem ser criadas
{: #ts_hostistaken}

Ao implementar um app no {{site.data.keyword.Bluemix_notm}}, a rota do app não pode ser criada se o nome do host especificado já estiver sendo usado.

Ao implementar um app no {{site.data.keyword.Bluemix_notm}}, você vê a mensagem de erro a seguir:
{: tsSymptoms}

`Criando a rota hostname.domainname ... Erro de servidor COM FALHA, código de status: 400, código de erro: 210003, mensagem: O host foi tomado: hostname`

Esse problema ocorre se o nome do host especificado
já estiver sendo usado.
{: tsCauses}

O nome do host especificado deve ser exclusivo no
domínio que você estiver usando. Para especificar um nome de host diferente, use um
dos métodos a seguir:
{: tsResolve}

  * Se você implementar seu aplicativo usando o arquivo `manifest.yml`, especifique o nome do host na opção host.	 
    ```
    host: host_name
	```
  * Se você implementar seu aplicativo a partir do prompt de comandos, use o comando `cf
push` com a opção **-n**.
    ```
    cf push appname -p app_path -n host_name
    ```


## Aplicativos WAR não podem ser enviados por push usando o comando cf push
{: #ts_cf_war}

Talvez não seja possível usar o comando cf push para implementar um app da web arquivado no {{site.data.keyword.Bluemix_notm}} caso o local do app não seja especificado corretamente.

Ao fazer upload de um app WAR no {{site.data.keyword.Bluemix_notm}} usando o comando `cf push`, você vê a mensagem de erro a seguir:
{: tsSymptoms}
`Erro de preparação: não é possível obter instâncias, uma vez que a preparação falhou.`

Esse problema poderá ocorrer se o arquivo WAR não for especificado ou se o caminho para o arquivo WAR não for especificado.
{: tsCauses}

Use a opção **-p** para especificar
um arquivo WAR ou inclua o caminho no arquivo WAR. Por exemplo:
{: tsResolve}

```
cf push MyUniqueAppName01 -p app.war
```

```
cf push MyUniqueAppName02 -p "./app.war"
```
Para obter mais informações
sobre o comando `cf push`, insira `cf push
     -h`. 	


## Caracteres de byte duplo não são exibidos corretamente quando os aplicativos Liberty são enviados por push ao Bluemix
{: #ts_doublebytes}

Os caracteres de byte duplo poderão não ser exibidos corretamente se o suporte Unicode não estiver configurado corretamente para os arquivos servlet ou JSP.

Quando um aplicativo Liberty é enviado por push para o {{site.data.keyword.Bluemix_notm}}, os caracteres de byte duplo especificados no app não são exibidos corretamente.
{: tsSymptoms}

O problema poderá ocorrer se o suporte Unicode não estiver configurado corretamente para os arquivos servlet ou JSP.
{: tsCauses}

É possível usar o código a seguir no arquivo servlet ou JSP:
{: tsResolve}

  * No arquivo de origem servlet
    ```
	response.setContentType("text/html; charset=UTF-8");
	```
  * No arquivo JSP
    ```
	<meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
	```


## Não é possível implementar apps Node.js
{: #ts_nodejs_deploy}

É possível encontrar problemas ao atualizar um app Node.js ou implementar um app Node.js no {{site.data.keyword.Bluemix_notm}}.

Ao atualizar um app Node.js ou implementar seu app Node.js
no {{site.data.keyword.Bluemix_notm}},
é possível ver uma das mensagens de erro a seguir:
{: tsSymptoms}

`Um app não foi detectado com êxito por nenhum buildpack disponível.`

`A instância (índice 0) falhou ao iniciar a aceitação de conexões.`

`Não é possível obter instâncias, uma vez que a preparação falhou.`

As causas possíveis são as seguintes:
{: tsCauses}

  * O comando inicial não foi especificado.
  * Os arquivos necessários para implementar um app Node.js estão ausentes no app ou estão em uma pasta diferente do diretório-raiz.

Use um dos métodos a seguir, dependendo da causa do problema:
{: tsResolve}

  * Especifique o comando inicial por um dos métodos a seguir:
     * Use a interface de linha de comandos cf. Por
exemplo:
        ```
		cf push MyUniqueNodejs01 -p app_path -c "node app.js"
		```
    * Use o arquivo [package.json ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://docs.npmjs.com/json){: new_window}. Por
exemplo:
	    ```
		{
      ...
  	   "scripts": {
	 		 "start": "node app.js"
 	   }
	}
	    ```
    * Use o arquivo `manifest.yml`. Por
exemplo:
	    ```
		applications:
  name: MyUniqueNodejs01
  ...
  command: node app.js
  ...
        ```

  * Assegure-se de que um arquivo `package.json` exista em seu app Node.js para que o buildpack Node.js possa reconhecer o app. Assegure-se de que esse arquivo esteja no diretório-raiz de seu app.
    O exemplo a seguir mostra um arquivo `package.json` simples:  
	```
	{
        "name": "MyUniqueNodejs01",
        "version": "0.0.1",
        "description": "A sample package.json file",
        "dependencies": {
                "express": "3.4.x",
                "jade": "1.1.x"
        },
        "engines": {
                "node": "0.10.x"
        },
        "scripts": {
                  "start": "node app.js"
        }
 }
    ```

Para obter mais dicas sobre apps Node.js, veja [Dicas para aplicativos Node.js](http://docs.cloudfoundry.org/buildpacks/node/node-tips.html ![External link icon](../icons/launch-glyph.svg "Ícone de link externo"){: new_window}.


## Erros de configuração aparecem no arquivo `server.xml` depois de importar um app do Liberty do Bluemix para o Eclipse
{: #ts_eclipse}

Se ocorrerem erros de configuração no arquivo `server.xml` depois de importar um app
{{site.data.keyword.Bluemix_notm}} Liberty no Eclipse, poderá ser necessário remover o arquivo
`server.xml` do projeto.

Depois de importar um app {{site.data.keyword.Bluemix_notm}} Liberty no Eclipse, ocorrerão erros
de configuração no arquivo `server.xml` na visualização Problemas do Eclipse.
{: tsSymptoms}

O buildpack do Liberty usa o arquivo `server.xml` para configurar o app e gera um arquivo `runtime-vars.xml` quando o app Liberty é enviado por push ao {{site.data.keyword.Bluemix_notm}}. Quando você importa o app para o Eclipse, o arquivo `runtime-vars.xml` não existe em seu ambiente local.
{: tsCauses}

É possível resolver esse problema removendo o arquivo server.xml do projeto. O buildpack cria o arquivo `server.xml` dinamicamente quando você envia por push o app como um app WAR. Para obter mais informações, veja [Liberty for Java](/docs/runtimes/liberty/index.html).
{: tsResolve}


## Os aplicativos não podem ser colocados em estágios usando buildpacks customizados
{: #ts_bp_compilation}

Talvez não seja possível implementar um app no {{site.data.keyword.Bluemix_notm}} usando um buildpack customizado caso os scripts no buildpack não sejam executáveis.

Ao implementar um app no {{site.data.keyword.Bluemix_notm}} usando um buildpack customizado, você vê a mensagem de erro `O aplicativo falhou na preparação, portanto, não há instâncias a serem exibidas.`
{: tsSymptoms}

Esse problema poderá ocorrer se scripts, como o script de detecção, o script de compilação e o script de liberação não forem executáveis.
{: tsCauses}

É possível usar o comando [git update ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](http://git-scm.com/docs/git-update-index){: new_window} para mudar a permissão de cada script para executável. Por exemplo, é possível digitar `git update --chmod=+x script.sh`.
{: tsResolve}

## Não é possível implementar um app do Delivery Pipeline no IBM Bluemix Continuous Delivery
 {: #ts_devops_to_bm}

 Talvez não seja possível implementar seu app usando o {{site.data.keyword.deliverypipeline}} no {{site.data.keyword.contdelivery_short}} se o arquivo `manifest.yml` não estiver presente em seu app.

 Ao implementar um app usando o {{site.data.keyword.deliverypipeline}} no {{site.data.keyword.contdelivery_short}}, uma mensagem de erro `Não é possível detectar um tipo de aplicativo suportado` poderá ser exibida.
 {: tsSymptoms}

 Esse problema pode ocorrer porque o pipeline requer um arquivo `manifest.yml` para implementar um app no {{site.data.keyword.Bluemix_notm}}.
 {: tsCauses}

 Para resolver esse problema, você deve criar um arquivo `manifest.yml`. Para obter informações adicionais sobre como criar um arquivo `manifest.yml`,
consulte [Manifest do
aplicativo](/docs/manageapps/depapps.html#appmanifest).
 {: tsResolve}

## Os apps Meteor não podem ser enviados por push
{: #ts_meteor}

Talvez não seja possível enviar um aplicativo Meteor por push para o {{site.data.keyword.Bluemix_notm}} caso o buildpack não seja especificado corretamente.

Ao implementar um app Meteor no {{site.data.keyword.Bluemix_notm}}, você pode ver a mensagem de erro `O aplicativo falhou na preparação, portanto não há instâncias a serem exibidas.`
{: tsSymptoms}

Esse problema ocorre porque nenhum buildpack integrado é fornecido para apps Meteor. Deve-se usar um buildpack customizado.
{: tsCauses}

Para usar um buildpack customizado para apps Meteor, use um dos métodos a seguir:
{: tsResolve}

  * Se você implementar seu app usando o arquivo `manifest.yml`, especifique a URL ou o nome de seu buildpack customizado usando a opção buildpack. Por
exemplo:
  ```
  buildpack: https://github.com/Sing-Li/bluemix-bp-meteor
  ```
  * Se você implementar seu aplicativo a partir do prompt de comandos, use o comando `cf
push` e especifique seu buildpack customizado usando
a opção **-b**. Por
exemplo:
    ```
	cf push appname -p app_path -b https://github.com/Sing-Li/bluemix-bp-meteor
	```
