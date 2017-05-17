---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-15"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Gerenciando seus dados e dispositivos
{: #iot4e_dashboard}
Visualize os dados por meio dos dispositivos registrados e gerencie seus dispositivos e usuários no {{site.data.keyword.iot_full}} com o
painel do {{site.data.keyword.iotelectronics}}.
{:shortdesc}

Use o painel do {{site.data.keyword.iotelectronics}} para
- Visualizar dispositivos registrados em sua organização
- Mapear usuários para dispositivos
- Executar ações em massa, como incluir e excluir grandes números de dispositivos
- Extrair dados do dispositivo

## Abrindo o painel
{: #iot4e_opendashboard}

**Importante:** antes de poder usar o painel pela primeira vez, deve-se [ativá-lo](#iot4e_enabledashboard).

Para abrir o painel
1. Abra seu painel do {{site.data.keyword.Bluemix_notm}} e clique no nome do serviço do {{site.data.keyword.iot_short_notm}}.  

    **Dica:** o nome do serviço termina com `iotf-service` e é descrito como *Internet of Things Platform* na coluna Oferta de serviços.
2. Na página de boas-vindas, clique em **Ativar**.
3. No menu, selecione **Eletroeletrônico**.

## Ativando o painel
{: #iot4e_enabledashboard}

Ative o painel do {{site.data.keyword.iotelectronics}} no {{site.data.keyword.iot_full}} executando as etapas a seguir.

  **Nota:** antes de iniciar, deve-se implementar uma instância do iniciador do {{site.data.keyword.iotelectronics}} em sua organização do {{site.data.keyword.Bluemix_notm}}. Implementar uma instância do iniciador
automaticamente implementa os aplicativos e serviços de componente, incluindo {{site.data.keyword.iot_short_notm}}.

1. Inclua uma nova função na chave API do {{site.data.keyword.iot_short_notm}}.
  1. Abra seu painel do {{site.data.keyword.Bluemix_notm}} e clique no nome do serviço do {{site.data.keyword.iot_short_notm}}.  

    **Dica:** o nome do serviço termina com `iotf-service` e é descrito como *Internet of Things Platform* na coluna Oferta de serviços.
  2. Na página de boas-vindas, clique em **Ativar**.
  3. No menu, selecione **Apps** ![ícone de apps](images/IOT_Icons_apps2.svg "Ícone de Apps") e, em seguida, clique no ícone de edição ![ícone de edição](images/IOT_Icons_Edit_Active_50.svg "Ícone de Edição") ao lado da chave API.
  4. Clique em **Incluir outra função** e selecione **Aplicativo de operações**.
  5. Clique em **Salvar**.

    ![Funções da API](images/IoT4E_API_roles.svg "Funções da API")

2. Localize o ID da organização, a chave API e o código de autenticação do {{site.data.keyword.iot_short_notm}}.
  1. Retorne para o painel do {{site.data.keyword.Bluemix_notm}}.
  2. Abra o aplicativo {{site.data.keyword.iotelectronics}}.

    **Dica:** o aplicativo está localizado na seção Aplicativos do seu painel do {{site.data.keyword.Bluemix_notm}}. Assegure-se de clicar no nome e não na rota.
  3. Exiba as variáveis de ambiente, clicando em **Tempo de execução** e, em seguida, selecione **Variáveis de ambiente**.
  4. Role para a seção rotulada `iotf-service`. Copie os valores a seguir. Eles serão necessários na próxima etapa.

    - `org` - o ID da organização do {{site.data.keyword.iot_short_notm}}
    - `apiKey` - a chave API do {{site.data.keyword.iot_short_notm}}
    - `apiToken` - o token de autenticação do {{site.data.keyword.iot_short_notm}}  

    ![Credenciais de autenticação de API](images/IoT4E_IoTFcred.svg "Credenciais de autenticação de API")

3. Insira as credenciais do {{site.data.keyword.iot_short_notm}} no serviço do {{site.data.keyword.iotelectronics}}.

  1. Retorne para o painel do {{site.data.keyword.Bluemix_notm}}.
  2. Abra o serviço do {{site.data.keyword.iotelectronics}} clicando no nome do serviço.

    **Dica:** o nome do serviço termina com `ibmiotforelectronics` e é descrito como *IoT for Electronics* na coluna Oferta de serviços.
  3. Na página de boas-vindas, insira a chave API, o token de autenticação e um ID de organização que você localizou na etapa anterior.
  4. Clique em **Atualizar** para salvar suas entradas.

    ![Configuração da plataforma](images/IoT4E_Platform_config.svg "Configuração da plataforma")

4. Agora é possível [abrir o painel do {{site.data.keyword.iotelectronics}}](#iot4e_opendashboard) no {{site.data.keyword.iot_short_notm}}.
