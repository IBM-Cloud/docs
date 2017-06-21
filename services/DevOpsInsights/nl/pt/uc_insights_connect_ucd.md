---

copyright:
  years: 2017
lastupdated: "2017-05-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Mostrando dados de servidores IBM UrbanCode Deploy
{: #connect_ucd}

Para ver os dados de um servidor IBM UrbanCode Deploy no Delivery Insights, deve-se configurar uma instância do DevOps Connect, instalar uma correção no servidor e, em seguida, conectar esse servidor ao DevOps Connect.
{:shortdesc}

## Pré-Requisitos
{: #prereqs}

Para ver informações dos servidores IBM UrbanCode Deploy no {{site.data.keyword.DRA_short}}, deve-se hospedar uma instância do DevOps Connect em um sistema que possa se conectar aos servidores IBM UrbanCode Deploy. Esse sistema pode ser um computador físico ou uma máquina virtual. 

O sistema que hospeda o DevOps Connect deve ter os pré-requisitos a seguir:
- O sistema deve ter um Java Runtime Environment (JRE) versão 8 ou mais recente.
- A variável `PATH` do sistema deve incluir o local do JRE.
- O sistema deve permitir que o DevOps Connect crie conexões de saída para o IBM Bluemix.

Além disso, seu servidor IBM UrbanCode Deploy deve estar na versão 6.2 ou mais recente.

## Configurado o serviço {{site.data.keyword.DRA_short}}
{: #configure_service}

Se você não tiver uma cadeia de ferramentas ou o {{site.data.keyword.DRA_short}}, o {{site.data.keyword.DRA_short}} deverá ser configurado primeiro:
1. No catálogo do {{site.data.keyword.Bluemix}}, clique em **{{site.data.keyword.DRA_short}}**, selecione um plano de precificação e clique em **Criar**.
1. Clique na guia **Gerenciar** e, em seguida, acima de **Obter insights em implementações do UrbanCode**, clique em **Iniciar aqui**. No plano de fundo, o Delivery Insights cria uma cadeia de ferramentas para sua organização. Cadeias de ferramentas são coleções de integrações de ferramentas e, nesse caso, o IBM UrbanCode Deploy e o {{site.data.keyword.DRA_short}} são parte de sua cadeia de ferramentas. Para obter mais informações sobre cadeias de ferramentas, veja [Trabalhando com cadeias de ferramentas](../ContinuousDelivery/toolchains_working.html).

Se você já tiver uma cadeia de ferramentas, siga estas etapas para incluir o Delivery Insights:
1. Se você ainda não tiver a ferramenta {{site.data.keyword.DRA_short}}, inclua-a em sua cadeia de ferramentas.
1. Na cadeia de ferramentas, clique na ferramenta {{site.data.keyword.DRA_short}}.
1. Acesse a página **Configurações > Configurações do Delivery Insights**.

Agora é possível seguir as instruções na página **Configuração do Delivery Insights** para instalar o DevOps Connect e conectá-lo ao {{site.data.keyword.DRA_short}}, conforme descrito na próxima seção.

## Instalando o DevOps Connect e conectando-o ao {{site.data.keyword.DRA_short}}
{: #install_connect}

1. Na página **Configuração do Delivery Insights**, siga as etapas para configurar o DevOps Connect e conecte os servidores IBM UrbanCode Deploy. Estas etapas incluem:
{: #set_up_connect}
  1. Configure um sistema para executar o DevOps Connect, conforme descrito em [Pré-requisitos](uc_insights_connect_ucd.html#prereqs).
  1. Faça download do DevOps Connect, que é fornecido em um arquivo JAR executável.
  1. Copie o script da página **Configuração do Delivery Insights** e execute-a. Esse comando inicia o DevOps Connect com um token que permite que ele se conecte à sua organização no {{site.data.keyword.Bluemix}}.
  1. Conecte seus servidores IBM UrbanCode Deploy ao DevOps Connect, conforme descrito na próxima seção.

## Conectando os servidores IBM UrbanCode Deploy ao DevOps Connect
{: #connect_ucd_to_connect}

1. Instale a correção no servidor IBM UrbanCode Deploy. Todas as versões do IBM UrbanCode Deploy requerem uma correção para se comunicar com o DevOps Connect. 
  1. Faça download da correção correta para sua versão do IBM UrbanCode Deploy acessando a página a seguir e fazendo download da correção correta:
  [http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/)

  1. Extraia o arquivo. Ele contém um ou mais arquivos de correção que devem ser incluídos no servidor.

  1. Pare o servidor. Veja [Iniciando e parando o servidor](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.4/com.ibm.udeploy.install.doc/topics/run_server.html).

  1. Coloque os arquivos de correção na pasta <code><em>application_data</em>/patches</code>, em que <code><em>application_data</em></code> é a pasta de dados do aplicativo do servidor. A pasta de dados do aplicativo padrão é `/opt/ibm-ucd/server/appdata` no Linux e `C:\Program Files\ibm-ucd\server\appdata` no Windows. Em sistemas de alta disponibilidade, a pasta de dados do aplicativo está sempre em uma unidade de rede compartilhada que cada servidor pode acessar.

  1. Opcional: enquanto o servidor estiver interrompido, para aumentar o desempenho da importação de dados desse servidor, execute os comandos SQL a seguir no banco de dados:  
  `create index rt_cpr_submitted_time on MyUCDDatabase.rt_app_process_request(submitted_time);`  
  `create index rt_cpr_submitted_time on MyUCDDatabase.rt_comp_process_request(component_id, submitted_time);`  
  Use o nome de seu banco de dados para `MyUCDDatabase`.
  
  <!-- Ross says that this will not be necessary for versions 6.2.4.1 and later if he gets his code changes in. -->

  1. Inicie o servidor. 

    **Nota:** talvez seja necessário esperar mais do que o normal para o servidor IBM UrbanCode Deploy iniciar. Se o servidor não for finalmente iniciado ou não estiver funcionando corretamente, exclua os arquivos de correção e, em seguida, reinicie o servidor.Os arquivos de correção não afetam permanentemente o servidor.

1. Algumas versões do IBM UrbanCode Deploy requerem uma correção adicional para que o servidor se conecte ao DevOps Connect. Se estiver usando o IBM UrbanCode Deploy versão 6.2 à 6.2.1.2, a correção adicional a seguir deverá ser instalada no servidor:
  1. Faça download da correção: [http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/ucd-6.2.1.1-WI149200-CLI-Updates-for-UCSync.jar](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/ucd-6.2.1.1-WI149200-CLI-Updates-for-UCSync.jar).
  1. Pare o servidor.
  1. Coloque o arquivo de correção na pasta <code><em>application_data</em>/patches</code>.
  1. Inicie o servidor.

1. Crie uma integração entre o DevOps Connect e o servidor IBM UrbanCode Deploy:  

  **Importante:** na primeira vez que a integração for executada, o DevOps Connect recuperará dados dos 90 dias anteriores. Se você tiver uma grande quantia de dados de implementação, esse processo poderá levar muito tempo. Para recuperar dados para menos de 90 dias, veja [Resolução de problemas](uc_insights_connect_ucd.html#troubleshooting).
  1. No IBM UrbanCode Deploy, crie um token de autenticação. Veja [Tokens](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.4/com.ibm.udeploy.admin.doc/topics/security_token.html).
  1. No DevOps Connect, clique em **Integrações** e, em seguida, clique em **Incluir novo**.
  1. Especifique um nome e uma descrição para a integração. O local padrão do DevOps Connect é `https://hostname:8443/`, em que `hostname` é o nome do host do sistema que hospeda o DevOps Connect.
  1. Na lista **Tipo de integração**, selecione **IBM UrbanCode Deploy for Cloud Reporting**.
  1. No campo **URI do servidor**, insira a URL pública do servidor IBM UrbanCode Deploy, como `https://my_UCD.example.com:8447`.
  1. No campo **Token de autenticação**, insira ou cole o token de autenticação que foi gerado pelo IBM UrbanCode Deploy.
  1. No campo **Usuário administrador**, insira uma lista separada por vírgula de IBMids para fornecer acesso à interface do DevOps Connect.
  1. Opcional: clique em **Executar integração** para executar a integração imediatamente. Por padrão, as integrações são executadas a cada minuto.
  1. Clique em **Salvar**.

  ![Configurando a integração no DevOps Connect](images/uc_insights_dc_integration.gif)

Agora seus dados estão sincronizados com o Delivery Insights. Agora é possível criar e visualizar relatórios que se baseiam nesses dados. Em seguida, mapeie os ambientes em seus servidores IBM UrbanCode Deploy para ambientes lógicos no Delivery Insights.

## Mapeando ambientes para relatórios
{: #mapping}

### Ambientes lógicos

O Delivery Insights agrupa seus ambientes do IBM UrbanCode Deploy (também chamados de *ambientes físicos*) em um ou mais ambientes lógicos. Dessa forma, é possível coletar ambientes em grupos que façam sentido para você e sua organização. Por exemplo, se você tiver vários ambientes de produção para vários aplicativos, será possível agrupar todos esses ambientes em um único ambiente lógico e combinar métricas para todos esses ambientes em um único painel do ambiente de produção. O mapeamento acontece por sequência de procura, portanto, é possível agrupar ambientes de qualquer maneira que faça sentido para os servidores IBM UrbanCode Deploy.

### Ambientes lógicos padrão

Por padrão, seus relatórios incluem ambientes lógicos que correspondem a ambientes do IBM UrbanCode Deploy usando sequências. Por exemplo, todos os ambientes com "dev" no nome são mapeados para o ambiente lógico DEV e todos os ambientes com "prod" no nome são mapeados para o ambiente lógico PROD.

![Os ambientes lógicos padrão](images/uc_insights_mapping.gif)

### Mapeando ambientes para ambientes lógicos

É possível mapear manualmente os ambientes físicos para ambientes lógicos ou usar padrões para associar ambientes físicos a ambientes lógicos dinamicamente.

Para mapear ambientes físicos para ambientes lógicos usando um padrão, siga estas etapas:

1. No {{site.data.keyword.DRA_short}}, clique em **Delivery Insights > Mapear ambientes**.
1. Clique em um ambiente lógico existente ou clique em **Incluir ambiente lógico**.
1. Nas configurações para o ambiente lógico, em **Padrões**, clique em **Incluir padrão**.
1. Especifique um padrão para nomes de ambiente. É possível usar o asterisco (*) como um curinga. Por exemplo, o padrão `env` corresponde aos ambientes `env1`, `env2` e `env`.
1. Verifique se o ambiente lógico contém os ambientes que você deseja.

Para mapear ambientes para ambientes lógicos manualmente, clique em **Incluir manualmente** e selecione os ambientes a serem incluídos ou removidos.

![Configurando a integração no DevOps Connect](images/uc_insights_mapping_manually.gif)

Agora que você mapeou os ambientes para ambientes lógicos, é possível agregar informações de relatório por esses ambientes lógicos.

## Criando Relatórios

Para criar um relatório, abra o {{site.data.keyword.DRA_short}}, clique em **Delivery Insights > Relatórios** e, em seguida, clique em **Incluir relatório**. 

De dentro do relatório, é possível incluir cartões na seção **Métricas**, filtrar a atividade em **Atividade recente do aplicativo** e incluir gráficos na seção **Detalhes do relatório**. Cada gráfico na seção **Detalhes do relatório** é individualmente filtrável e customizável. Para ver os dados brutos atrás de um gráfico, na parte superior direita do gráfico, clique no botão Configurações do gráfico e, em seguida, clique em **Dados do relatório**.

Para mudar a ordem dos gráficos, na parte superior direita da página, clique no botão Configurações e, em seguida, clique em **Editar layout do gráfico**. Em seguida, é possível arrastar e soltar os gráficos para configurar a ordem no relatório.

## Compartilhando Relatórios
Por padrão, somente você pode ver os relatórios do Delivery Insights. É possível compartilhar o relatório com outros usuários na organização do Bluemix. Para compartilhar um relatório com alguém na organização do Bluemix, abra o relatório e, em seguida, na parte superior direita do relatório, clique no botão Configurações e, em seguida, clique em **Compartilhar**.  

![Compartilhando um relatório](images/uc_insights_sharing.gif).

## Criando Relatórios de Auditoria

Os relatórios de auditoria mostram uma lista completa de toda a atividade que atende aos filtros configurados, como um PDF. Para criar um relatório de auditoria, clique em **Delivery Insights > Criar relatório de auditoria**. Em seguida, especifique as informações para o relatório, incluindo um nome. Além disso, configure o contexto para o relatório, como para um aplicativo, um ambiente lógico ou um ambiente em um servidor IBM UrbanCode Deploy (um ambiente físico). Daí, selecione os dados a serem mostrados no relatório e clique em **Criar**. 

## Resolver problemas
{: #troubleshooting}

Se várias solicitações de aplicativos e de processos do componente forem armazenadas no banco de dados do servidor IBM UrbanCode Deploy, poderão ocorrer erros durante o processo de recuperação. Uma mensagem semelhante ao texto a seguir é gravada no log de saída do servidor:

`ORA-01652: unable to extend temp segment by 128 in tablespace TEMP`

Para contornar esse comportamento, edite o arquivo `plugin.properties` para que o plug-in reduza o número de dias de dados válidos a serem recuperados. O arquivo `plugin.properties` está no diretório `~/.ibm/cloud-sync/plugins/settings/reporting-ucd-plugin/` no computador em que o DevOps Connect foi instalado. Edite a linha a seguir para remover o sinal de número (#) e reduzir o número de dias:

`#numDaysToRetrieve=90`

Por exemplo, mude a linha para o texto a seguir para recuperar apenas os 30 dias anteriores de dados válidos:

`numDaysToRetrieve=30`

Salve o arquivo e, em seguida, execute a integração novamente. Verifique os logs do servidor para assegurar-se de que o erro não ocorra mais.
