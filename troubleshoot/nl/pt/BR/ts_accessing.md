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



# Resolução de problemas para acessar o {{site.data.keyword.Bluemix_notm}} 
{: #accessing}


Problemas gerais com o acesso ao {{site.data.keyword.Bluemix}}
podem incluir um usuário que não foi capaz de efetuar login no {{site.data.keyword.Bluemix_notm}},
uma conta paralisada em um estado pendente etc. No entanto, em vários casos, é possível recuperar-se desses
problemas seguindo algumas etapas simples. 
{:shortdesc}

## Não é possível efetuar login no {{site.data.keyword.Bluemix_notm}}
{: #ts_unabletologin}

Deve-se ter uma conta válida do {{site.data.keyword.Bluemix_notm}} para efetuar login.


Ao tentar efetuar login no {{site.data.keyword.Bluemix_notm}}, você verá uma das mensagens de erro a seguir: 
{: tsSymptoms} 

 * No Portal do Cliente
  
   `You have reached this page because your authentication was successful, however, this IBMid is not associated with any IBM Cloud accounts. If you believe this to be in error, contact your Account Owner or Master User.`

 * No console do {{site.data.keyword.Bluemix_notm}}
  
  `You have reached this page because your authentication was successful, however, this IBMid is not associated with any  {{site.data.keyword.Bluemix_notm}} accounts.`


Uma das razões mais prováveis para obter esta mensagem de erro é que você ainda não tem uma conta do {{site.data.keyword.Bluemix_notm}} criada ou você precisa mudar para a autenticação do IBMid. 
{: tsCauses} 
 

Siga o processo de inscrição para criar uma conta do {{site.data.keyword.Bluemix_notm}} ou entre em contato com o usuário principal ou com o administrador da conta para alternar para o IBMid. 
{: tsResolve}

Dependendo de como sua conta foi configurada, algumas dessas opções de login podem se aplicar a você: 
 * Os usuários do SoftLayer com IDs do SoftLayer devem efetuar login por meio do [Portal do cliente ![Ícone de link externo](../icons/launch-glyph.svg)](https://control.softlayer.com){: new_window}.
 * Os usuários do SoftLayer com um IBMid e com ou sem uma conta do Bluemix vinculada podem efetuar login por meio do [Portal do cliente ![Ícone de link externo](../icons/launch-glyph.svg)](https://control.softlayer.com){: new_window} para abrir o Portal do cliente SoftLayer ou por meio do [console do Bluemix ![Ícone de link externo](../icons/launch-glyph.svg)](https://console.{DomainName}){: new_window} para abrir o painel Infraestrutura. 
 * Os usuários do Bluemix sem uma conta do SoftLayer vinculada devem efetuar login por meio do console do Bluemix.
 * Os usuários do Bluemix com uma conta do SoftLayer vinculada podem efetuar login por meio do [console do Bluemix ![Ícone de link externo](../icons/launch-glyph.svg)](https://console.{DomainName}){: new_window} ou do [Portal do cliente ![Ícone de link externo](../icons/launch-glyph.svg)](https://control.softlayer.com){: new_window}.
 

## A Senha é inválida
{: #ts_logintobm}

Deve-se ter um IBMid válido para efetuar login no console do {{site.data.keyword.Bluemix_notm}}.

Ao tentar efetuar login no {{site.data.keyword.Bluemix_notm}}, você verá a mensagem de erro a seguir: 
{: tsSymptoms} 

`A senha inserida não está correta.`

O IBMid e a senha que você usa para efetuar login no {{site.data.keyword.Bluemix_notm}} são inválidos.
{: tsCauses} 
 
Para obter um IBMid e uma senha válidos, acesse a página Meu perfil IBM e conclua uma das etapas a seguir:
{: tsResolve}
  * Se você já tiver se registrado para um IBMid e deseja verificar se seu ID e senha são válidos, clique em **Efetuar login** e insira seu IBMid e sua senha na página Efetuar login. Se você esqueceu sua senha, clique em **Esqueceu sua senha** na página de login para reconfigurá-la. Caso tenha esquecido
seu ID IBM ou continue a ter problemas com a senha, entre em contato com o Help desk de
registro IBM mundial para obter ajuda. 
  * Se você não tiver um IBMid, clique em **Registrar** para registrar um IBMid e uma senha. 



## Não é possível efetuar login com um nome de usuário do Softlayer
{: #ts_softlayer_username}

Deve-se ter um ID IBM e uma senha válidos para efetuar login no
{{site.data.keyword.Bluemix_notm}}.


Ao tentar efetuar login no console do {{site.data.keyword.Bluemix_notm}} com seu nome de usuário do Softlayer, você receberá a seguinte mensagem: 
{: tsSymptoms} 

`Nós não reconhecemos este IBMid ou e-mail. `

Deve-se ter um IBMid para efetuar login para usar o painel Infraestrutura no console do Bluemix.
{: tsCauses} 
 
Se você for um usuário do SoftLayer que está usando um ID do SoftLayer, deverá alternar para a autenticação do IBMid no Portal do Cliente dentro de cada conta que você tem acesso antes de ser capaz de efetuar login usando a autenticação do IBMid. 

Entre em contato com o usuário principal ou com o administrador da conta para alternar para o IBMid. 
{: tsResolve}



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

  
    
## O failover automático entre regiões do {{site.data.keyword.Bluemix_notm}}
não está disponível
{: #ts_failover}

Não é possível usar failover automático entre regiões do {{site.data.keyword.Bluemix_notm}}. No entanto, é possível usar um provedor de DNS que suporte failover entre vários
endereços IP como solução alternativa.
 

Quando um região do {{site.data.keyword.Bluemix_notm}} se torna indisponível, os apps em execução nessa região também ficam indisponíveis, ainda que os mesmos apps estejam em execução em outra região do {{site.data.keyword.Bluemix_notm}}.
{: tsSymptoms}

 
O {{site.data.keyword.Bluemix_notm}}
ainda não fornece failover automático de uma região para outra.
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



## A conta está pendente
{: #ts_accntpding}

Se sua conta estiver pendente, não será possível efetuar login no {{site.data.keyword.Bluemix_notm}}.

 
Depois de registrar em uma conta de avaliação do {{site.data.keyword.Bluemix_notm}},
talvez você não possa efetuar login no {{site.data.keyword.Bluemix_notm}}. Em vez disso, você verá a mensagem a seguir:
{: tsSymptoms}

<code>Sua conta está pendente. Aguarde até 24 horas pela confirmação por email e verifique também sua pasta de spam. Se você ainda não tiver recebido sua confirmação por e-mail, entre em contato com o <a href="http://ibm.biz/bluemixsupport.com" target="_blank">Suporte do Bluemix <img src="../icons/launch-glyph.svg" alt="Ícone de link externo"></a>.</code>


Depois de registrar em uma conta de avaliação do {{site.data.keyword.Bluemix_notm}},
você receberá um email de confirmação. Deve-se clicar no link
que está no email de confirmação para concluir o processo de registro.
{: tsCauses} 

O email de confirmação é enviado ao endereço de email fornecido. Verifique sua caixa de entrada e sua pasta de emails não desejados. Se você não tiver recebido o e-mail de confirmação, entre em contato com o [Suporte do {{site.data.keyword.Bluemix_notm}} ![Ícone de link externo](../icons/launch-glyph.svg)](http://ibm.biz/bluemixsupport.com){: new_window}.  
{: tsResolve}



## Não é possível incluir usuários em uma organização
{: #ts_adduser}

É possível convidar mais de um usuário para trabalhar sob a mesma organização. É possível convidar os usuários para a sua organização
somente se você for o proprietário da conta ou se for ambos, um gerente
e um membro da organização.
 

Não é possível ver o link **Convidar um novo usuário** em sua sessão
**Gerenciar organizações**. 
{: tsSymptoms}

 

Somente os usuários {{site.data.keyword.Bluemix_notm}} a seguir
podem convidar usuários para uma organização:
{: tsCauses}
  * O proprietário da conta da organização
  * Os gerenciadores de organização que também são membros, não colaboradores, da organização
  
No
{{site.data.keyword.Bluemix_notm}}, é possível ser um membro ou um colaborador de uma organização:

<dl><dt>Colaborador</dt>
<dd>Você é um colaborador de uma organização, se já tiver uma conta do {{site.data.keyword.Bluemix_notm}} e alguém
convidá-lo para a organização.</dd>
<dt>Membro</dt>
<dd>Você é um membro de uma organização, se não tiver uma conta do {{site.data.keyword.Bluemix_notm}}, mas então
alguém convidá-lo para a organização e você se inscrever para {{site.data.keyword.Bluemix_notm}} a partir do convite.</dd>
</dl>


Não é possível convidar os usuários para a sua organização, de for um colaborador da
organização, mesmo se tiver sido designado como um gerenciador da organização.

**Nota:** Todos os gerenciadores de organização, incluindo aqueles que são colaboradores de uma organização, podem incluir, modificar e remover os usuários que já estão na organização.

 

Se você não conseguir convidar os usuários para sua organização e precisar de uma função diferente
para fazer isso, entre em contato com o gerenciador da sua organização
para alterar a sua função. Para identificar o gerente da organização, conclua as
etapas a seguir:
{: tsResolve}

  1. Acesse o Painel do {{site.data.keyword.Bluemix_notm}}. Na barra de menus, clique no item de menu **Suporte** e clique em **Gerenciar organizações**.
  2. Acesse sua organização e visualize as informações sobre o gerente da organização na guia **USUÁRIOS**.  
  
Se você não conseguir convidar os usuários porque é um colaborador
e não um membro, deve-se excluir a conta anterior do {{site.data.keyword.Bluemix_notm}}
e, em seguida, ser convidado para se associar como um membro da organização. Para excluir sua conta anterior e se associar à conta como um membro,
conclua as etapas a seguir: 

  1. Entre em contato com o [Suporte do {{site.data.keyword.Bluemix_notm}} ![Ícone de link externo](../icons/launch-glyph.svg)](http://ibm.biz/bluemixsupport){: new_window} para abrir um chamado de suporte e solicitar a exclusão de sua conta. Se houver dados associados
à sua conta antiga que você deseja salvar e mover para a nova conta,
inclua essas informações em seu email. 
  2. Após sua conta ser excluída, peça a um usuário com a função de gerenciador
de organização para convidá-lo para a organização como um gerenciador de organização. Em seguida, inscreva-se no {{site.data.keyword.Bluemix_notm}} a partir do convite. 




## O registro em lote de usuários não é suportado
{: #ts_batchregistration}

Ao
registrar usuários para {{site.data.keyword.Bluemix_notm}},
deve-se registrar cada usuário individualmente.
 

O {{site.data.keyword.Bluemix_notm}} não
fornece a capacidade para registrar diversos usuários ao mesmo tempo.
{: tsSymptoms}
 

O {{site.data.keyword.Bluemix_notm}} não suporta registro de lote de usuários. Para registrar usuários para o {{site.data.keyword.Bluemix_notm}},
deve-se registrar cada usuário individualmente.
{: tsCauses}
 

Para registrar vários usuários para o {{site.data.keyword.Bluemix_notm}},
deve-se concluir as etapas a seguir para cada usuário:
{: tsResolve}

  1. Clique em **INSCREVER-SE** no console do {{site.data.keyword.Bluemix_notm}}.
  2. Conclua as etapas seguindo o assistente.

    

## A página do {{site.data.keyword.Bluemix_notm}} não pode ser carregada
{: #ts_err}

Ao usar o console do {{site.data.keyword.Bluemix_notm}}, você pode não ser capaz de carregar uma página do {{site.data.keyword.Bluemix_notm}}. Em vez disso, talvez você veja as mensagens de erro BXNUI0001E ou BXNUI0016E.
 

É possível ver uma das mensagens de erro a seguir ao usar o console do {{site.data.keyword.Bluemix_notm}}:
{: tsSymptoms}

`BXNUI0001E: A página não foi carregada, pois o Bluemix não detectou se existe uma sessão.`


`BXNUI0016E: Os apps e serviços não foram recuperados, pois uma página do Bluemix não foi carregada.`

 
É possível concluir uma ou mais das ações
a seguir, conforme for necessário:
{: tsResolve}

  * Atualizar ou reiniciar seu navegador.
  * Efetuar logout do {{site.data.keyword.Bluemix_notm}} e
efetuar login novamente.
  * Usar o modo de navegação privada do seu navegador. 
  * Limpar os cookies e o cache do navegador.
  * Usar um navegador diferente. Para obter informações sobre as versões dos navegadores que são suportadas pelo {{site.data.keyword.Bluemix_notm}}, veja [Pré-requisitos do {{site.data.keyword.Bluemix_notm}} ![Ícone de link externo](../icons/launch-glyph.svg)](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}.
  * Se você tiver instalado a interface de linha de comandos cf, insira o comando `cf apps` para ver se seu aplicativo está em execução.
  
  
  
  
  

