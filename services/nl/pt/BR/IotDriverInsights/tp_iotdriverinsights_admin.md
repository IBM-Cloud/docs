---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Administrando o Trajectory Pattern Analysis
{: #tp_iotdriverinsights_admin}

Última atualização: 22 de julho de 2016
{: .last-updated}

Para administrar o serviço Trajectory Pattern Analysis, use o console de administração no painel do {{site.data.keyword.Bluemix_notm}}. No console de administração, é possível configurar parâmetros para o Trajectory Pattern Analysis e gerenciar os dados armazenados no serviço. Também é possível visualizar as informações do locatário e reconfigurar a senha do locatário.

{:shortdesc}

## Iniciando o console de administração
{: #start-admin-console}

Para acessar o console de administração do serviço Trajectory Pattern Analysis do {{site.data.keyword.iotdriverinsights_full}}

1. No painel do {{site.data.keyword.Bluemix_notm}}, clique no quadro do serviço {{site.data.keyword.iotdriverinsights_short}}.
2. Selecione a visualização **Gerenciar** de sua instância de serviço.
Anote as credenciais de nome de usuário e de senha porque elas vão ser necessárias mais tarde. Para acessar o console de administração, seu ID IBM será necessário, que pode não ser o mesmo de suas credenciais do {{site.data.keyword.Bluemix_notm}}.
3. Clique em **Ativar** e, quando solicitado, insira suas credenciais de ID IBM.
4. Clique em **EFETUAR LOGIN**. A janela **Console do administrador** é aberta.


## Gerenciando informações do locatário
{: #viewtenantinfo}

Para visualizar as informações do locatário, clique em **Informações do locatário**.

### Reconfigurando a senha do locatário
{: #resettenantpassword}

Para reconfigurar a senha do locatário:

1. Na janela **Informações do locatário**, clique em **RECONFIGURAR**.
2. Na caixa de diálogo de confirmação, clique em **OK**.
Uma nova senha é gerada e exibida na visualização **Informações do locatário**.
**Importante:** certifique-se de atualizar a senha em todos os aplicativos que acessam a API do {{site.data.keyword.iotdriverinsights_short}}.

## Configurando os parâmetros de serviço
{: #configureparameters}

Os parâmetros de serviço controlam o modo de análise dos dados da viagem. Para modificar os parâmetros de serviço do Trajectory Pattern Analysis:

1. Abra a visualização **Parâmetros**.
2. Clique na guia **Parâmetros do Padrão de trajetória** e atualize os [parâmetros de análise do padrão de trajetória](#tp_parameters) para se adequarem a seus requisitos.
3. Clique em **SALVAR**.
4. Clique em **OK**.

Os valores de parâmetro atualizados serão aplicados à próxima tarefa que for enviada.

### Parâmetros de limite de suporte

A tabela a seguir descreve os parâmetros de limite de suporte que podem ser configurados na guia **Parâmetros do Padrão de trajetória**.

|Nome do parâmetro|Description|Valor Padrão|
|:--------|:--------|:-------|
|Suporte mínimo de números de viagens para um O/D|Os números de viagens de suporte mínimo absoluto necessários para um padrão de O/D (Origem/Destino)|4 (deve ser mais de zero)|
|Suporte mínimo de números de viagens para uma rota|Os números de viagens de suporte mínimo absoluto necessários para um padrão de rota|2 (deve ser mais de zero)|

## Gerenciando os dados de resultados
{: #managedata}

Os dados de resultados gerados pela análise de dados do serviço Trajectory Pattern Analysis são armazenados no sistema até serem excluídos.

Para excluir os dados de resultados:

1. Clique em **Gerenciamento de dados** > **Resultado do Padrão de trajetória**. Os dados de resultados são exibidos.
2. Selecione um registro e, em seguida, clique em **EXCLUIR**.
