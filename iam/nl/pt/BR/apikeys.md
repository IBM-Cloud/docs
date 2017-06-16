---

copyright:

  years: 2015, 2017
lastupdated: "2017-05-10"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Gerenciando chaves API
{: #manapikey}

Uma chave de interface de programação de aplicativos (chave API) é um código passado por programas de computador que chama uma interface de programação de aplicativos (API) para identificar o programa de chamada, seu desenvolvedor ou seu usuário para o website. As chaves API são usadas para rastrear e controlar como a API está sendo usada, por exemplo, para evitar uso malicioso ou abuso da API (conforme definido talvez pelos termos de serviço). A chave API age muitas vezes como um identificador exclusivo e um token secreto para autenticação e geralmente tem um conjunto de direitos de acesso na API associada a ela. As chaves API podem basear-se no sistema de identificador exclusivo universal (UUID) para assegurar que sejam exclusivas para cada usuário.

Como um usuário do {{site.data.keyword.Bluemix_notm}}, talvez você queira usar uma chave API quando ativar um programa ou um script sem distribuir sua senha para o script. É possível que um benefício de uso de uma chave API seja que um usuário ou uma organização possa criar várias chaves API para diferentes programas e que as chaves API poderão ser excluídas independentemente se comprometidas sem interferir com outras chaves API ou até mesmo com o usuário. Além disso, como um [usuário federado](/docs/admin/adminpublic.html#federatedid), é possível usar uma chave API para efetuar login. Para obter mais informações sobre como usar uma chave API para efetuar login, veja a documentação do [comando `bluemix login` da CLI do {{site.data.keyword.Bluemix_notm}}](/docs/cli/reference/bluemix_cli/bx_cli.html#bluemix_login) e o [comando `cf login` da CLI cf](/docs/cli/reference/cfcommands/index.html#cf_login).

É possível gerenciar suas chaves API do {{site.data.keyword.Bluemix_notm}} na janela Chaves API do Bluemix. Acesse **Gerenciar** &gt; **Segurança** &gt; **Chaves API do Bluemix** para ver uma lista de suas chaves API com descrições e datas. É possível criar, editar ou excluir chaves API por meio dessa página.

Para criar uma chave API:

1. Acesse **Gerenciar** &gt; **Segurança** &gt; **Chaves API do Bluemix**.
2. Clique em **Criar chave API**.
3. Insira um nome e uma descrição para sua chave API.
4. Clique em **Criar chave API**.
5. Em seguida, clique em **Mostrar** para exibir a chave API para copiá-la e salvá-la para mais tarde ou clique em **Fazer download da chave API**.

**Nota**: a chave API só está disponível para exibição ou download no momento da criação. Se a chave API for perdida, uma nova chave API deverá ser criada.

Para editar uma chave API:

1. Acesse **Gerenciar** &gt; **Segurança** &gt; **Chaves API do Bluemix**.
2. No menu **Ações** de uma chave API listada na tabela, clique em **Editar o nome e a descrição** 
3. Atualize as informações de sua chave API.
4. Clique em **Atualizar chave API**.

Para excluir uma chave API: 

1. Acesse **Gerenciar** &gt; **Segurança** &gt; **Chaves API do Bluemix**.
2. No menu **Ações** de uma chave API listada na tabela, clique em **Excluir**.
3. Em seguida, confirme a exclusão clicando em **Excluir chave**.

Também será possível usar a CLI do {{site.data.keyword.Bluemix_notm}} para gerenciar suas chaves API listando suas chaves, criando chaves, atualizando chaves ou excluindo chaves. Veja a seção do comando [`bluemix iam api-keys`](/docs/cli/reference/bluemix_cli/bx_cli.html#bluemix_iam) para obter mais informações.

