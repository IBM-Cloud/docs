---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-01-11"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 





# Resolução de problemas para gerenciar aplicativos
{: #managingapps}


Problemas gerais com o gerenciamento de aplicativos podem incluir
aplicativos que não podem ser atualizados e caracteres de byte duplo que não são exibidos. No entanto, em vários casos, é possível recuperar-se desses
problemas seguindo algumas etapas simples.
{:shortdesc}





## Impossível alternar apps para o modo de depuração
{: #ts_debug}

Você poderá não ser capaz de ativar o modo de depuração se a versão da Java virtual machine (JVM) for 8 ou inferior. 


Depois que você seleciona **Ativar depuração de aplicativo**, as ferramentas tentam alternar o aplicativo para o modo de depuração. Em seguida, o ambiente de trabalho Eclipse inicia uma sessão de depuração. Quando as ferramentas ativam o modo de depuração com êxito, o status do aplicativo da web exibe `Atualizando modo`, `Desenvolvendo` e `Depurando`. 
{: tsSymptoms}

No entanto, quando as ferramentas falham em ativar o modo de depuração, o status do aplicativo da web exibe somente `Atualizando modo` e `Desenvolvendo` e não exibe `Depurando`. As ferramentas também podem exibir a mensagem de erro a seguir na visualização de Console:

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

Se a sua JVM de ambiente de trabalho for uma dessas versões, você poderá ter problemas ao criar uma sessão de depuração. Sua JVM de ambiente de trabalho é geralmente a JVM do sistema de seu computador local. Sua JVM do sistema não é a mesma que a JVM de seu aplicativo Java do Bluemix em execução. O aplicativo Java do Bluemix quase sempre é executado no IBM JVM e, às vezes, no OpenJDK JVM.
  

Para verificar a versão do Java que o IBM Eclipse Tools for Bluemix executa, conclua as etapas a seguir:
{: tsResolve}

  1. No IBM Eclipse Tools for Bluemix, selecione **Ajuda** > **Sobre o Eclipse** > **Detalhes da instalação** > **Configuração**.
  2. Localize a propriedade `eclipse.vm` na lista. A linha a seguir é um exemplo de uma propriedade `eclipse.vm`:
	
	```
	eclipse.vm=C:\Program Files\IBM\ibm-java-sdk-80-win-x86_64\bin\..\jre\bin\j9vm\jvm.dll
	```

  3. Na linha de comandos, insira `java -version` a partir do diretório `bin` de sua instalação do Java. Suas informações da versão do IBM JVM são exibidas.

Se a sua JVM de ambiente de trabalho for IBM JVM 7 ou 8, ou uma versão anterior do Oracle JVM 8, conclua as etapas a seguir para alternar para o Oracle JVM 8:

  1. Faça download e, em seguida, instale o Oracle JVM 8; veja [Downloads do Java SE ![Ícone de link externo](../icons/launch-glyph.svg)](http://www.oracle.com/technetwork/java/javase/downloads/index.html){: new_window} para obter detalhes.
  2. Reinicie o Eclipse.
  3. Verifique se a propriedade `eclipse.vm` aponta para sua nova instalação do Oracle JVM 8.

  
## Não é possível reutilizar nomes de aplicativos excluídos
{: #ts_reuse_appname}
  
Depois de excluir um app, é possível reutilizar o nome do app somente depois de excluir a rota do app. 

Quando você tentar reutilizar o nome do app, receberá a mensagem a seguir:
{: tsSymptoms}

`O nome já é usado por outro app.`

Quando um app é excluído, sua rota, que é a URL do app, não é automaticamente excluída. Portanto, não está disponível para reutilização. Deve-se acessar o espaço em que o app foi criado para excluir a rota para que ele possa ser reutilizado.
{: tsCauses}

Execute as etapas a seguir para excluir a rota não utilizada: 
{: tsResolve}

  1. Verifique se a rota pertence ao espaço atual inserindo o comando a seguir: 
     ```
	 cf routes
	 ```
  2. Se a rota não pertencer ao espaço atual, alterne para o espaço ou a
organização à qual ela pertence inserindo o comando a seguir: 
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
Não será possível criar um aplicativo ou um serviço se a sua organização atual não tiver um espaço associado com ela.

Ao tentar criar um aplicativo no Bluemix, você vê a mensagem de erro a seguir:
{: tsSymptoms}

`BXNUI0515E: os espaços na organização não foram recuperados. Ou ocorreu um problema de conexão de rede ou sua organização atual não possui um espaço associado a ela.`

Esse erro geralmente é recebido na primeira vez em que você tenta criar um aplicativo ou um serviço a partir do Catálogo quando um espaço ainda não estiver criado. 
{: tsCauses}

Certifique-se de que você criou um espaço em sua organização atual.  Para criar um espaço, use um dos métodos a seguir:
{: tsResolve}

  * Na barra de menus, clique em **Conta** &gt; **Gerenciar organizações.** Selecione a organização na qual deseja criar o espaço e, em seguida, clique em **Criar um espaço**.
  * Na interface de linha de comandos cf, digite `cf create-space <space_name> -o <organization_name>`.

Tente novamente. Se você vir essa mensagem novamente, acesse a página [Status do Bluemix ![Ícone de link externo](../icons/launch-glyph.svg)](http://ibm.biz/bluemixstatus){: new_window} para verificar se um serviço ou componente tem um problema.



## Não é possível executar as ações solicitadas
{: #ts_authority}

Pode ser que você não consiga concluir as ações sem autoridade de acesso apropriada.

 

Ao tentar executar ações para uma instância de serviço ou uma instância de app, não é possível concluir as ações solicitadas e ver uma das mensagens de erro a seguir: 
{: tsSymptoms}

`BXNUI0514E: você não é um desenvolvedor para nenhum dos espaços na organização <orgName>.`


`Erro do servidor, código de status: 403, código de erro: 10003, mensagem: você não tem autorização para executar a ação solicitada.`

 

Você não possui o nível apropriado de autoridade necessário para executar as ações. 
{: tsCauses}

  
Para obter o nível de autoridade apropriado, use um dos métodos a seguir: 
{: tsResolve}
 * Selecione outra organização e outro espaço para os quais tenha a função de desenvolvedor. 
 * Peça ao gerenciador de organização para mudar sua função para desenvolvedor ou para criar um espaço e, em seguida, designar a função de desenvolvedor a você. Veja [Gerenciando organizações e espaços](/docs/admin/orgs_spaces.html) para obter detalhes.
 



## Não é possível acessar serviços do {{site.data.keyword.Bluemix_notm}} em razão de erros de autorização
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
Para obter mais informações sobre os comandos que podem ser usados em outras linguagens de programa, veja [Java ![Ícone de link externo](../icons/launch-glyph.svg)](http://docs.run.pivotal.io/buildpacks/java/java-tips.html#env-var){: new_window} e [Ruby ![Ícone de link externo](../icons/launch-glyph.svg)](http://docs.run.pivotal.io/buildpacks/ruby/ruby-tips.html#env-var){: new_window}. 
 

 
 




## Não é possível implementar apps usando o IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}
{: #ts_bm_tools_facet}

Quando uma máscara não suportada é aplicada ao projeto Eclipse, talvez você não consiga implementar os apps no {{site.data.keyword.Bluemix_notm}} usando o IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}. 

 

É possível implementar com sucesso seu app no {{site.data.keyword.Bluemix_notm}} usando a CLI do Cloud Foundry. No entanto, não é possível implementar o app no {{site.data.keyword.Bluemix_notm}} usando o IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} e você vê a mensagem de erro: `A máscara de projeto <facet_name> não é suportada.` Por exemplo, `A máscara de projeto Cloud Foundry Standalone Application versão 1.0 não é suportada.`
{: tsSymptoms}

 

O IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} mapeia projetos para tempos de execução do {{site.data.keyword.Bluemix_notm}} por máscaras de projeto. As máscaras definem os requisitos para projetos Java EE no Eclipse e são usadas como parte da configuração de tempo de execução para que diferentes tempos de execução sejam associados a diferentes projetos. Se a máscara aplicada ao projeto não for suportada pelo IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}, você pode não conseguir implementar seu app usando o IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}.
{: tsCauses}


Deve-se remover a máscara do projeto Eclipse para que seja possível implementar seu app usando o IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}.
{: tsResolve} 

Para remover a máscara, no IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}, clique em **Projeto>Propriedades>Máscaras de projeto** para o projeto. Em seguida, limpe a caixa de seleção para a máscara não suportada. 



## Erros 502 Gateway inválido são recebidos
{: #ts_502_error}

Se você receber os erros 502 Gateway inválido ao interagir com apps no {{site.data.keyword.Bluemix_notm}}, verifique a página de status do {{site.data.keyword.Bluemix_notm}} e, em seguida, execute as ações apropriadas.

 

Você recebe mensagens de erro que iniciam com 502 Gateway inválido. Por exemplo, você pode ver `502 Gateway inválido: o terminal registrado falhou em manipular a solicitação.`
{: tsSymptoms}

 

Um erro de Gateway inválido geralmente acontece quando você visita um website que usa um servidor proxy para armazenar e retransmitir os dados do servidor principal que hospeda o site. O servidor principal e o servidor proxy não podem se conectar adequadamente; portanto, você verá o código de status 502 do HTTP em sua janela do navegador. Esse código de status indica que o servidor principal do site não recebeu a implementação HTTP esperada pelo servidor proxy.
{: tsCauses}

Outras causas menos comuns de um erro de Gateway inválido são os dropouts do provedor de serviços da Internet (ISP), configurações de firewall inválidas e erros de cache do navegador. 

 

Se você suspeitar que um serviço do {{site.data.keyword.Bluemix_notm}} está inativo, verifique primeiramente a página [Status do {{site.data.keyword.Bluemix_notm}} ![Ícone de link externo](../icons/launch-glyph.svg)](http://ibm.biz/bluemixstatus){: new_window}. Talvez queira usar o serviço em outra região do {{site.data.keyword.Bluemix_notm}} como uma solução alternativa. As informações detalhadas estão disponíveis em [Usando serviços em outra região](/docs/services/reqnsi.html#cross_region_service). Se o status de serviço for normal, tente as etapas a seguir para resolver o problema: 
{: tsResolve}

  * Tente novamente a ação:
    * Recarregar a página pressionando F5 em seu teclado ou clicando no botão de atualização. Se essa etapa não funcionar, limpe os cookies e o cache do seu navegador e, em seguida, recarregue novamente.
	* Usar um navegador diferente.
	* Reinicializar seu roteador, seu modem e seu computador. Reinicializar esses dispositivos pode limpar diversos erros que conduzem ao erro 502. 
  * Aguardar e tentar novamente mais tarde. Em algumas instâncias, os problemas temporários podem ocorrer com seu provedor de serviços da Internet ou serviços do {{site.data.keyword.Bluemix_notm}}. É possível aguardar até que os problemas temporários sejam resolvidos.
  * Se o problema ainda existir, entre em contato com o suporte do {{site.data.keyword.Bluemix_notm}}. Veja [Entrando em contato com o Suporte do {{site.data.keyword.Bluemix_notm}} ![Ícone de link externo](../icons/launch-glyph.svg)](/docs/support/index.html#contacting-bluemix-support){: new_window} para obter mais informações. 




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

Apps Android em certas regiões em que o Google não está acessível não podem receber as notificações que você envia por meio do serviço IBM {{site.data.keyword.mobilepushshort}}. Nesse caso, é possível usar os serviços de terceiro como solução alternativa.

Você liga um serviço {{site.data.keyword.mobilepushshort}} ao seu app Bluemix e envia uma mensagem aos dispositivos registrados. No entanto, os apps que são desenvolvidos na plataforma Android não podem receber suas notificações em certas regiões. 
{: tsSymptoms}

O serviço IBM {{site.data.keyword.mobilepushshort}} usa o serviço Google Cloud Messaging (GCM) para despachar notificações para apps móveis que são desenvolvidos na plataforma Android. Para ativar o recebimento de notificações em apps Android, o serviço Google Cloud Messaging (GCM) deve estar acessível para apps móveis. Nas regiões em que o serviço GCM não pode ser atingido pelos apps Android, os apps Android não conseguem receber {{site.data.keyword.mobilepushshort}}.
{: tsCauses}

 
Use serviços de terceiro que não dependam do serviço GCM como uma solução alternativa, por exemplo, [Pushy ![Ícone de link externo](../icons/launch-glyph.svg)](https://pushy.me){: new_window}, [igetui ![Ícone de link externo](../icons/launch-glyph.svg)](http://www.getui.com/){: new_window} e [jpush ![Ícone de link externo](../icons/launch-glyph.svg)](https://www.jpush.cn/){: new_window}.
{: tsResolve}



## O limite de serviços da organização foi excedido
{: #ts_servicelimit}

Se você for um usuário de conta para teste, talvez não possa criar um aplicativo no {{site.data.keyword.Bluemix_notm}} se tiver excedido seu limite de serviços da organização.
 

Ao tentar criar um aplicativo no {{site.data.keyword.Bluemix_notm}}, você verá a mensagem de erro a seguir: 
{: tsSymptoms}

`BXNUI2032E: O recurso <service_instances> não foi criado. Ocorreu um erro enquanto o Cloud Foundry estava sendo contatado para criar o recurso. Mensagem do Cloud Foundry: "Você excedeu seu limite de serviços da organização."`



Esse erro ocorre quando você excede o limite no número de instâncias de serviços que pode ter para sua conta. O número máximo de instâncias de serviços para uma conta para teste é 10.
{: tsCauses} 

 

Exclua todas as instâncias de serviços que não são necessárias, ou remova o limite no número de instâncias de serviços que você pode ter.
{: tsResolve}
 
  * Para excluir uma instância de serviços, é possível usar o console do {{site.data.keyword.Bluemix_notm}} ou a interface da linha de comandos.
    Para usar o console do {{site.data.keyword.Bluemix_notm}} para excluir uma instância de serviço, conclua as etapas a seguir:
	  1. No Painel do {{site.data.keyword.Bluemix_notm}}, clique no serviço que você deseja acessar.  O cartão de serviços é exibido.
	  2. No cartão de serviços, clique no ícone **Menu**.
	  3. Clique em **Excluir serviço**. Depois de excluir a instância de serviço, você será solicitado a refazer o estágio no aplicativo ao qual a instância de serviço foi vinculada. 
    Para usar a interface de linha de comandos para excluir uma instância de serviço, conclua as etapas a seguir:
	  1. Desvincule a instância de serviço de um aplicativo digitando `cf unbind-service <appname> <service_instance_name>`.
	  2. Exclua a instância de serviço digitando `cf delete-service <service_instance_name>`.
	  3. Depois de excluir a instância de serviço, você pode desejar remontar o aplicativo ao qual a instância de serviço foi vinculada digitando `cf restage <appname>`.
  * Para remover o limite no número de instâncias de serviços que você pode ter, converta sua conta de avaliação em uma conta paga. Para obter informações sobre como converter sua conta para teste para uma conta paga, veja [Como mudar seu plano](/docs/pricing/index.html#changing).

  
  
## Os executáveis não podem ser executados no {{site.data.keyword.Bluemix_notm}}
{: #ts_executable}

Talvez você não possa executar os executáveis no {{site.data.keyword.Bluemix_notm}} quando eles forem desenvolvidos e construídos em um ambiente diferente. 

 

Você não pode executar executáveis no {{site.data.keyword.Bluemix_notm}} quando eles forem desenvolvidos e construídos em um ambiente diferente.
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

Se você for um usuário de conta para teste, talvez não consiga implementar um app no {{site.data.keyword.Bluemix_notm}} caso tenha excedido o limite de memória da sua organização. É possível reduzir a memória que seus apps usam ou aumentar a cota de memória de sua conta. 



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
	  1. No Painel do {{site.data.keyword.Bluemix_notm}}, selecione seu aplicativo. A página de detalhes do app é aberta.
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
	  
 

Quando um serviço que você ligar a um app travar, problemas como indisponibilidade, exceções e falhas de conexão poderão ocorrer no app.
O {{site.data.keyword.Bluemix_notm}} não reinicia automaticamente o app para se recuperar desses problemas.
{: tsSymptoms}



Esse comportamento é de acordo com o design do Cloud Foundry.
{: tsCauses} 

 

É possível reiniciar manualmente o app digitando o comando a seguir na interface de linha de comandos:
{: tsResolve}

```
cf push appname -p app_path
```
Além disso, é possível codificar o app para identificar e recuperar de problemas como indisponibilidades, exceções e falhas na conexão. 

	  

## As variáveis definidas pelo usuário são perdidas quando um aplicativo é enviado por push
{: #ts_varsnotretained}

Ao enviar por push um app para o {{site.data.keyword.Bluemix_notm}} a partir do IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}, as variáveis especificadas são reconfiguradas a menos que você salve as salve no arquivo manifest.



As variáveis especificadas são perdidas depois que você envia por push um app para o {{site.data.keyword.Bluemix_notm}} a partir do IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}.
{: tsSymptoms} 


As variáveis que você especificou são salvas somente se salvá-las para o arquivo manifest.
{: tsCauses} 

 

Ao enviar por push um app para o {{site.data.keyword.Bluemix_notm}} a partir do IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}, selecione a caixa de seleção **Salvar no arquivo manifest** na página de detalhes do Aplicativo do assistente do Aplicativo. Em seguida, as variáveis que você especificou no assistente são salvas para o arquivo manifest de seu aplicativo. Na próxima vez em que abrir o assistente, as variáveis serão exibidas automaticamente.
{: tsResolve}



## Os ícones do {{site.data.keyword.Bluemix_notm}} Live Sync não são mostrados
{: #ts_llz_lkb_3r}

Você criou um app no IBM Bluemix DevOps Services, mas os ícones do IBM Bluemix Live Sync não são mostrados no IDE da web.

 

Ao editar um app Node.js no IDE da web do DevOps Services, os ícones de edição em tempo real, reinicialização rápida e depuração do {{site.data.keyword.Bluemix_notm}} não são mostrados.
{: tsSymptoms}

 

Os ícones não estão disponíveis nessas circunstâncias:
{: tsCauses}

  * O arquivo `manifest.yml` não é armazenado no nível superior de seu projeto.
  * Seu app é armazenado em um subdiretório em vez do nível superior de seu projeto, mas o caminho para o subdiretório não é especificado no arquivo `manifest.yml`.
  * O app não contém um arquivo `package.json`.


Use um dos métodos a seguir para resolver o problema: 
{: tsResolve} 

  * Se o arquivo `manifest.yml` não estiver armazenado no
nível superior de seu projeto, armazene-o lá.
  * Se seu app estiver armazenado em um subdiretório, especifique o caminho para o
subdiretório no arquivo `manifest.yml`.
  ```
   path: path_to_application
   ```
  * Crie um arquivo `package.json` que esteja no
mesmo diretório que seu app.

  
  
  
<!-- begin STAGING ONLY --> 

## O Bluemix Live Sync Debug não é iniciado na linha de comandos
{: #ts_no_debug}

Você ativou o recurso IBM Bluemix Live Sync Debug para seu app usando a linha
de comandos, mas não é possível acessar a interface de depuração.  
  
 

Você ativou o recurso de depuração para seu aplicativo configurando a variável de
ambiente **BLUEMIX_APP_MGMT_ENABLE**. No entanto, não é possível
acessar a interface com o usuário de depuração em `app_url/bluemix-debug/manage`.
{: tsSymptoms}



O recurso de depuração não pode ser ativado nestas situações:
{: tsCauses} 

  * Quando o `manifest` contém o atributo de comando
  * Quando você usa a opção **-c** para enviar por push um app
para o {{site.data.keyword.Bluemix_notm}}

 
  
Use uma das opções a seguir para resolver o problema: 
{: tsResolve}

  * A prática recomendada é usar o buildpack IBM Node.js para iniciar o app. Para obter mais informações, consulte a seção Comando de inicialização do tópico
[Implementando um aplicativo Node.js no {{site.data.keyword.Bluemix_notm}}](/docs/runtimes/nodejs/index.html#nodejs_runtime). 
  * Desative o comando para seu app existente revisando o atributo de
comando no `manifest.yml` para o comando: null ou editando seu
comando push para incluir `-c Null`. 
  * Remova o atributo de **comando** do `manifest.yml`. Em
seguida, exclua o app atual do {{site.data.keyword.Bluemix_notm}} e envie por
push o app novamente.
  
<!-- end STAGING ONLY -->  
  
  

  
  
## As organizações não podem ser localizadas no {{site.data.keyword.Bluemix_notm}}
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



Esse problema ocorre porque o terminal de API da região
com a qual você deseja trabalhar não está especificado e a organização
que está sendo procurada pode estar em uma região diferente.
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

Você pode não conseguir usar o comando cf push para implementar um app da Web arquivado no {{site.data.keyword.Bluemix_notm}} se o local do app não for especificado corretamente.
	


Ao fazer upload de um app WAR no {{site.data.keyword.Bluemix_notm}} usando o comando `cf push`, você vê mensagem de erro `Erro de preparação: não é possível obter instâncias uma vez que a preparação falhou.`
{: tsSymptoms} 

 

Esse problema poderá ocorrer se o arquivo WAR não for
especificado, ou se o caminho para o arquivo WAR não for especificado. 
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





## Caracteres de byte duplo não são exibidos corretamente quando os aplicativos Liberty são enviados por push ao {{site.data.keyword.Bluemix_notm}}
{: #ts_doublebytes}

Os caracteres de byte duplo podem não ser exibidos corretamente
se o suporte Unicode não estiver configurado para os arquivos servlet ou JSP.

 

Quando um aplicativo Liberty é enviado por push para o {{site.data.keyword.Bluemix_notm}}, os caracteres de byte duplo que são especificados no app não são exibidos corretamente.
{: tsSymptoms}

 

O problema poderá ocorrer se o suporte Unicode não for configurado
corretamente para os arquivos servlet ou JSP.
{: tsCauses}


É possível usar o código a seguir dentro do arquivo servlet ou
JSP:
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

É possível encontrar problemas ao atualizar um app Node.js
ou implementar um app Node.js no {{site.data.keyword.Bluemix_notm}}.



Ao atualizar um app Node.js ou implementar seu app Node.js
no {{site.data.keyword.Bluemix_notm}},
é possível ver uma das mensagens de erro a seguir:
{: tsSymptoms} 

`Um app não foi detectado com êxito por nenhum buildpack disponível.`


`A instância (índice 0) falhou ao iniciar a aceitação de conexões.`


`Não é possível obter instâncias, uma vez que a preparação falhou.`


 

Os motivos a seguir são possíveis causas do problema:
{: tsCauses}
 
  * O comando inicial não foi especificado.
  * Arquivos que são necessários para implementar um app Node.js estão ausentes
no app ou foram colocados em uma pasta diferente do diretório-raiz.
  


	
Execute as ações a seguir com base na causa que leva
ao problema:
{: tsResolve} 

  * Especifique o comando inicial por um dos métodos a seguir: 
      * Use a interface de linha de comandos cf. Por
exemplo: 
        ```
		cf push MyUniqueNodejs01 -p app_path -c "node app.js"
		```
	  * Use o arquivo [package.json ![Ícone de link externo](../icons/launch-glyph.svg)](https://docs.npmjs.com/json){: new_window}. Por
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

  * Assegure-se de que um arquivo `package.json` exista em seu app Node.js para ativar o buildpack Node.js para reconhecer o app. Além disso,
deve-se colocar esse arquivo no diretório-raiz de seu app.	
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
	
Para obter mais dicas sobre apps Node.js, veja [Dicas para aplicativos Node.js ![Ícone de link externo](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/buildpacks/node/node-tips.html){: new_window}.	




## Erros de configuração aparecem no arquivo `server.xml` depois de importar um app {{site.data.keyword.Bluemix_notm}} Liberty do Bluemix DevOps Services para o Eclipse
{: #ts_eclipse}

Se você vir erros de configuração no arquivo `server.xml` depois de importar um app {{site.data.keyword.Bluemix_notm}} Liberty do IBM Bluemix DevOps Services para o Eclipse, pode ser necessário remover o arquivo `server.xml` do projeto. 

 

Depois de importar um app {{site.data.keyword.Bluemix_notm}} Liberty do {{site.data.keyword.Bluemix_notm}} DevOps Services para o Eclipse, você vê erros de configuração no arquivo `server.xml` a partir da visualização Problemas do Eclipse. 
{: tsSymptoms}

 

O buildpack do Liberty usa o arquivo `server.xml` para configurar o app e gera um arquivo `runtime-vars.xml` quando o app Liberty é enviado por push ao {{site.data.keyword.Bluemix_notm}}. Quando você importa o app para o Eclipse, o arquivo `runtime-vars.xml` não existe em seu ambiente local.
{: tsCauses}

 

É possível resolver esse problema removendo o arquivo server.xml do projeto. O buildpack cria o arquivo `server.xml` dinamicamente quando você
envia por push o app como um app WAR. Para obter mais informações, consulte [Liberty for Java](/docs/runtimes/liberty/index.html).
{: tsResolve}
	
	
## Os aplicativos não podem ser colocados em estágios usando buildpacks customizados
{: #ts_bp_compilation}

Você pode não conseguir implementar um app no {{site.data.keyword.Bluemix_notm}} usando um buildpack customizado se os scripts no buildpack não forem executáveis.



Ao implementar um app no {{site.data.keyword.Bluemix_notm}} usando um buildpack customizado, você vê a mensagem de erro `O aplicativo falhou na preparação, portanto, não há instâncias a serem exibidas.`
{: tsSymptoms} 


Esse problema
poderá ocorrer se scripts, como o script de detecção, o script de compilação
                e o script de liberação não forem executáveis.
{: tsCauses}

 

É possível usar o comando [git update ![Ícone de link externo](../icons/launch-glyph.svg)](http://git-scm.com/docs/git-update-index){: new_window} para mudar a permissão de cada script para executável. Por exemplo, é possível digitar `git update --chmod=+x script.sh`.
{: tsResolve}
	
	
	
## Não é possível implementar um aplicativo a partir do DevOps Services para o {{site.data.keyword.Bluemix_notm}}
{: #ts_devops_to_bm}

Você pode não conseguir enviar por push seu app do IBM Bluemix DevOps Services para o {{site.data.keyword.Bluemix_notm}} se o arquivo `manifest.yml` não estiver presente em seu app.

 

Ao implementar um app a partir do DevOps Services no {{site.data.keyword.Bluemix_notm}}, uma mensagem de erro `Impossível detectar um tipo de aplicativo suportado` pode ser exibida.
{: tsSymptoms}

 

Esse problema pode ocorrer porque o DevOps Services requer um arquivo `manifest.yml` para implementar um app no {{site.data.keyword.Bluemix_notm}}.
{: tsCauses}

 

Para resolver esse problema, você deve criar um arquivo `manifest.yml`. Para obter informações adicionais sobre como criar um arquivo `manifest.yml`,
consulte [Manifest do
aplicativo](/docs/manageapps/depapps.html#appmanifest).
{: tsResolve}	
	




## Os apps Meteor não podem ser enviados por push
{: #ts_meteor}

Talvez você não consiga enviar por push um aplicativo Meteor para
{{site.data.keyword.Bluemix_notm}} se o buildpack não estiver especificado corretamente.

 

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
	
  

    
## O botão Implementar no {{site.data.keyword.Bluemix_notm}} não implementa um app
{: #deploytobluemixbuttondoesntdeployanapp}

Se você clicar no botão Implementar ao {{site.data.keyword.Bluemix_notm}}
e descobrir que o repositório Git não é clonado ou o app não
é implementado, tente os métodos de resolução de problemas para os seguintes problemas.
  * [O projeto Bluemix DevOps Services não pode ser criado](#project-cannot-be-created)
  * [O repositório Git não é localizado e não pode ser clonado no DevOps Services](#repo-not-found)
  * [O repositório Git é clonado no DevOps Services, mas o app não é implementado no {{site.data.keyword.Bluemix_notm}}](#repo-cloned-app-not-deployed)

Para obter mais informações sobre como criar o botão, consulte Criando um botão
Implementar no {{site.data.keyword.Bluemix_notm}}.

### O projeto Bluemix DevOps Services não pode ser criado
{: #project-cannot-be-created}

Se você descobrir que o projeto DevOps Services não pode ser criado, conta do IBM {{site.data.keyword.Bluemix_notm}} pode ter expirado.



Você clica no botão **Implementar no Bluemix**, mas a etapa "Criando projeto" não é concluída com êxito.
{: tsSymptoms} 


Sua conta do {{site.data.keyword.Bluemix_notm}}
pode ter expirado.
{: tsCauses} 

Use um dos métodos a seguir para corrigir o problema:
{: tsResolve}

  * Efetue login no {{site.data.keyword.Bluemix_notm}} e
atualize as informações de sua conta.
  * Clique no botão **Implementar no Bluemix** novamente.


### O repositório Git não é localizado e não pode ser clonado no DevOps Services
{: #repo-not-found}

Se você descobrir que o repositório Git não foi clonado, pode existir um problema
com o repositório ou com o fragmento do botão.



Você clica no botão **Implementar no Bluemix**, mas o repositório Git não é localizado e não pode ser clonado no DevOps Services. A etapa "Clonando repositório" não é concluída com êxito. Portanto, o app não pode ser implementado no {{site.data.keyword.Bluemix_notm}}. 
{: tsSymptoms} 

Esse problema pode ocorrer pelas razões a seguir:
{: tsCauses} 

  * O repositório Git pode não existir ou estar acessível.
  * Pode existir um problema no HTML ou na redução de preço do fragmento do botão.
  * Pode existir um problema em que caracteres especiais, parâmetros de consulta ou
fragmentos na URL estejam evitando que o repositório Git seja
acessado corretamente.

Use um dos métodos a seguir para corrigir o problema:
{: tsResolve}

  * Verifique se seu repositório Git existe, está acessível publicamente
e se a URL está correta.
  * Verifique se o fragmento não contém erros de HTML ou de redução de preço.
  * Se caracteres especiais, parâmetros de consulta ou fragmentos causarem um problema com a URL do repositório Git, codifique a URL no fragmento do botão.
  

  
  
### O repositório Git é clonado no DevOps Services, mas o app não é implementado no {{site.data.keyword.Bluemix_notm}}
{: #repo-cloned-app-not-deployed}

Se você descobrir que o app não foi implementado, podem existir problemas
com o código no repositório.
     


Você clica no botão **Implementar no Bluemix** e o repositório Git é clonado no DevOps Services, mas o app não é implementado no {{site.data.keyword.Bluemix_notm}}. A etapa "Implementando no Bluemix" não é concluída com êxito.
{: tsSymptoms} 

Esse problema pode ocorrer pelas razões a seguir:
{: tsCauses}  

  * Pode não haver espaço suficiente no espaço do {{site.data.keyword.Bluemix_notm}}
para implementar um aplicativo. 
  * Um serviço necessário pode não estar declarado no arquivo `manifest.yml`.
  * Um serviço necessário pode estar declarado no arquivo `manifest.yml`,
mas o serviço já está no espaço de destino.
  * Pode existir um problema com o código no repositório.
Para diagnosticar o problema, revise a construção e implemente logs
a partir da implementação:
  1. Quando a etapa "Implementando no Bluemix" não for concluída com êxito, clique no link na etapa anterior "Configurando pipeline" para abrir o Delivery Pipeline.
  2. Identifique a construção com falha ou o estágio de implementação.
  3. No estágio com falha, clique em **Visualizar logs e histórico**.
  4. Localize a mensagem de erro.
   
Use um dos métodos a seguir para corrigir o problema:
{: tsResolve}

  * Se a mensagem de erro indicar que não há espaço suficiente no espaço
do {{site.data.keyword.Bluemix_notm}}
para implementar o app, destine outro espaço.
  * Se a mensagem de erro indicar que um serviço necessário não está declarado no arquivo `manifest.yml`, notifique o proprietário do repositório de que o serviço necessário deve ser incluído.
  * Se a mensagem de erro indicar que um serviço necessário já existe
no espaço de destino, selecione um espaço diferente para ser usado.
  * Se a mensagem de erro indicar que existe um problema com a construção,
corrija todos os problemas com o código que está evitando que o app seja
construído. Para verificar se o código não contém quaisquer problemas, construa
o código usando comandos Git:
    1. Clone o repositório Git:
    ```
    git clone <git_repository_URL>
    ```
	2. Abra o diretório do app:
	```
	cd <appname>
	```
	3. Crie o app:
	```
	<appname> create
	```
	4. Se necessário, forneça complementos.
	5. Inclua todas as variáveis de configuração necessárias.
	6. Envie o código por push:
	```
	git push <appname> master
	```
	7. Verifique se o app está construído corretamente.
	8. Se necessário, execute o comando de implementação post:
	```
	<appname> run
	```
	9. Abra o app e verifique se ele está funcionando corretamente:
	```
	<appname> open
	```
	
## Falha ao implementar um app a partir da barra de execução
{: #deployinganappfromtherunbarfails}

Nesse cenário, a implementação falha em um estado amarelo, "não sincronizado". 

O app que você está implementando tem a mesma rota de outro app que está
em execução. Para corrigir esse problema, mude o caminho para ser exclusivo.

## A barra de execução não pode ser encontrada
{: #runbarcannotbefound}

Caso você não veja a barra de execução no Eclipse Orion {{site.data.keyword.webide}}, um destes problemas ocorreu:

1. O {{site.data.keyword.jazzhub}} não está identificando seu projeto como um projeto.
   * Correção: no diretório raiz do seu projeto, crie um arquivo `project.json`.
2. O {{site.data.keyword.jazzhub_short}} falhou ao determinar em qual pasta seu app está.
   * Correção: se seu app estiver em um diretório diferente da raiz do projeto, execute uma destas etapas:
      * No diretório raiz do seu projeto, crie um arquivo
`manifest.yml`. Em seguida, edite o arquivo para que ele aponte para o local de seu app; por exemplo, `path: path_to_your_app`
      * Mova seu app para que ele fique no diretório raiz do seu projeto.
3. O {{site.data.keyword.jazzhub_short}} não detecta que seu app é um app Node.js.
   * Correção: na pasta do app de seu projeto, crie um arquivo `package.json`.
   

## O gancho do GitHub não está funcionando
{: #githubhookisntworking}

Se você configurou seu projeto GitHub para criar links de itens de trabalho
quando você enviar por push confirmações e os links não estiverem funcionando
conforme o esperado, siga estas etapas para encontrar o problema:

1. Em seu repositório GitHub, clique em **Configurações**.
   ![Link de configurações do GitHub](images/github_settings.png)

2. Clique em **Webhooks & serviços**.
   ![Link de webhooks e serviços do GitHub](images/github_webhook.png)

3. Para visualizar a mensagem, passe o mouse sobre o ícone de status do {{site.data.keyword.jazzhub}}.
   ![Mensagem de erro no gancho de serviço](images/github_error.png)

4. Resolva o erro de acordo com a mensagem do GitHub.

5. Para verificar se a correção funcionou, confirme e envie por push outra mudança, ou acesse a página de serviço do {{site.data.keyword.jazzhub_short}} e clique em **Testar serviço**.
   ![botão Testar serviço do GitHub](images/github_test.png)

6. Confirme se não há erros verificando o ícone de status novamente.
   ![Ícone de status sem erros](images/githubResolved_small.png)

Para obter mais informações, veja [Configurando projetos do GitHub para o Bluemix DevOps Services ![Ícone de link externo](../icons/launch-glyph.svg)](https://hub.jazz.net/docs/githubhooks/){: new_window}.


# Resolução de problemas para gerenciamento de contas
{: #managingaccounts}

Você pode ter problemas ao gerenciar sua conta, como apps diferentes compartilham o mesmo nome de domínio e administradores não podem visualizar todas as organizações. No entanto, em vários casos, é possível recuperar-se desses
problemas seguindo algumas etapas simples.
{:shortdesc}


## A conta está inativa
{: #ts_accnt_inactive}

Não é possível criar um app no {{site.data.keyword.Bluemix_notm}} se a sua conta estiver inativa. Deve-se entrar em contato com a equipe de suporte para corrigir esse problema.



Ao tentar criar um app no {{site.data.keyword.Bluemix_notm}}, você vê a mensagem de erro a seguir:
{: tsSymptoms} 

`BXNUI0096E: O app não foi criado. Sua conta está inativa porque ela foi cancelada
ou suspensa.`


O status de sua conta do {{site.data.keyword.Bluemix_notm}} torna-se inativo quando a conta é cancelada ou suspensa.
{: tsCauses}

 

Para reativar sua conta, entre em contato com o [Suporte do {{site.data.keyword.Bluemix_notm}} ![Ícone de link externo](../icons/launch-glyph.svg)](http://ibm.biz/bluemixsupport.com){: new_window}. No email, deve-se incluir as informações a seguir:
{: tsResolve}

  * O ID IBM que você usa para efetuar login no {{site.data.keyword.Bluemix_notm}}.
  * O nome da organização em que seu app está sendo criado. Essas informações podem ajudar a equipe de suporte a determinar se você está designado às funções ou associação corretas em sua organização.



## Nenhum espaço está associado com a sua organização atual
{: #ts_no_space}

Não será possível criar um aplicativo se não houver espaço
associado à sua organização atual.



Ao tentar criar um app no {{site.data.keyword.Bluemix_notm}}, você vê a mensagem de erro a seguir:
{: tsSymptoms} 


`BXNUI0097E: Para que seja possível incluir um app, pelo menos um espaço deve estar associado à sua organização e região. No Painel, clique em **Criar um espaço**. Quando o espaço for criado, tente novamente. `



Os apps no {{site.data.keyword.Bluemix_notm}} devem ser criados dentro de um espaço em sua organização.
{: tsCauses} 

 

Para criar um espaço, use um dos métodos a seguir: 
{: tsResolve}
 
  * No Painel do {{site.data.keyword.Bluemix_notm}}, selecione a organização em que você deseja criar o espaço, em seguida, clique em **Criar um espaço**.
  * Na interface de linha de comandos cf, digite `cf create-space <space_name> -o <organization_name>`.
  
  
  
  
## Os apps compartilham o mesmo nome de domínio
{: #ts_domain_diff}

Você pode observar que diversos aplicativos compartilham a mesma
URL em {{site.data.keyword.Bluemix_notm}}.

 

Esse problema pode ocorrer quando você designa a mesma
rota de URL para diferentes aplicativos dentro de um espaço.
{: tsCauses}

Por exemplo, você envia por push o aplicativo myApp1 para o {{site.data.keyword.Bluemix_notm}} e configura o domínio como "mynewapp.stage1.mybluemix.net". Em seguida, você envia por push outro aplicativo myApp2 para o mesmo espaço e configura uma de suas rotas de URL como "mynewapp.stage1.mybluemix.net". A rota agora é mapeada para ambos os aplicativos.

 

Esse é o comportamento suportado do {{site.data.keyword.Bluemix_notm}} e
é possível usar essa prática para atingir o tempo de inatividade zero para o upgrade de seu
aplicativo. Para obter mais informações, veja Implementações azul-verde.
{: tsResolve}
  
	
	
<!-- begin STAGING ONLY --> 
	
	
## Os administradores não podem visualizar todas as organizações usando o console do {{site.data.keyword.Bluemix_notm}}
{: #ts_ui_org}

Como um administrador, quando você usa o console do {{site.data.keyword.Bluemix_notm}}, não é possível exibir todas as organizações para administrá-las. Você pode exibir e administrar apenas as organizações às quais pertence.

 

Como um administrador, não é possível ver todas as organizações usando o console do {{site.data.keyword.Bluemix_notm}}.
{: tsSymptoms}

 

Esta é uma limitação do console do {{site.data.keyword.Bluemix_notm}}.
{: tsCauses}

 

É possível usar o comando, como `cf orgs`, `cf
create-org` e `cf delete-org`, a partir da interface de linha
de comandos cf para gerenciar todas as organizações. Para obter uma lista completa de
comandos cf, insira `cf help`.
{: tsResolve}
	
<!-- end STAGING ONLY -->




## O cartão de crédito não pode ser incluído
{: #ts_addcc}

Não é possível enviar suas informações de cartão de crédito para converter
sua conta para teste em uma conta Pré-pago.

 

O botão Enviar na página Incluir cartão de crédito está desativado.
{: tsSymptoms}

 

Esse problema ocorre quando suas informações não são preenchidas corretamente na página Incluir cartão de crédito.
{: tsCauses}

 

Conclua as etapas a seguir para resolver esse problema:
{: tsResolve}

  1. Na página Incluir cartão de crédito, preencha todos os campos obrigatórios nas seções de informações de contato, endereço de contato e endereço para cobrança.
  2. Selecione **Eu li e concordo com os Termos e Condições da IBM**,
em seguida, clique em **Enviar**. A seção **Selecionar um método de pagamento** é exibida.
  3. Insira seu número do cartão de crédito, a data de expiração de seu cartão
e o código de segurança que está em seu cartão. Em seguida,
clique em **Enviar**.





# Resolução de problemas para tempos de execução
{: #runtimes}

Talvez você tenha problemas ao usar os tempos de execução do IBM® Bluemix™. No entanto, em vários casos, é possível recuperar-se desses
problemas seguindo algumas etapas simples.
{:shortdesc}


## Buildpack obsoleto usado quando um aplicativo é enviado por push
{: #ts_loading_bp}


Talvez você não consiga usar os componentes de buildpack mais recentes ao enviar um app por push. É possível usar buildpacks que possuem mecanismos integrados
para evitar o carregamento de componentes obsoletos ou é possível excluir os conteúdos no diretório de cache de seu app antes de enviar por push ou remontar o app. 

 

Ao enviar por push ou remontar um app após a atualização do
buildpack, os componentes de buildpack mais recentes não são carregados automaticamente. Como resultado, o seu aplicativo usa os componentes de buildpack obsoletos a partir do cache. As atualizações
que foram aplicadas ao buildpack desde a última vez que o app foi enviado por
push não são implementadas. 
{: tsSymptoms}



Alguns
buildpacks não são configurados para fazer download automaticamente de todos os componentes
atualizados da Internet para assegurar que você sempre use a versão mais
recente.
{: tsCauses} 

 

É possível usar buildpacks que possuem mecanismos integrados para
evitar o carregamento de componentes obsoletos. Os buildpacks a seguir são dois
exemplos: 
{: tsResolve}

  * [Buildpack Java do Cloud Foundry ![Ícone de link externo](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/java-buildpack){: new_window}. Esse buildpack tem um mecanismo integrado para assegurar que a versão mais recente do buildpack seja usada. Para obter mais informações sobre como esse mecanismo funciona, veja [extending-caches.md ![Ícone de link externo](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/java-buildpack/blob/master/docs/extending-caches.md){: new_window}. 
  * [Buildpack Node.js do Cloud Foundry ![Ícone de link externo](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/nodejs-buildpack){: new_window}. Esse buildpack tem funcionalidade semelhante usando variáveis de ambiente. Para que o buildpack Node.js sempre possa fazer download de módulos do nó a partir da Internet, digite o comando a seguir na interface de linha de comandos cf: 	
  ```
  set NODE_MODULES_CACHE=false
  ```
Se o buildpack que você estiver usando não fornecer um mecanismo para carregar os componentes mais recentes automaticamente, será possível excluir manualmente os conteúdos no diretório de cache e enviar por push seu app novamente executando as etapas a seguir:
  1. Efetue o check-out de uma ramificação de um buildpack nulo, por exemplo, https://github.com/ryandotsmith/null-buildpack. Para obter informações sobre como efetuar check-out de uma ramificação, veja [Conceitos básicos do Git - Obtendo um repositório Git ![Ícone de link externo](../icons/launch-glyph.svg)](http://www.git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository){: new_window}.  
  2. Inclua a linha a seguir no arquivo `null-buildpack/bin/compile` e confirme as mudanças. Para obter informações sobre como confirmar mudanças, veja [Conceitos básicos do Git - Registrando mudanças no repositório ![Ícone de link externo](../icons/launch-glyph.svg)](http://www.git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository){: new_window}.
  ```
  rm -rfv $2/*
  ```
  3. Envie seu app por push com o buildpack nulo que foi modificado para excluir o cache usando o comando a seguir. Depois de concluir essa etapa, todos os conteúdos no diretório de cache de seu app serão excluídos.
  ```
  cf push appname -p app_path -b <modified_null_buildpack>
  ```
  4. Envie seu app por push com o buildpack mais recente que você deseja usar usando o comando a seguir: 
  ```
  cf push appname -p app_path -b <latest_buildpack>
  ```
  
	


## Mensagens de AVISO do buildpack PHP
{: #ts_phplog}

Talvez você veja mensagens que contenham AVISO nos logs. É possível parar a criação de log dessas mensagens alterando o nível de criação de log.	
	
 

Ao enviar por push um aplicativo para o Bluemix usando um buildpack PHP, você pode ver mensagens que contêm `NOTICE`:
{: tsSymptoms}

```
• 2015-01-26T15:00:59.70+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: [pool www] 'user' directive is ignored when FPM is not running as root
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: [pool www] 'user' directive is ignored when FPM is not running as root
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: fpm is running, pid 93
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: ready to handle connections
```



No buildpack PHP, o parâmetro error_log é usado para definir o nível de criação de log. Por padrão, o valor do parâmetro `error_log` é **stderr notice**. O exemplo a seguir mostra a configuração do nível de criação de log padrão no arquivo `nginx-defaults.conf` do buildpack PHP que é fornecido pelo Cloud Foundry. Para obter mais informações, veja [cloudfoundry/php-buildpack ![Ícone de link externo](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/php-buildpack/blob/ff71ea41d00c1226d339e83cf2c7d6dda6c590ef/defaults/config/nginx/1.5.x/nginx-defaults.conf){: new_window}.
{: tsCauses} 

```
daemon off;
error_log stderr notice;
pid @{HOME}/nginx/logs/nginx.pid;
```

 	
	
As mensagens `NOTICE` são informativas e não necessariamente indicam que ocorreu um problema. É possível parar a criação de log dessas mensagens mudando o nível de criação de log de aviso de erro padrão para erro padrão no arquivo nginx-defaults.conf de seu buildpack. Por exemplo: 	
{: tsResolve}

```
daemon off;
error_log stderr error;
pid @{HOME}/nginx/logs/nginx.pid;
```
Para obter mais informações sobre como mudar a configuração de criação de log padrão, veja [error_log ![Ícone de link externo](../icons/launch-glyph.svg)](http://nginx.org/en/docs/ngx_core_module.html#error_log){: new_window}.
	

## Impossível importar uma biblioteca Python de terceiro para o {{site.data.keyword.Bluemix_notm}}
{: #ts_importpylib}

Pode ser que você não consiga importar uma biblioteca Python de terceiros para o {{site.data.keyword.Bluemix_notm}}. É possível resolver o problema incluindo arquivos de configuração no diretório-raiz do aplicativo python.


Ao tentar importar uma biblioteca Python de terceiros, como a biblioteca `web.py`, o comando `cf push` falha.
{: tsSymptoms}


 

Esse problema ocorre quando as informações de configuração para o aplicativo Python estão ausentes.
{: tsCauses}


 

Para resolver o problema, inclua um arquivo `requirements.txt` e um arquivo `Procfile` no diretório-raiz de seu app Python. As informações a seguir assumem que você esteja importando a biblioteca web.py:
{: tsResolve}

  1. Inclua um arquivo `requirements.txt` no diretório-raiz de seu app Python.
     O arquivo `requirements.txt` especifica os pacotes de biblioteca necessários para o seu aplicativo Python e a versão dos pacotes. O exemplo a seguir mostra o conteúdo do arquivo `requirements.txt`, em que `web.py==0.37` indica que a versão da biblioteca `web.py` que será transferida por download é 0,37 e `wsgiref==0.1.2` indica que a versão da interface do gateway do servidor da web que é requerida pela biblioteca web.py é 0.1.2.
	 ```
	 web.py==0.37
     wsgiref==0.1.2
	 ```
	Para obter mais informações sobre como configurar o arquivo `requirements.txt`, consulte [Arquivos de requisitos](https://pip.readthedocs.org/en/1.1/requirements.html).
	
  2. Inclua um arquivo `Procfile` no diretório-raiz de seu aplicativo Python.
	O arquivo `Procfile` deve conter o comando inicial do aplicativo Python. No comando a seguir, *yourappname* é o nome de seu aplicativo Python e *PORT* é o número da porta que o seu aplicativo Python deve usar para receber solicitações de usuários do app. *$PORT* é opcional. Se você não especificar PORT no comando inicial, o número da porta sob a variável de ambiente `VCAP_APP_PORT` que está dentro do aplicativo será usado em seu lugar. 
	```
	web: python <yourappname>.py $PORT
	```
Agora você pode importar a biblioteca Python de terceiros para o {{site.data.keyword.Bluemix_notm}}.	



## O botão Ações na página Detalhes da instância está desativado
{: #ts_actionsbutton}



O botão Ações na página Detalhes da instância está desativado.
{: tsSymptoms} 

 

Esse problema ocorre por causa dos seguintes motivos:
{: tsCauses}

  * O aplicativo não é um aplicativo da Web Java™. O Runtime Management Utilities (RMU) suporta somente aplicativos da web que são implementados com buildpacks Liberty.
  * O aplicativo não é implementado com o buildpack Liberty integrado.
  * O aplicativo foi implementado com uma versão anterior do buildpack Liberty.



Se o problema for causado por uma versão anterior do buildpack Liberty, reimplemente o aplicativo no {{site.data.keyword.Bluemix_notm}}. Caso contrário, é possível fornecer os arquivos de log do aplicativo do cliente para a equipe de suporte:
{: tsResolve} 

  * logs/messages.log
  * logs/stdout.log
  * logs/stderr.log
  

  
  
## São necessárias credenciais ao abrir janela de rastreio ou dump
{: #ts_username}


 

Um nome de usuário e senha são necessários ao abrir a janela de rastreio e dump.
{: tsSymptoms}

 

Esse problema ocorre por causa do tempo limite da sessão de login.
{: tsCauses}

 

A solução é reinserir o nome de usuário e senha.
{: tsResolve}




## Ocorre um erro quando operações de rastreio ou de dump estão em execução
{: #ts_target}

 

Uma mensagem de erro é exibida quando as operações de rastreio ou dump estão em execução. A mensagem indica que uma instância de destino para um app não está no estado em execução	
{: tsSymptoms}

```
Instância 0: A especificação de rastreio foi configurada com êxito
Instância 2: A especificação de rastreio foi configurada com êxito.
Instância 1: A instância de destino 1 para o app abcd não está no estado de execução.
Instância 3: A especificação de rastreio foi configurada com êxito
Instância 4: A especificação de rastreio foi configurada com êxito
```



Esse problema ocorre por causa dos seguintes motivos:
{: tsCauses} 

  * As capacidades de gerenciamento de rastreio ou dump são apenas para instâncias do aplicativo que estão em execução. As operações de rastreio ou dump não podem ser usadas em instâncias do aplicativo que são interrompidas, estão iniciando ou são travadas.
  * O status da instância do aplicativo é alterado quando o diálogo de rastreio ou dump é aberto. 
  


A solução é fechar a janela e depois reabri-la novamente.
{: tsResolve} 



## Instâncias possuem configuração traceSpecification diferente
{: #ts_different_config}

 

Para diferentes instâncias de um aplicativo, você pode ver uma configuração traceSpecification diferente.
{: tsSymptoms}

 

Esse problema ocorre por causa dos seguintes motivos:
{: tsCauses}

  * Você pode ter mudado a configuração para uma ou mais instâncias anteriormente. Se você muda a configuração traceSpecification para uma instância, ela não se aplica a outras instâncias do mesmo aplicativo. Por exemplo, seu aplicativo usa log4j e você tem 2 instâncias para esse aplicativo. É possível mudar o nível de log da instância 0 de informações para depuração, mas o nível de log da instância 1 permanece informações. 
  * O aplicativo está ampliado e tem novas instâncias. O RMU não se aplica à configuração traceSpecification da instância existente para a nova instância ampliada. A nova instância usa a configuração padrão. Por exemplo, seu aplicativo usa log4j e tem uma instância. É possível mudar o nível de log dessa instância de informações para depuração. Depois de fazer essa mudança, se você ampliar seu aplicativo em duas instâncias, o nível de log da nova instância será informações, em vez de depuração.
  


Este comportamento é esperado.
{: tsResolve} 





## Cota do disco excedida
{: #ts_diskquota}

Você pode ver, em seu log de app, que sua cota do disco foi excedida.

 

Você vê a mensagem de erro `Cota do disco excedida` no log de seu app.
{: tsSymptoms}



Este problema é causado por um dos motivos a seguir: 
{: tsCauses} 

  * Os arquivos de dump são gerados com as instâncias do aplicativo em execução e os arquivos usam até a cota de disco alocada. Por padrão, a cota de disco para uma instância do aplicativo é 1 GB. É possível verificar o uso de seu disco clicando em **Painel>Aplicativo>Tempo de Execução do Aplicativo**. O exemplo a seguir mostra as informações de tempo de execução, incluindo uso do disco, para duas instâncias de um aplicativo:
    ```
    Instance	State	CPU	Memory Usage	Disk Usage

	0		Executando	1,0%	344,8 MB/512 MB	236,8 MB/1 GB
	2		Executando	2,3%	361,2 MB/512 MB	235,7 MB/1 GB
    ```
  * A cota do disco é limitada pela cota da organização atual.
  
  


É possível resolver esse problema usando um dos métodos a seguir:
{: tsResolve} 

  * Excluir arquivos de dump depois de eles serem transferidos por download.
  * Reimplementar o aplicativo com uma cota do disco maior, incluindo a entrada a seguir no manifest de implementação:
    ```
	disk_quota: 2048
	```
	
	
<!-- begin STAGING ONLY --> 

	
## Os objetos do criador de logs Log4js não são exibidos na janela pop-up Rastreio do Node.js
{: #ts_logger}

Os objetos do criador de logs log4js não são exibidos na janela pop-up Rastreio do Node.js quando os módulos log4js e ibmbluemix são usados em seu app. 	

 
Os objetos do criador de logs log4js não são exibidos na janela pop-up Rastreio do Node.js quando os módulos log4js, winston e ibmbluemix são usados em seu app.
{: tsSymptoms}


Como o módulo ibmbluemix fornece uma API unificada para operações de log que usam os módulos log4js e winston, apenas os objetos do criador de logs ibmbluemix são exibidos na janela pop-up Rastreio do Node.js. Isso tem o objetivo de fazer com que as configurações de nível de log para os objetos do criador de logs ibmbluemix, log4js e winston parem de sobrescrever umas às outras.
{: tsCauses}


Este comportamento é esperado.
{: tsResolve}

<!-- end STAGING ONLY -->




<!-- begin STAGING ONLY -->


## A caixa de seleção Aplicar configuração de rastreio a todas as instâncias do aplicativo está desativada
{: #ts_bunyan}

A caixa de seleção **Aplicar configuração de rastreio a todas as instâncias do aplicativo** é desmarcada e desativada na janela pop-up Rastreio do Node.js quando os níveis do criador de logs Bunyan são modificados.



Quando você muda os níveis dos objetos do criador de logs Bunyan, a caixa de seleção **Aplicar configuração de rastreio a todas as instâncias do aplicativo** é desmarcada e desativada na janela pop-up Rastreio do Node.js.
{: tsSymptoms} 

 

Quando os níveis de log do Bunyam são modificados, a configuração de rastreio não pode ser aplicada a todas as instâncias de um aplicativo. Isso ocorre porque a biblioteca Bunyam não requer que os nomes ou identificadores dos objetos do criador de logs Bunyam sejam exclusivos. Mais de um dos objetos do criador de logs Bunyam que são usados para especificar níveis nas mensagens de log do seu aplicativo podem ter o mesmo nome ou identificador. Portanto, se a configuração de rastreio estiver ativada para um aplicativo, os níveis de log especificados nas mensagens de log do aplicativo poderão ser imprecisos.
{: tsCauses}




Este comportamento é esperado.
{: tsResolve} 

<!-- end STAGING ONLY -->

