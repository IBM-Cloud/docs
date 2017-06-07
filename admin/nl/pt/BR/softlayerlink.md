---



copyright:

  years: 2016, 2017
lastupdated: "2017-03-17"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Alternando para o IBMid
A autenticação no SoftLayer agora usa o IBMid para fornecer um único login para todos os {{site.data.keyword.Bluemix_notm}}. As contas existentes do SoftLayer estão sendo ativadas para alternar para a autenticação do IBMid. Um assistente de migração fornece orientação durante essa alternância. 
{:shortdesc}

Ao iniciar o processo para alternar para um IBMid, sempre será possível cancelar antes de concluir o processo. No entanto, sempre que você efetuar login, o prompt para alternar para um IBMid será exibido. Cada conta do SoftLayer que você planejar vincular a uma conta do {{site.data.keyword.Bluemix_notm}} deverá pertencer a um IBMid exclusivo com um endereço de e-mail exclusivo.

Para alternar sua conta existente do SoftLayer para um IBMid, conclua as etapas a seguir:
1. Efetue login na conta do SoftLayer e clique em **OK** quando o prompt para alternar para um IBMid for exibido.

   Se você for um usuário principal e um prompt para alternar para um IBMid não for exibido no {{site.data.keyword.slportal}}, [Entre em contato com o suporte IBM](/docs/support/index.html#contacting-support) para obter ajuda.
  
   Se anteriormente você tiver efetuado login e tiver clicado em **Posteriormente** no prompt, mas desejar alternar para a autenticação do IBMid na sessão atual, acesse a página Editar perfil do usuário e clique em **Alternar para IBMid**.

2. Siga os prompts do assistente para criar seu IBMid. 

   Insira um endereço de e-mail que não esteja atualmente sendo usado por nenhum IBMid. Esse endereço de e-mail é usado como o nome de usuário para o novo IBMid e é onde seu código de registro é enviado após a criação do IBMid. Será possível atualizar o endereço de e-mail que está associado ao IBMid posteriormente, mas não será possível mudar o nome de usuário.

3. Ao receber seu código de registro, clique no link no e-mail ou copie a URL em um navegador e insira seu código de registro.

   O código de registro é válido por sete dias e pode ser usado apenas uma vez.
  
4. Depois de enviar seu código de registro, use seu IBMid para efetuar login no {{site.data.keyword.slportal}}.

   No prompt Login da conta, acesse a seção **Login da conta IBMid** e clique em **Efetuar login com o IBMid**. Não use os campos **Nome do usuário** e **Senha** que foram usados anteriormente com seu ID do SoftLayer.

Se você for um novo cliente, será solicitado a informar seu IBMid existente ou a criar um novo IBMid quando efetuar check-out da ordem. 
  * Para usar um IBMid existente, insira o nome de usuário ou o endereço de e-mail do IBMid se ele for exclusivo (ou seja, não é compartilhado entre diversos IBMids).
  
  * Para criar um novo IBMid, insira um endereço de e-mail que não esteja atualmente em uso por nenhum IBMid. Esse endereço de e-mail é o nome de usuário do IBMid e é onde seu código de registro é enviado após a criação do IBMid. Será possível atualizar o endereço de e-mail que está associado ao IBMid posteriormente, mas não será possível mudar o nome de usuário. 
  
Para resolver os problemas ao efetuar login com o IBMid, veja [Resolução de problemas para acessar o Bluemix](/docs/troubleshoot/ts_accessing.html#accessing).

## Ativando contas do usuário para autenticação do IBMid
{: #link_accounts_resellers}

Em alguns casos, antes que um usuário possa alternar para um IBMid, um revendedor ou distribuidor deve ativar a conta para usar a autenticação do IBMid. 

  * A autenticação do IBMid deve ser ativada para cada conta de usuário existente que você deseja vincular a uma conta do Bluemix. Em seguida, cada usuário deverá concluir o processo para alternar para um IBMid usando o assistente de migração, conforme descrito na seção anterior. Entre em contato com o [Suporte IBM](/docs/support/index.html#contacting-support) para ativar uma conta existente do SoftLayer para usar a autenticação do IBMid. 
  
  * Para assegurar-se de que novas contas de usuário sejam criadas com um IBMid, o atributo `CREATE_NEW_ACCOUNT_WITH_IBMid_AUTHENTICATION` deve ser configurado na conta de usuário principal imediata. Entre em contato com o [Suporte IBM](/docs/support/index.html#contacting-support) ou com seu fornecedor para configurar o atributo para suas contas.  

## Vinculando as contas de usuário IBMid
{: #link_user_accounts}

Depois que as contas de usuário são alternadas para a autenticação de IBMid, os revendedores e distribuidores podem vincular as contas do SoftLayer e do {{site.data.keyword.Bluemix_notm}} para usar os recursos combinados de infraestrutura e plataforma.

**Nota**:
  * O usuário principal da conta que está sendo vinculada deve ter um IBMid.
  * Cada conta do usuário que você vincular a uma conta do {{site.data.keyword.Bluemix_notm}} deverá pertencer a um IBMid exclusivo com um endereço de e-mail exclusivo. Embora um único IBMid possa ter múltiplas contas do SoftLayer, deve-se mudar o usuário principal para ser um IBMid exclusivo para cada conta. Entre em contato com o [Suporte do IBM SoftLayer ![Ícone de link externo](../icons/launch-glyph.svg)](https://knowledgelayer.softlayer.com/topic/support){: new_window} para mudar o usuário principal de uma conta do SoftLayer.
  * Ao incluir novos usuários em uma conta vinculada, deve-se incluí-los na conta do SoftLayer e do {{site.data.keyword.Bluemix_notm}} para que possam acessar todos os recursos do console unificado. 
  
Conclua as etapas a seguir para vincular cada conta a uma conta do {{site.data.keyword.Bluemix_notm}}:
1. Para vincular a uma conta existente do {{site.data.keyword.Bluemix_notm}} ou para criar uma nova, efetue login em sua conta do SoftLayer como o usuário principal e clique no link do {{site.data.keyword.Bluemix_notm}}.

   O IBMid que é o usuário principal da conta do SoftLayer deve ser o proprietário da conta do {{site.data.keyword.Bluemix_notm}} à qual você está se vinculando. 
   
2. Siga os prompts do assistente, incluindo a inclusão de usuários da conta do SoftLayer na conta do {{site.data.keyword.Bluemix_notm}}.
3. Depois de vincular a conta, informe ao usuário final de cada conta para migrar para o IBMid seguindo o procedimento descrito na seção anterior.

**Recomendação**: migre apenas as contas do usuário final para o IBMid. Não migre contas da marca, que são contas pai para contas do usuário final e não contêm recursos. Os usuários de conta da marca que migram para o IBMid perdem a capacidade de efetuar login no Brand Agent Portal (BAP).  
  
