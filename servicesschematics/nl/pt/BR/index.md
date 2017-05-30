---

copyright:
  years: 2017
lastupdated: "2017-05-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Introdução ao {{site.data.keyword.bpfull_notm}} (Beta)
{: #gettingstarted}

O {{site.data.keyword.bplong}} é uma ferramenta de automação que pode ser usada para definir e implementar sua infraestrutura em nuvem como uma única unidade e reutilizar essas definições de recurso em nuvem em qualquer número de ambientes.
{:shortdesc}

O {{site.data.keyword.bpshort}} usa o Terraform, da HashiCorp, para codificar a infraestrutura. Os componentes de sua infraestrutura são divididos em recursos individuais, que podem ser qualquer coisa, de hardware físico a contas do usuário. Ao abstrair recursos de alto e de baixo nível, será possível tratar sua infraestrutura como você trata seu software, como código. 

Ao trabalhar com o {{site.data.keyword.bpshort}}, você grava configurações para seu ambiente em sintaxe declarativa. Você indica como deseja a aparência de seu ambiente, como tendo 10 {{site.data.keyword.virtualmachinesshort}} em produção. O serviço compara sua configuração com o que o Terraform criou anteriormente e inclui ou remove recursos, conforme necessário.

O {{site.data.keyword.bpshort}} é uma ferramenta colaborativa do DevOps que fornece uma fonte isolada de verdade para a infraestrutura. É possível armazenar configurações do ambiente no controle de versão, dando à sua equipe a capacidade de conduzir revisões de código, definir a versão de sua infraestrutura, controlar as mudanças por meio do histórico de confirmação e reverter as mudanças mais facilmente.

O {{site.data.keyword.bpshort}} fica automaticamente disponível a todos os usuários em sua conta do {{site.data.keyword.Bluemix_notm}}.


## Criando uma Configuração
{: #configuration}

Ao criar uma configuração, você está codificando os recursos em nuvem que compõem seu ambiente.
{:shortdesc}


Se desejar experimentar uma configuração de amostra com o {{site.data.keyword.bpshort}}, conclua as etapas a seguir. Na amostra, é possível provisionar uma chave SSH para usar no {{site.data.keyword.BluSoftlayer}}. 

**Nota:** a configuração de amostra requer uma conta do {{site.data.keyword.BluSoftlayer}}. Veja a [vinculação do doc de suas contas do {{site.data.keyword.Bluemix_notm}} e do SoftLayer](../../pricing/linking_accounts.html#unifyingaccounts) se você tiver uma conta existente ou será possível [inscrever-se para uma conta](https://console.ng.bluemix.net/docs/pricing/index.html#pay-accounts).

1. Gere um par de chaves SSH localmente.
  ```
  ssh-keygen -t rsa
  ```
  {:codeblock}

2. Bifurque a configuração de amostra no <a href="https://github.com/IBM-Bluemix/tf-bluemix-ssh-key" target="_blank">GitHub <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>. 

  Os exemplos a seguir mostram os diferentes tipos de blocos que estão na configuração de amostra. É possível ver a configuração completa no arquivo `main.tf` do repositório GitHub.
  
  * O bloco do provedor configura o provedor {{site.data.keyword.IBM_notm}} Cloud e as credenciais de login.

    ```
    provider "ibmcloud" {
      ibmid                    = "${var.ibmid}"
      ibmid_password           = "${var.ibmidpw}"
      softlayer_account_number = "${var.slaccountnum}"
    }
    ```
    {:screen}
  
  * O bloco de recurso define um componente de sua infraestrutura, que nesta amostra é uma chave SSH.
  
    ```
    resource "ibmcloud_infra_ssh_key" "ssh_key" {
      label = "${var.key_label}"
      notes = "${var.key_note}"
      public_key = "${var.public_key}"
    }
    ```
    {:screen}
  
  * O bloco de variáveis define suas variáveis, que podem ser inseridas na GUI do {{site.data.keyword.bpshort}} para esta amostra.
  
    ```
    variable ibmid {
      type = "string"
      description = "Your IBM-ID."
    }
    ```
    {:screen}
  
  * O bloco de saída define o que será exibido na saída do Terraform depois que a configuração for usada para criar seu ambiente e o recurso (chave SSH) for criado.
  
    ```
    output "ssh_key_id" {
      value = "${ibmcloud_infra_ssh_key.ssh_key.id}"
    }
    ```
    {:screen}
  
Agora é possível criar um ambiente por meio de sua configuração. 

{:codeblock}

## Criando um Ambiente
{: #environment}

Ao criar um ambiente, você aponta o serviço para sua configuração para que o serviço possa extrair suas mudanças de código mais recentes.
{:shortdesc}

Usando a configuração de amostra, conclua as etapas a seguir para criar um ambiente.

1. No menu, selecione **Serviços** e, em seguida, **{{site.data.keyword.bpshort}}**. Você é levado para o painel do {{site.data.keyword.bpshort}}.

2. No menu de navegação esquerdo, selecione **Ambientes** e clique em **Criar ambiente** para descrever as propriedades sobre sua configuração. A criação de um ambiente define como o {{site.data.keyword.bpshort}} provisiona e atualiza os recursos em nuvem, mas não cria os recursos ainda.

3. Insira detalhes sobre seu ambiente. A configuração de amostra requer os valores que estão listados na tabela a seguir.

  <table summary="Os valores necessários para que você possa usar a configuração de amostra como a origem de seu ambiente.">
  <caption>Tabela 1. Os valores necessários para que você possa usar a configuração de amostra como a origem de seu ambiente.
  </caption>
  <thead>
  <th colspan="1">A</th>
  <th colspan="1">Descrição</th>
  </thead>
  <tbody>
  <tr>
  <td>URL do controle de versão</td>
  <td>Insira a URL do GitHub na qual você bifurcou a configuração de amostra.</td>
  </tr>
  <tr>
  <td>Nome de  ausente</td>
  <td>Insira um nome exclusivo para designar a seu ambiente.</td>
  </tr>
  <td>Versão do Terraform</td>
  <td>Insira a versão do Terraform para assegurar-se de que uma versão compatível do Terraform seja executada em seu ambiente. Para a configuração de amostra, use a versão <code>0.9.1</code>.</td>
  </tr>
  <tr>
  <td>Variáveis</td>
  <td>É possível definir variáveis no serviço ou substituir as variáveis de ambiente que estão nos arquivos <code>.tf</code>. É possível mascarar variáveis sensíveis ao clicar no ícone de bloqueio. O mascaramento de variáveis evita que outros usuários vejam os valores ocultos na página de detalhes do ambiente.
  <p>
  <p>Inclua as variáveis e os valores a seguir para funcionar com a configuração de amostra:
  <ul>
  <li><code>ibmid</code> - Insira seu {{site.data.keyword.ibmid}} integral como o valor.</li>
  <li><code>ibmidpw</code> - Insira a senha que está associada a seu {{site.data.keyword.ibmid}} e clique no ícone de bloqueio para mascarar o valor.</li>
  <li><code>slaccountnum</code> - Insira seu número da conta do {{site.data.keyword.BluSoftlayer}}.
   <li><code>datacenter</code> - Insira o datacenter no qual você deseja implementar o recurso de chave SSH. Veja o <a href="https://github.com/IBM-Bluemix/tf-bluemix-ssh-key/blob/master/README.md" target="_blank">arquivo leia-me <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a> para obter uma lista completa de valores disponíveis.</li> 
   <li><code>public_key</code> - Insira a chave SSH pública. Para copiar a chave pública para a área de transferência, será possível executar o comando <code>pbcopy < ~/.ssh/id_rsa.pub</code>.
   <li><code>key_label</code> - Identifique a chave com um nome exclusivo.
   <li><code>key_note</code> - Opcional: inclua texto descritivo sobre a chave SSH.</ul></td>
   </tr></tbody></table>

4. Quando você tiver terminado de preencher os detalhes do ambiente, clique em **Criar**. O ambiente recém-criado será exibido. 
5. Para ver uma visualização de quais recursos foram provisionados ou removidos durante a implementação de seu ambiente, clique em **Plano**. 
6. Visualize o log do plano para inspecionar se há erros na saída. 
7. Quando você estiver pronto para ativar seu ambiente, clique em **Aplicar**. Será possível monitorar o log de aplicação para ver ser a chave foi implementada com sucesso. Uma implementação bem-sucedida mostra a linha a seguir em direção ao término da saída:

  ```
  Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
  ```
  {: screen}

  Também é possível visualizar a chave SSH no [{{site.data.keyword.slportal}}](https://control.bluemix.net/devices/sshkeys).
8. Opcional: para remover a chave SSH e remover o ambiente do {{site.data.keyword.Bluemix_notm}}, selecione **Destruir recursos** no menu Ações.

### O que vem a seguir
{: #next}

* Para descobrir mais sobre como implementar programaticamente seus ambientes, [efetue check-out da CLI ou da API](schematics_deploying.html).
* Para criar suas próprias configurações do zero, efetue check-out dos <a href="https://ibm-bluemix.github.io/tf-ibm-docs/">recursos do {{site.data.keyword.IBM_notm}} Cloud <img src="../../icons/launch-glyph.svg" alt="Ícone de link externo"></a>. Os recursos do {{site.data.keyword.IBM_notm}} Cloud ficam disponíveis como um provedor de plug-in do Terraform.
