---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-03-02"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 



# Resolução de problemas para acessar o {{site.data.keyword.Bluemix_notm}} 
{: #accessing}


Problemas gerais ao acessar o {{site.data.keyword.Bluemix}} podem incluir dificuldades em efetuar login no {{site.data.keyword.Bluemix_notm}} ou em uma conta que está em um estado pendente. Em muitos casos, é possível recuperar-se desses problemas seguindo algumas etapas simples.
{:shortdesc}

## Não é possível efetuar login no {{site.data.keyword.Bluemix_notm}}: senha incorreta
{: #ts_logintobm}

Deve-se ter uma senha válida que esteja associada a seu IBMid para efetuar login no console do {{site.data.keyword.Bluemix_notm}}.

Deve-se ter uma senha válida que esteja associada a seu IBMid ou ID do SoftLayer para efetuar login por meio do [Portal do cliente](https://control.softlayer.com).

Ao tentar efetuar login no {{site.data.keyword.Bluemix_notm}}, a mensagem de erro a seguir será exibida:
{: tsSymptoms} 

`A senha inserida não está correta.`

O IBMid e a senha que são usados para efetuar login no {{site.data.keyword.Bluemix_notm}} não são válidos.
{: tsCauses} 
 
Use uma das soluções a seguir:
{: tsResolve}
 * Digite a senha correta. Para verificar se seu IBMid e senha são válidos, é possível acessar a página Meu perfil IBM, clicar em **Efetuar login** e inserir seu IBMid e senha na página Efetuar login. 
 * Caso tenha esquecido sua senha, clique em **Esqueceu sua senha** para reconfigurar sua senha. Em seguida, retorne para o [console do Bluemix](https://console.{DomainName}) ou para o [Portal do cliente](https://control.softlayer.com) e efetue login novamente.
 * Caso tenha esquecido seu IBMid ou continue tendo problemas com a senha, entre em contato com o Help desk de registro IBM mundial para obter ajuda. 
 * Para obter um IBMid e uma senha válidos, acesse a página Meu perfil IBM e, em seguida, clique em **Registrar**.
  
**Nota:** se você estiver na página Conectar à IBM e o processo de login for interrompido por algum motivo (por exemplo, reconfiguração de senha), retorne para o [console do Bluemix](https://console.{DomainName}) ou para o [Portal do cliente](https://control.softlayer.com) e inicie o processo de login novamente.
 

## Não é possível efetuar login no {{site.data.keyword.Bluemix_notm}}: credenciais de login inválidas
{: #ts_login_invalid_credentials}

Ao efetuar login usando seu IBMid, a mensagem a seguir é exibida:
{: tsSymptoms}

`Credenciais de login inválidas fornecidas. Se você tiver um IBMid associado à sua conta, efetue login aqui` 

* Você alternou para um IBMid, mas tentou efetuar login por meio do [Portal do cliente](https://control.softlayer.com) usando seu nome de usuário e senha anteriores do SoftLayer.
{: tsCauses}

* Você tentou efetuar login por meio do [Portal do cliente](https://control.softlayer.com), mas inseriu seu IBMid e senha nos campos Nome de usuário e Senha. 

Clique em **efetuar login aqui** na mensagem ou acesse a seção Login da conta IBMid e clique em **Efetuar login com o IBMid**.
{: tsResolve}

Não use os campos **Nome do usuário** e **Senha** que foram usados com o ID anterior do Softlayer.


## Não é possível efetuar login no {{site.data.keyword.Bluemix_notm}}: IBMid ou e-mail não reconhecido
{: #ts_softlayer_username}

Ao efetuar login no console do {{site.data.keyword.Bluemix_notm}}, a mensagem a seguir será exibida:
{: tsSymptoms} 

`Nós não reconhecemos este IBMid ou e-mail. `

Você tentou efetuar login no console do {{site.data.keyword.Bluemix_notm}}, mas não usou um IBMid válido. Por exemplo, você não inseriu um endereço de e-mail completo para o IBMid ou tentou usar um nome de usuário e uma senha do SoftLayer.
{: tsCauses}
 
Deve-se ter um ID IBM e uma senha válidos para efetuar login no
{{site.data.keyword.Bluemix_notm}}.

 * Assegure-se de inserir um endereço de e-mail completo para o IBMid.
 {: tsResolve}
 * No caso de um usuário do SoftLayer com um ID do SoftLayer, deve-se alternar para a autenticação do IBMid no Portal do cliente em cada conta à qual tiver acesso antes de ser possível efetuar login usando a autenticação do IBMid.
 Para obter mais informações, veja [Alternando para o IBMid](/docs/admin/softlayerlink.html#ibmid_switch).


## Não é possível efetuar login no {{site.data.keyword.Bluemix_notm}}: o IBMid não está associado a nenhuma conta do IBM Cloud
{: #ts_login_noswitch}

Ao efetuar login usando seu IBMid, a mensagem a seguir é exibida:
{: tsSymptoms}

`You have reached this page because your authentication was successful, however, this IBMid is not associated with any IBM Cloud accounts. If you believe this to be in error, contact your Account Owner or Master User.`

Você efetuou login por meio do [Portal do cliente](https://control.softlayer.com) com um IBMid válido, mas não alternou para a autenticação do IBMid no SoftLayer.
{: tsCauses} 
 
Conclua as verificações a seguir, conforme apropriado:
{: tsResolve}
 * Entre em contato com o usuário principal ou com o administrador da conta para verificar se você está ativado para alternar para a autenticação do IBMid.
 * Assegure-se de concluir a etapa Alternar para o IBMid na conta do Softlayer. Veja [Alternando para o IBMid](/docs/admin/softlayerlink.html#ibmid_switch).
 * Assegure-se de seguir as ações no e-mail **Associar o usuário do SoftLayer a um IBMid**. Verifique o e-mail em sua caixa de entrada e sua pasta de spam. Para obter o e-mail novamente, por exemplo, se ele tiver expirado, acesse a página Editar perfil do usuário no Portal de controle e clique em **Reenviar e-mail**. Como alternativa, entre em contato com o [Suporte do {{site.data.keyword.Bluemix_notm}} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](http://ibm.biz/bluemixsupport.com){: new_window}.

**Nota:** se tiver criado seu IBMid diretamente com o IBMid, você receberá dois e-mails para processar; um do registro do IBMid e um do Softlayer. Assegure-se de seguir as ações dos dois e-mails.

Dependendo de como sua conta foi configurada, algumas dessas opções de login podem se aplicar a você: 
 * Os usuários do SoftLayer com IDs do SoftLayer devem efetuar login por meio do [Portal do Cliente](https://control.softlayer.com).
 * Os usuários do SoftLayer com um IBMid e com ou sem uma conta do Bluemix vinculada podem efetuar login por meio do [Portal do Cliente](https://control.softlayer.com) para abrir o Portal do Cliente SoftLayer ou por meio do [console do Bluemix](https://console.{DomainName}) para abrir o painel Infraestrutura. 


## Não é possível efetuar login no {{site.data.keyword.Bluemix_notm}}: o IBMid não está associado a nenhuma conta do {{site.data.keyword.Bluemix_notm}}
{: #ts_unabletologin}

Ao efetuar login no {{site.data.keyword.Bluemix_notm}}, a mensagem a seguir é exibida:
{: tsSymptoms} 
 
`You have reached this page because your authentication was successful, however, this IBMid is not associated with any  {{site.data.keyword.Bluemix_notm}} accounts.`

Você efetuou login por meio do [console do Bluemix](https://console.{DomainName}) com um IBMid válido, mas ainda não tem uma conta criada do {{site.data.keyword.Bluemix_notm}}.
{: tsCauses} 

Para criar uma conta do {{site.data.keyword.Bluemix_notm}}, siga o processo de inscrição.
{: tsResolve}

Dependendo de como sua conta foi configurada, algumas dessas opções de login podem se aplicar a você: 
 * Os usuários do Bluemix sem uma conta do SoftLayer vinculada devem efetuar login por meio do console do Bluemix.
 * Os usuários do Bluemix com uma conta do SoftLayer vinculada podem efetuar login por meio do [console do Bluemix](https://console.{DomainName}) ou do [Portal do Cliente](https://control.softlayer.com).
 

## Não é possível efetuar login no {{site.data.keyword.Bluemix_notm}}: o console não abre
{: #ts_login_stalls}

Ao efetuar login usando seu IBMid, uma mensagem de êxito de login será exibida, mas você não retornará para o [console do Bluemix](https://console.{DomainName}) ou para o [Portal do cliente](https://control.softlayer.com).
{: tsSymptoms}

Use uma das soluções a seguir:
{: tsResolve}
 * Feche seu navegador, limpe o cache e os cookies e, em seguida, tente efetuar login novamente.
 * Assegure-se de efetuar login por meio do [console do Bluemix](https://console.{DomainName}) ou do [Portal do cliente](https://control.softlayer.com), em vez de diretamente do serviço de autenticação do IBMid.
 
 
## Não é possível efetuar login no {{site.data.keyword.Bluemix_notm}}: o login do IBMid não é concluído
{: #ts_login_ibmid}

Ao efetuar login no {{site.data.keyword.Bluemix_notm}}, a autenticação com o IBMid não é concluída.
{: tsSymptoms}

Pode haver um problema com o serviço de autenticação do IBMid.
{: tsCauses}

Verifique o status do serviço em [IBM BlueID ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://new.wind.ibmcloud.com/webapp/#/status/a1a0c5d743d94a6a9597087541564d8e){: new_window} e, em seguida, tente novamente.
{: tsResolve}


## Não é possível efetuar login no {{site.data.keyword.Bluemix_notm}}: a conta está pendente
{: #ts_accntpding}

Se a sua conta estiver pendente, não será possível efetuar login no {{site.data.keyword.Bluemix_notm}}.
 
Depois de registrar em uma conta de avaliação do {{site.data.keyword.Bluemix_notm}},
talvez você não possa efetuar login no {{site.data.keyword.Bluemix_notm}}. É exibida a seguinte mensagem:
{: tsSymptoms}

<code>Sua conta está pendente. Aguarde até 24 horas pela confirmação por email e verifique também sua pasta de spam. Se você ainda não tiver recebido sua confirmação por e-mail, entre em contato com o <a href="http://ibm.biz/bluemixsupport.com" target="_blank">Suporte do Bluemix</a>.</code>

Depois de registrar em uma conta de avaliação do {{site.data.keyword.Bluemix_notm}},
você receberá um email de confirmação. Deve-se clicar no link
que está no email de confirmação para concluir o processo de registro.
{: tsCauses} 

O email de confirmação é enviado ao endereço de email fornecido. Verifique sua caixa de entrada e sua pasta de spam. Se você não tiver recebido o e-mail de confirmação, entre em contato com o [Suporte do {{site.data.keyword.Bluemix_notm}} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](http://ibm.biz/bluemixsupport.com){: new_window}.  
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
  
    
## O failover automático entre regiões do {{site.data.keyword.Bluemix_notm}} não está disponível
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

## Não é possível incluir usuários em uma organização
{: #ts_adduser}

É possível convidar mais de um usuário para trabalhar sob a mesma organização. É possível convidar os usuários para a sua organização
somente se você for o proprietário da conta ou se for ambos, um gerente
e um membro da organização.
 
Não é possível ver o link **Convidar um novo usuário** na seção **Gerenciar organizações**.
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

Não será possível convidar usuários para a sua organização, se você for um colaborador da organização, mesmo se tiver sido designado como um gerenciador da organização.

**Nota:** Todos os gerenciadores de organização, incluindo aqueles que são colaboradores de uma organização, podem incluir, modificar e remover os usuários que já estão na organização.

Se não puder convidar usuários para sua organização e precisar de uma função diferente para fazer isso, entre em contato com o gerenciador de sua organização para mudar sua função. Para identificar o gerente da organização, conclua as
etapas a seguir:
{: tsResolve}

  1. Acesse o Painel do {{site.data.keyword.Bluemix_notm}}. Na barra de menus, clique no item de menu **Conta** e clique em **Gerenciar organizações**.
  2. Acesse sua organização e visualize as informações sobre o gerente da organização na guia **USUÁRIOS**.  
  
Se não puder convidar usuários porque é um colaborador e não um membro, sua conta anterior do {{site.data.keyword.Bluemix_notm}} deverá ser excluída e você convidado para se associar à conta, em seguida, como um membro da organização. Para excluir sua conta anterior e se associar à conta como um membro,
conclua as etapas a seguir: 

  1. Entre em contato com o [Suporte do {{site.data.keyword.Bluemix_notm}} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](http://ibm.biz/bluemixsupport){: new_window} para abrir um chamado de suporte e solicitar a exclusão de sua conta. Se houver dados associados
à sua conta antiga que você deseja salvar e mover para a nova conta,
inclua essas informações em seu email. 
  2. Após sua conta ser excluída, peça a um usuário com a função de gerenciador
de organização para convidá-lo para a organização como um gerenciador de organização. Em seguida, inscreva-se no {{site.data.keyword.Bluemix_notm}} a partir do convite. 

## O registro em lote de usuários não é suportado
{: #ts_batchregistration}

Ao
registrar usuários para {{site.data.keyword.Bluemix_notm}},
deve-se registrar cada usuário individualmente.

O {{site.data.keyword.Bluemix_notm}} não fornece a capacidade para registrar múltiplos usuários ao mesmo tempo.
{: tsSymptoms}
 
O {{site.data.keyword.Bluemix_notm}} não suporta registro de lote de usuários. Para registrar usuários para o {{site.data.keyword.Bluemix_notm}},
deve-se registrar cada usuário individualmente.
{: tsCauses}
 
Para registrar múltiplos usuários para o {{site.data.keyword.Bluemix_notm}}, conclua as etapas a seguir para cada usuário:
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

Conclua uma ou mais das ações a seguir, conforme necessário:
{: tsResolve}

  * Atualizar ou reiniciar seu navegador.
  * Efetuar logout do {{site.data.keyword.Bluemix_notm}} e
efetuar login novamente.
  * Usar o modo de navegação privada do seu navegador. 
  * Limpar os cookies e o cache do navegador.
  * Usar um navegador diferente. Para obter informações sobre as versões dos navegadores que são suportados pelo {{site.data.keyword.Bluemix_notm}}, veja [Pré-requisitos do Bluemix](/docs/overview/whatisbluemix.html#prereqs).
  * Se você tiver instalado a interface de linha de comandos cf, insira o comando `cf apps` para ver se seu app está em execução.
