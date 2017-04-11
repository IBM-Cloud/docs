---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-01-10"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 


# Resolução de problemas para gerenciamento de contas 
{: #managingaccounts}

Os problemas gerais ao gerenciar sua conta podem incluir apps diferentes que compartilham o mesmo nome de domínio ou administradores que não podem visualizar todas as organizações. Em muitos casos, é possível recuperar-se desses problemas seguindo algumas etapas simples.
{:shortdesc}


## A conta está inativa
{: #ts_accnt_inactive}

Não será possível criar um app no {{site.data.keyword.Bluemix_notm}} se a sua conta estiver inativa. Deve-se entrar em contato com a equipe de suporte para corrigir esse problema.

Ao tentar criar um app no {{site.data.keyword.Bluemix_notm}}, você vê a mensagem de erro a seguir:
{: tsSymptoms} 

`BXNUI0096E: O app não foi criado. Sua conta está inativa porque ela foi cancelada
ou suspensa.`

O status de sua conta do {{site.data.keyword.Bluemix_notm}} torna-se inativo quando a conta é cancelada ou suspensa.
{: tsCauses}


Para reativar sua conta, entre em contato com o [Suporte do {{site.data.keyword.Bluemix_notm}} ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](http://ibm.biz/bluemixsupport.com){: new_window}. Inclua as informações a seguir no e-mail:
{: tsResolve}

  * O ID IBM que você usa para efetuar login no {{site.data.keyword.Bluemix_notm}}.
  * O nome da organização em que seu app está sendo criado. Essas informações podem ajudar a equipe de suporte a determinar se você está designado às funções ou associação corretas em sua organização.


## Nenhum espaço está associado com a sua organização atual
{: #ts_no_space}

Não será possível criar um aplicativo se não houver espaço associado à sua organização atual.

Ao tentar criar um app no {{site.data.keyword.Bluemix_notm}}, você vê a mensagem de erro a seguir:
{: tsSymptoms} 

`BXNUI0097E: Para que seja possível incluir um app, pelo menos um espaço deve estar associado à sua organização e região. No Painel, clique em Criar um espaço. Quando o espaço for criado, tente novamente. `

Os apps no {{site.data.keyword.Bluemix_notm}} devem ser criados em um espaço em sua organização.
{: tsCauses} 

Para criar um espaço, use um dos métodos a seguir: 
{: tsResolve}
 
  * No Painel do {{site.data.keyword.Bluemix_notm}}, selecione a organização em que você deseja criar o espaço, em seguida, clique em **Criar um espaço**.
  * Na interface de linha de comandos cf, digite `cf create-space <space_name> -o <organization_name>`.

  
## Os apps compartilham o mesmo nome de domínio
{: #ts_domain_diff}

É possível observar que vários apps compartilham a mesma URL no {{site.data.keyword.Bluemix_notm}}.

Esse problema pode ocorrer quando você designa a mesma rota de URL a diferentes apps em um espaço.
{: tsCauses}

Por exemplo, você envia por push o app myApp1 para o {{site.data.keyword.Bluemix_notm}} e configura o domínio como "mynewapp.stage1.mybluemix.net". Em seguida, você envia por push outro app myApp2 para o mesmo espaço e configura uma de suas rotas de URL como "mynewapp.stage1.mybluemix.net". A rota agora é mapeada para ambos os apps.

Esse é o comportamento suportado do {{site.data.keyword.Bluemix_notm}} e é possível usar essa prática para atingir o tempo de inatividade zero para o upgrade de seu app. Para obter mais informações, veja [Usando a implementação blue-green para reduzir o tempo de inatividade e o risco ![Ícone de link externo](../icons/launch-glyph.svg "Ícone de link externo")](https://docs.cloudfoundry.org/devguide/deploy-apps/blue-green.html){: new_window}.
{: tsResolve}
  

## Os administradores não podem visualizar todas as organizações usando a interface com o usuário do {{site.data.keyword.Bluemix_notm}}
{: #ts_ui_org}

Como administrador, quando você utiliza a interface com o usuário do
{{site.data.keyword.Bluemix_notm}}, não é possível exibir cada organização para
administrá-las. Você pode exibir e administrar apenas as organizações às quais pertence.

Como administrador, não é possível ver todas as organizações usando a interface com o usuário do {{site.data.keyword.Bluemix_notm}}.
{: tsSymptoms}

Essa é uma limitação da interface com o usuário do {{site.data.keyword.Bluemix_notm}}.
{: tsCauses}

É possível usar comandos, como `cf orgs`, `cf create-org` e `cf delete-org` da interface da linha de comandos cf para gerenciar todas as organizações. Para obter uma lista completa de
comandos cf, insira `cf help`.
{: tsResolve}
	
## O cartão de crédito não pode ser incluído
{: #ts_addcc}

Não é possível enviar suas informações de cartão de crédito para converter sua conta para teste em uma conta Pré-pago.

O botão **Enviar** na página Incluir cartão de crédito está desativado.
{: tsSymptoms}

Esse problema acontece quando suas informações não são preenchidas corretamente na página Incluir cartão de crédito.
{: tsCauses}


Conclua
as etapas a seguir:
{: tsResolve}

  1. Na página Incluir cartão de crédito, preencha todos os campos obrigatórios nas seções de informações de contato, endereço de contato e endereço para cobrança.
  2. Selecione **Eu li e concordo com os Termos e Condições da IBM**,
em seguida, clique em **Enviar**. A seção **Selecionar um método de pagamento** é exibida.
  3. Insira seu número do cartão de crédito, a data de validade de seu cartão e o código de segurança no cartão. Em seguida, clique em **Enviar**.
