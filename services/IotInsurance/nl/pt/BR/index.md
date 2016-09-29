---

copyright:
  years: 2016

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# Introdução ao {{site.data.keyword.iotinsurance_short}} (Beta)
{: #iotins_gettingstarted}
Última atualização: 12 de setembro de 2016
{: .last-updated}

O {{site.data.keyword.iotinsurance_full}} é um serviço {{site.data.keyword.Bluemix_notm}} que pode ser usado para coletar, gerenciar e analisar dados de segurados conectados. O {{site.data.keyword.iotinsurance_short}} oferece a capacidade de fornecer avaliação de risco personalizada, proteção em tempo real e reduções de custo de política.
{:shortdesc}

Para que este serviço funcione, deve-se implementar os serviços e aplicativos necessários e, em seguida, configurar os serviços.

**Pré-requisitos:** antes de iniciar, assegure-se de que os pré-requisitos a seguir estejam adequados:
- Deve existir uma instância do [serviço {{site.data.keyword.iotinsurance_short}}](https://new-console.ng.bluemix.net/catalog/services/iot-for-insurance/) no espaço do {{site.data.keyword.Bluemix_notm}}.
- Pelo menos 10 GB de armazenamento devem estar disponíveis em seu computador.

## Implementando os serviços e os aplicativos necessários
{: #deploying_services}

1. Para implementar todos os serviços e aplicativos necessários, no painel do {{site.data.keyword.Bluemix_notm}}, clique no tile do serviço {{site.data.keyword.iotinsurance_short}} e, em seguida, clique em **Implementar**.

  O {{site.data.keyword.iotinsurance_short}} implementa todos os serviços e aplicativos Node.js que ele requer. Ele automaticamente liga os aplicativos aos serviços.

  Cada instância de serviço usa o plano de serviço padrão. É possível fazer upgrade de qualquer plano de serviço posteriormente acessando o console do serviço. Também é possível usar uma instância existente de um serviço excluindo a nova instância e ligando manualmente a instância existente ao serviço {{site.data.keyword.iotinsurance_short}}. Para obter mais informações sobre os aplicativos, consulte [Sobre o {{site.data.keyword.iotinsurance_short}}](iotinsurance_overview.html).

2. Verifique se todos os serviços e aplicativos estão criados e funcionando adequadamente. Em seu painel do {{site.data.keyword.Bluemix_notm}}, verifique se todos os aplicativos possuem um status de `Em execução`.

3. Verifique se o painel do {{site.data.keyword.iotinsurance_short}} está funcional e se é possível acessar as APIs.
  1. Clique no quadro do serviço {{site.data.keyword.iotinsurance_short}} e, em seguida, selecione a guia **Credenciais de serviço**.
  2. Clique em **Visualizar credenciais de serviço** e anote o ID do usuário e a Senha. Você usará essas credenciais nas etapas a seguir.
  3. Abra o painel do {{site.data.keyword.iotinsurance_short}} selecionando a guia **Gerenciar** e clicando em **Abrir**.
  4. Visualize as APIs, clicando em **APIs**.

## Configurando os serviços
{: #iot4i_configservices}
Execute as tarefas a seguir para configurar os serviços:

### Configurando o {{site.data.keyword.amashort}}
{: #config_ama}
1. Identifique a URL base do aplicativo da API do {{site.data.keyword.iotinsurance_short}}. Essa URL é exibida no tile do aplicativo e está no formato *appName*-api.mybluemix.net.

2. Abra o serviço {{site.data.keyword.amashort}}.

3. Na seção **Customizado**, clique em **Configurar** e, em seguida, insira as credenciais de autenticação a seguir:

  - **Nome da região**: `IoT4I`

  - **URL do provedor de identidade customizado**: a URL do aplicativo API no formato a seguir:
  ```
  https://appName-api.mybluemix.net
  ```

  - **URIs de redirecionamento de seu aplicativo da web**: deixe esse campo em branco.

### Configurando o {{site.data.keyword.mobilepushshort}}
{: #config_push}
Para ativar notificações push para um app móvel existente, deve-se configurar o serviço {{site.data.keyword.mobilepushshort}} e incluir um arquivo de Padrões de Criptografia de Chave Pública (PKCS) 12. 
Para obter informações sobre o aplicativo móvel, consulte [Instalando e conectando o aplicativo móvel de amostra](iotinsurance_mobile_app.html). Para obter informações sobre o {{site.data.keyword.mobilepushshort}}, consulte [Introdução ao Push Notifications](https://new-console.stage1.ng.bluemix.net/docs/services/mobilepush/index.html).

  1. Abra o serviço {{site.data.keyword.mobilepushshort}}.
  2. Clique em **Configurar Push**.
  3. Na seção Certificado do Apple Push Notifications, faça upload do arquivo PKCS 12 para seu app móvel e insira a senha.

O que Vem a Seguir?
{: #whats_next}
Veja o que é possível fazer com o {{site.data.keyword.iotinsurance_short}}.

- Criar uma [associação de usuário e blindagem](iotinsurance_create_users.html).
- Instalar e conectar o [aplicativo móvel de amostra](iotinsurance_mobile_app.html).
- Melhorar o desempenho com [serviços avançados](iotinsurance_advancedservices.html).
- Visualizar as [APIs](https://iot4i-docs-api.mybluemix.net/dist/).

# Links Relacionados
{: #rellinks}

## Tutoriais e amostras
{: #samples}
* [Código do aplicativo móvel de amostra no Github](https://github.com/ibm-watson-iot/ioti-mobile){:new_window}

## Referência de API
{: #api}
* [Exemplos de API do {{site.data.keyword.iotinsurance_short}}](https://iot4i-docs-api.mybluemix.net/dist/){:new_window}

## Links Relacionados
{: #general}
* [Documentação do {{site.data.keyword.iot_full}}](https://new-console.ng.bluemix.net/docs/services/IoT/index.html)
* [Fórum de suporte do desenvolvedor](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
* [Fórum de suporte do Stack overflow](http://stackoverflow.com/questions/tagged/ibm-bluemix)
