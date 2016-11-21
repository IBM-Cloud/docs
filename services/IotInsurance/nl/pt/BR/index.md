---

copyright:
  years: 2016
lastupdated: "2016-10-26"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# Introdução ao {{site.data.keyword.iotinsurance_short}}

O {{site.data.keyword.iotinsurance_full}} é um serviço {{site.data.keyword.Bluemix_notm}} que pode ser usado para coletar, gerenciar e analisar dados de segurados conectados. O {{site.data.keyword.iotinsurance_short}} oferece a capacidade de fornecer avaliação de risco personalizada, proteção em tempo real e reduções de custo de política.
{:shortdesc}

Para que este serviço funcione, deve-se implementar os serviços e aplicativos necessários e, em seguida, configurar os serviços. Encontre
uma visão geral dos serviços e do app e um diagrama de arquitetura em [Sobre
o {{site.data.keyword.iotinsurance_short}}](iotinsurance_overview.html)

**Pré-requisitos:** antes de iniciar, assegure-se de que os pré-requisitos a seguir estejam adequados:
- Uma instância do [serviço do {{site.data.keyword.iotinsurance_short}}](https://console.ng.bluemix.net/catalog/services/iot-for-insurance/) deve existir em
seu espaço do {{site.data.keyword.Bluemix_notm}}.
- Pelo menos 2 GB de memória livre devem estar disponíveis em sua organização {{site.data.keyword.Bluemix_notm}} para ativar a função Implementar.

## Implementando os serviços e os aplicativos necessários
{: #deploying_services}

1. Para implementar todos os serviços e aplicativos necessários, no [console do{{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net/#all-items), clique no serviço do {{site.data.keyword.iotinsurance_short}} e, em seguida, clique em **Implementar**.

  O {{site.data.keyword.iotinsurance_short}} implementa todos os serviços e aplicativos Node.js que ele requer. Ele automaticamente liga os aplicativos aos serviços.

  Cada instância de serviço usa o plano de serviço padrão. É possível fazer upgrade de qualquer plano de serviço posteriormente acessando o console do serviço. Também é possível usar uma instância existente de um serviço excluindo a nova instância e ligando manualmente a instância existente ao serviço {{site.data.keyword.iotinsurance_short}}. Para obter mais informações sobre os aplicativos, consulte [Sobre o {{site.data.keyword.iotinsurance_short}}](iotinsurance_overview.html).

2. Verifique se o painel do {{site.data.keyword.iotinsurance_short}} está funcional e se é possível acessar as APIs.
  1. Abra o painel do {{site.data.keyword.iotinsurance_short}} clicando em
**Abrir**. Aceite as credenciais pré-preenchidas clicando em
**Login**.
  2. Retorne ao console de serviço do
{{site.data.keyword.iotinsurance_short}} e visualize as APIs clicando em
**APIs**.

  **Nota:** Após a implementação, é possível acessar o painel ou
as APIs diretamente inserindo as respectivas URLs em seu navegador. Quando você usa esse
método, deve-se inserir suas credenciais de serviço do
{{site.data.keyword.iotinsurance_short}}. Para localizar suas credenciais,
retorne ao console de serviço do {{site.data.keyword.iotinsurance_short}}. Clique
na guia **Credenciais de serviço** e, em seguida, clique em
**Visualizar credenciais**. Anote o ID do usuário e a senha.

## Configurando os serviços
{: #iot4i_configservices}
Execute as tarefas a seguir para configurar os serviços:

### Configurando o {{site.data.keyword.amashort}}
{: #config_ama}
1. Retorne ao console do Bluemix. Todos os apps e serviços que foram implementados pelo {{site.data.keyword.iotinsurance_short}} são exibidos.

1. Copie a URL do aplicativo de API do {{site.data.keyword.iotinsurance_short}}. Clique com o botão direito no aplicativo de API e selecione **Copiar local do link**.

2. Abra o serviço {{site.data.keyword.amashort}}. O serviço está disponível na seção Serviços do seu console do {{site.data.keyword.Bluemix_notm}}.

3. Ative a autenticação clicando em **Ativo**.

4. Na seção **Customizado**, clique em **Configurar** e, em seguida, insira as credenciais de autenticação a seguir:

  - **Nome da região**: `IoT4I`

  - **URL do provedor de identidade customizado**: cole a URL do aplicativo da API que você copiou na primeira etapa.

  - **URIs de redirecionamento de seu aplicativo da web**: deixe esse campo em branco.

5. Salve suas configurações. Agora é possível retornar ao console de serviço do
{{site.data.keyword.iotinsurance_short}} ou ao console do
{{site.data.keyword.Bluemix_notm}}.

### Configurando o {{site.data.keyword.mobilepushshort}}
{: #config_push}
Para ativar notificações push para um app móvel existente, deve-se configurar o serviço {{site.data.keyword.mobilepushshort}} e incluir um arquivo de Padrões de Criptografia de Chave Pública (PKCS) 12. Para obter informações sobre o aplicativo móvel, consulte [Instalando e conectando o aplicativo móvel de amostra](iotinsurance_mobile_app.html). Para obter informações sobre o {{site.data.keyword.mobilepushshort}}, consulte [Introdução ao Push Notifications](https://console.stage1.ng.bluemix.net/docs/services/mobilepush/index.html).

  1. Abra o serviço {{site.data.keyword.mobilepushshort}}.
  2. Clique em **Configurar**.
  3. Na seção Certificado do Apple Push Notifications, faça upload do arquivo PKCS 12 para seu app móvel e insira a senha.


O que Vem a Seguir?
{: #whats_next}
Veja o que é possível fazer com o {{site.data.keyword.iotinsurance_short}}.

- Usar as instruções e APIs no Shield Toolkit para criar uma [associação de usuário e blindagem](iotinsurance_shield_toolkit.html).
- Instalar e conectar o [aplicativo móvel de amostra](iotinsurance_mobile_app.html).
- Fazer download ou visualizar todas as [APIs no site do GitHub](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples).

# Links Relacionados
{: #rellinks}

## Tutoriais e amostras
{: #samples}
* [Código de app móvel de amostra no GitHub](https://github.com/ibm-watson-iot/ioti-mobile){:new_window}

## Referência de API
{: #api}
* [API do {{site.data.keyword.iotinsurance_short}}](https://iot4i-api-docs.mybluemix.net/){:new_window}
* [Exemplos de API do {{site.data.keyword.iotinsurance_short}}](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){:new_window}


## Links Relacionados
{: #general}
* [Documentação do {{site.data.keyword.iot_full}}](https://console.ng.bluemix.net/docs/services/IoT/index.html)
* [Fórum de suporte do desenvolvedor](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
* [Fórum de suporte do Stack overflow](http://stackoverflow.com/questions/tagged/ibm-bluemix)
